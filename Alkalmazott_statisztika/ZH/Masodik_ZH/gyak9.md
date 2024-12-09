# Első feladat
Állapítsuk meg 90% döntési szint mellett, hogy egy dobókocka szabályos-e. Jelölje A~i~ azt az eseményt, hogy a kockán i-t dobunk. Ekkor 
$$P(A_i)=\frac{1}{6}, i=1,...,6.$$

A kocka 900-szori feldobásakor az alábbi eredmény adódott:
$$
k_1=148, k_2=173, k_3=139, k_4=170, k_5=162, k_6=108
$$
(k~i~    jelöli A~i~ gyakoriságát).
1. Hipotézisek
H0: A kocka szabályos.
H1: Nem szabályos.
2. Próbastatisztika értéke
3. Kritikus értékek
4. Döntés (0, ha elfogadjuk   ~    1, ha elvetjük)
## Feladat megoldása
```Matlab
function [chi2, decision] = khi_negyzet(k, n, alpha)
    % Várható gyakoriságok
    E = n / length(k)
    
    % Khi-négyzet statisztika kiszámítása
    chi2 = sum((k - E).^2 / E);
    
    % Kritikus érték meghatározása
    df = length(k) - 1;
    chi2_crit = chi2inv(1 - alpha, df)
    
    % Döntés
    decision = chi2 > chi2_crit
end
% Adatok
k = [148, 173, 139, 170, 162, 108];
n = 900;
alpha = 0.10;

% Futtatás
[chi2, decision] = khi_negyzet(k, n, alpha);
```
# Második feladat
Vizsgáljuk meg 97% döntési szint mellett, hogy a szemszín és a hajszín függetlenek-e egymástól!
200 embert megfigyelve az alábbi megfigyelések adódtak:

| | Szőke haj | Barna haj | Fekete haj |
| ----------- | ----------- | ----------- |----------- | 
|Kék szem|29|23|2|
|Barna szem|8|72|20|
|Zöld szem|19|22|5|
1. H0: A hajszín és a szemszín függetlenek.
H1: Nem függetlenek
2. Próbastatisztika értéke:
3. Kritikus érték:
4. Döntés (0, ha elfogadjuk   ~    1, ha elvetjük) 
## Feladat megoldása
```Matlab
% Adatok
megfigyelt = [29, 23, 2;   % Kék szem
              8,  72, 20;  % Barna szem
              19, 22, 5];  % Zöld szem

% Margóösszegek
sor_osszeg = sum(megfigyelt, 2);    % Sorösszegek
oszlop_osszeg = sum(megfigyelt, 1); % Oszlopösszegek
ossz_osszeg = sum(megfigyelt(:));   % Teljes elemszám

% Elvárt értékek
elvart = (sor_osszeg * oszlop_osszeg) / ossz_osszeg;

% Khi-négyzet próbastatisztika
chi2_stat = sum((megfigyelt(:) - elvart(:)).^2 ./ elvart(:));

% Szignifikanciaszint és szabadságfok
alpha = 0.03; % 97%-os döntési szint
df = (size(megfigyelt, 1) - 1) * (size(megfigyelt, 2) - 1);

% Kritikus érték
kritikus_ertek = chi2inv(1 - alpha, df);

% Döntés
if chi2_stat <= kritikus_ertek
    dontes = 0; % Elfogadjuk H0-t
else
    dontes = 1; % Elvetjük H0-t
end

% Eredmények kiíratása
disp(['Próbastatisztika: ', num2str(chi2_stat)]);
disp(['Kritikus érték: ', num2str(kritikus_ertek)]);
disp(['Döntés (0: elfogadjuk, 1: elvetjük): ', num2str(dontes)]);

```