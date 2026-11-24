
clc;
clear;
close all;
format short;

%% =====================================================
% 1. PARAMETER SALURAN IRIGASI
% ======================================================

b = 1.0;           % Lebar dasar saluran (m)
m = 1.0;           % Kemiringan talud
S = 0.0005;        % Kemiringan dasar saluran
k = 70;            % Koefisien Strickler
n = 1/k;           % Koefisien Manning
g = 9.81;          % Percepatan gravitasi (m/s2)
H = 0.9;           % Tinggi saluran (m)

tol = 1e-8;        % Toleransi numerik
max_iter = 200;    % Maksimum iterasi

%% =====================================================
% 2. DATA DEBIT KALIBRASI DAN PENGUJIAN
% ======================================================

Q_kalibrasi = [0.15 0.20 0.30 0.40 ...
               0.50 0.60 0.80 1.00];

Q_uji = [0.175 0.25 0.35 0.45 ...
         0.55 0.70 0.90];

%% =====================================================
% 3. PEMBENTUKAN PERSAMAAN MANNING
% ======================================================

% Luas penampang basah
A_fungsi = @(y) (b + m.*y).*y;

% Keliling basah
P_fungsi = @(y) b + 2.*y.*sqrt(1 + m^2);

% Jari-jari hidraulis
R_fungsi = @(y) A_fungsi(y)./P_fungsi(y);

% Persamaan debit Manning
Q_fungsi = @(y) (1/n).*A_fungsi(y).* ...
    R_fungsi(y).^(2/3).*sqrt(S);

% Persamaan nonlinear untuk mencari kedalaman
% f(y) = Q_manning(y) - Q_target = 0

%% =====================================================
% 4. PENYELESAIAN NUMERIK METODE BISECTION
% ======================================================

Q_semua = [Q_kalibrasi Q_uji];

hasil = zeros(length(Q_semua), 9);

for i = 1:length(Q_semua)

    Q_target = Q_semua(i);

    % Interval awal
    a = 0;
    c = H;

    % Iterasi Bisection
    for iter = 1:max_iter

        y = (a+c)/2;

        f_y = Q_fungsi(y)-Q_target;

        if abs(f_y) < tol
            break;
        end

        if f_y > 0
            c = y;
        else
            a = y;
        end

    end

    %% =================================================
    % 5. PERHITUNGAN PARAMETER HIDRAULIKA
    % ==================================================

    % Kedalaman normal
    y_normal = y;

    % Luas penampang basah
    A = A_fungsi(y_normal);

    % Keliling basah
    P = P_fungsi(y_normal);

    % Jari-jari hidraulis
    R = A/P;

    % Lebar permukaan air
    T = b+2*m*y_normal;

    % Kecepatan aliran
    V = Q_target/A;

    % Bilangan Froude
    Fr = V/sqrt(g*A/T);

    % Tinggi jagaan
    F = H-y_normal;

    % Menyimpan hasil
    hasil(i,:) = [Q_target y_normal A P R T V Fr F];

end

%% =====================================================
% 6. PEMISAHAN DATA KALIBRASI DAN PENGUJIAN
% ======================================================

hasil_kalibrasi = hasil(1:length(Q_kalibrasi),:);

hasil_uji = hasil(length(Q_kalibrasi)+1:end,:);

nama_kolom = {'Q','y','A','P','R','T','V','Fr','F'};

Tabel_kalibrasi = array2table(hasil_kalibrasi,...
    'VariableNames',nama_kolom);

Tabel_uji = array2table(hasil_uji,...
    'VariableNames',nama_kolom);

%% =====================================================
% 7. MENAMPILKAN HASIL PERHITUNGAN
% ======================================================

disp('======================================');
disp('HASIL PERHITUNGAN DATA KALIBRASI');
disp('======================================');

disp(Tabel_kalibrasi);

disp('======================================');
disp('HASIL PERHITUNGAN DATA PENGUJIAN');
disp('======================================');

disp(Tabel_uji);

%% =====================================================
% 8. PEMERIKSAAN KRITERIA KP-03
% ======================================================

V_maks = max(hasil(:,7));
Fr_maks = max(hasil(:,8));
y_maks = max(hasil(:,2));
F_min = min(hasil(:,9));

disp('======================================');
disp('PEMERIKSAAN KRITERIA KP-03');
disp('======================================');

fprintf('Kecepatan maksimum = %.4f m/s\n',V_maks);
fprintf('Froude maksimum = %.4f\n',Fr_maks);
fprintf('Kedalaman maksimum = %.4f m\n',y_maks);
fprintf('Tinggi jagaan minimum = %.4f m\n',F_min);

if V_maks <= 3
    disp('Kecepatan: MEMENUHI');
else
    disp('Kecepatan: TIDAK MEMENUHI');
end

if Fr_maks < 0.55
    disp('Froude: MEMENUHI');
else
    disp('Froude: TIDAK MEMENUHI');
end

if F_min >= 0.20
    disp('Tinggi jagaan: MEMENUHI');
else
    disp('Tinggi jagaan: TIDAK MEMENUHI');
end

%% =====================================================
% 9. GRAFIK HUBUNGAN DEBIT DAN KEDALAMAN
% ======================================================

figure;

plot(hasil_kalibrasi(:,1),...
     hasil_kalibrasi(:,2),...
     'bo-','LineWidth',1.5,...
     'MarkerFaceColor','b');

hold on;

plot(hasil_uji(:,1),...
     hasil_uji(:,2),...
     'rs','MarkerSize',8,...
     'MarkerFaceColor','r');

xlabel('Debit Q (m^3/s)');
ylabel('Kedalaman Normal y (m)');

title('Hubungan Debit dan Kedalaman Aliran');

legend('Data Kalibrasi',...
       'Data Pengujian',...
       'Location','northwest');

grid on;

%% =====================================================
% 10. GRAFIK HUBUNGAN DEBIT DAN KECEPATAN
% ======================================================

figure;

plot(hasil(:,1),hasil(:,7),...
    'k-o','LineWidth',1.5);

xlabel('Debit Q (m^3/s)');
ylabel('Kecepatan V (m/s)');

title('Hubungan Debit dan Kecepatan Aliran');

grid on;

%% =====================================================
% 11. GRAFIK HUBUNGAN DEBIT DAN BILANGAN FROUDE
% ======================================================

figure;

plot(hasil(:,1),hasil(:,8),...
    'm-o','LineWidth',1.5);

hold on;

yline(0.55,'r--','Batas KP-03');

xlabel('Debit Q (m^3/s)');
ylabel('Bilangan Froude');

title('Hubungan Debit dan Bilangan Froude');

grid on;

%% =====================================================
% 12. MENYIMPAN HASIL KE FILE EXCEL
% ======================================================

writetable(Tabel_kalibrasi,...
    'Hasil_Kalibrasi.xlsx');

writetable(Tabel_uji,...
    'Hasil_Pengujian.xlsx');

disp('======================================');
disp('PERHITUNGAN SELESAI');
disp('File Excel berhasil disiapkan.');
disp('======================================');
