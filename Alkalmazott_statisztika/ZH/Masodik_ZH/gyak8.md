# Első feladat
Egy teherautó rakománnyi 550 milliliteres üdítőitalból 10 palackot véletlenszerűen kiválasztva és lemérve azok űrtartalmát az alábbi, milliliterben kifejezett értékeket kaptuk:
$$543, 553, 552, 536, 552, 558, 538, 530, 545, 557.$$
Ismert, hogy a palackokba töltött üdítőital mennyisége **normális eloszlású 10 ml szórással. 91%-os döntési szintet** használva vizsgálja meg a gyártó azon állítását, hogy a palackokba átlagosan 550 milliliter üdítőitalt töltöttek!
1. 
H0: m=
H1: m≠
2. Próbastatisztika értéke:
3. Elfogadási tartomány határai (kritikus értékek):
4. Döntés ( 0, ha elfogadjuk   ~   1, ha elvetjük)
```Matlab
data = [543, 553, 552, 536, 552, 558, 538, 530, 545, 557];
%H0 = 550;
%H1 = m != 550;
[~, ~, ~, z] = ztest(data, 550, 10)
alpha = 0.09;
cval=norminv(1-alpha/2);
[-cval cval]
```
# Második feladat
Egy gabonaraktárban 50 kg-os kiszerelésben búzát csomagolnak. A havi minőségellenőrzés során azt is meg akarták vizsgálni, hogy a raktárból kikerülő zsákokban tényleg 50kg búza van-e, ezért lemértek nyolc darab véletlenül kiválasztott zsákot. Eredményül a következőket kapták:
$$49.8, 50, 49.5, 50.3, 48.2, 49.3, 52.9, 53.9.$$
Hipotéziseit és az adatokra vonatkozó feltételeit pontosan megfogalmazva döntsön 96%-os szinten, a zsákok átlagos töltőtömege tényleg 50 kg-e!
1. 
H0: m=
H1: m≠
1. Próbastatisztika értéke:
2. Elfogadási tartomány határai (kritikus értékek):
3. Döntés ( 0, ha elfogadjuk   ~   1, ha elvetjük)
## Hipotézisek
```Matlab
H0: m=50;
H1: m≠50;
```
## Próbastatisztika, kritikusértékek
```Matlab
data = [49.8, 50, 49.5, 50.3, 48.2, 49.3, 52.9, 53.9];
[~, ~, ~, z] = ttest(data, 50) %Próbastatisztika
alpha = 0.04 %1-0.96
cval=tinv(1-alpha/2, 7); %8-1
ET = [-cval cval] %Kritikus értékek
```
# Harmadik feladat
Készítsen egy Matlab függvényt, amely egy n-elemű x mintavektor, m0 várható érték, sigma szórás és alpha szignifikancia szint esetén visszaadja a 2-oldai z-próba teszt-statisztikáját (z) és az elfogadási tartományát (ET):
$$
z = \frac{\bar{x} - m_0}{\sigma} \sqrt{n}, \\
ET = \left[ -z_{1-\frac{\alpha}{2}}, z_{1-\frac{\alpha}{2}} \right],
$$
ahol z∗ a standard normális kvantilis-függvénye (norminv(*)).
A változók definiálásánál használjon pontosvesszőt!
```Matlab
function [z ET] = z_test(x,m0,sigma,alpha)
    % n: mintavektor elemszáma
    n = length(x);
    
    % x_átlag: mintavektor átlaga
    x_mean = mean(x);

    % z-próba teszt-statisztika
    z = (x_mean - m0) / (sigma / sqrt(n));

    % Z-kvantilis meghatározása
    z_star = norminv(1 - alpha / 2);

    % Elfogadási tartomány (ET)
    ET = [-z_star, z_star];
end
```
Barta megoldása
```Matlab
function [z ET] = z_test(x,m0,sigma,alpha)
    z = (mean(x)-m0) / sigma * sqrt(length(x));
    ET = [-norminv(1-alpha/2) norminv(1-alpha/2)];
end
```