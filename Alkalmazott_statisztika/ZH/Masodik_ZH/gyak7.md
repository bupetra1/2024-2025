# Első feladat
Az alábbi Matlab környezetben adott a UStemps adathalmaz, amely a következő változókat tartalmazza:
- **City**: A város neve és állama
- **JanTemp**: Januári középhőmérséklet F˚-ban
- **Lat**: szélességi fog (é-d)
- **Long**: hosszúsági fok (k-ny)

Első lépésként adjuk meg a januári középhőmérsékletet ˚C-ban, ha 32˚F = 0 ˚C és 212˚F = 100˚C.
**Számoljuk ki a szélességi fok felső-kvartilisét, majd ezek után dolgozzunk csak azokkal a városokkal, amelyek szélességi foka kisebb mint, az előbb kiszámított felső-kvartilis! Mi lesz ezen városok átlaghőmérsékletének az:**
- Átlaga
- Korrigált szórása
- Mi lesz azon városok aránya, ahol a középhőmérséklet fagyáspont (0°C) alatt van? 
- Melyik városban volt a legmelegebb?
## Feladat megoldás lépései
### UStemps beolvasása
```Matlab
load UStemps.mat
ustemp = readtable('UStemps.txt')
ustemp.City
```
### °F -> °C
```Matlab
homerseklet_celsiusban = (ustemp.JanTemp - 32)/1.8
ustemp.Celsius = homerseklet_celsiusban
```
### Szélességi fog felső-kvartilise:
```Matlab
felso_kvartilis=quantile(ustemp.Lat,.75)
```
### Azon városok listája, amiknek a szélességi foka kisebb, mint a felső kvartilis:
```Matlab
varosok_nevei = ustemp.City(ustemp.Lat<felso_kvartilis)
```
### Városok összes adatának mentése
```Matlab
ujadatbazis = ustemp(ustemp.Lat<felso_kvartilis,:)
```
### Mi az átlaghőmérsékletek átlaga?
```Matlab
atlag=mean(ujadatbazis.Celsius)
```
### Mi a korrigált szórása az átlaghőmérsékleteknek?
```Matlab
szoras=std(ujadatbazis.Celsius)
```
### Melyik városban volt a legmelegebb?
```Matlab
maximum_homerseklet = max(ujadatbazis.Celsius);
keresett_varos = find(ujadatbazis.Celsius == maximum_homerseklet)
ujadatbazis(keresett_varos, 'City')
```
### Azon városok aránya, ahol a középhőmérséklet fagyáspont alatt van:
```Matlab
osszes_varos=height(ujadatbazis)
nulla_fok_alatt=sum(ujadatbazis.Celsius<0)
fagyaspont_alatti_varosok_aranya = nulla_fok_alatt/osszes_varos
```
## Feladat megoldása a tesztben:
```Matlab
%Átváltás °F-ból °C-be
homerseklet_celsiusban = (JanTemp - 32)/1.8;
Celsius = homerseklet_celsiusban;
%Felső kvantilis kiszámítása
felso_kvantilis=quantile(Lat,.75);
%Feltételnek megfelelő adatok kimentése
varosok_nevei = City(Lat<felso_kvantilis);
ujadatbazis = Celsius(Lat<felso_kvantilis);
ujvarosok = City(Lat<felso_kvantilis);
%Átlag
atlag=mean(ujadatbazis);
%Korrigált szórás
szoras = std(ujadatbazis);
%Városok aránya
osszes_varos=length(ujadatbazis);
nulla_fok_alatt=sum(ujadatbazis<0);
fagyaspont_alatti_varosok_aranya = nulla_fok_alatt/osszes_varos;
%Legmelegebb város kiválasztása
maximum_homerseklet = max(ujadatbazis);
keresett_varos = find(ujadatbazis == maximum_homerseklet);
ujvarosok(keresett_varos);
```
# Második feladat
Készítsen egy Matlab függvényt, amely egy n-elemű x mintavektor és t valós szám esetén visszaadja az alábbi képlet alapján definiált **empirikus eloszlásfüggvény** értékét a t helyen:
$$
F^*(t) =
\begin{cases} 
0, & \text{ha } t \leq x_1^*, \\
\frac{k}{n}, & \text{ha } x_k^* < t \leq x_{k+1}^*, \\
1, & \text{ha } x_n^* < t.
\end{cases}
$$

A függvény neve legyen fun, a kimenőváltozó legyen F.
```Matlab
function F = fun(x,t)
    x_rendezett = sort(x);% Az x vektor elemeit sorba rendezzük
    n = length(x); % Ezután meghatározzuk a vektor hosszát
%A képlet alapján felírjuk a feltételeinket
    if t <= x_rendezett(1)%Azért kell ide az 1-es, mert az 1. index van a képletben
        F = 0; % Ha t kisebb vagy egyenlő a legkisebb mintaelemmel
    elseif t > x_rendezett(end)% end -> utolsó elem
        F = 1; % Ha t nagyobb a legnagyobb mintaelemnél
    else
        k = find(x_rendezett < t, 1, 'last');%Megnézzük, hogy a t nagyobb-e mint a vektor legnagyobb eleme, ha igen akkor a visszatérési értéket növeljük egyel
        F = k / n; %k
    end
end
```
# Harmadik feladat 
Készítsen egy Matlab függvényt, amely egy n-elemű x mintavektor és q (0 < q < 1) szám esetén visszaadja az alábbi képlet alapján definiált **q-kvantilist**:
\[ h = nq + \frac{1}{2} \]

\[
Q(q) = x_{[h]}^* + (h - \lfloor h \rfloor)(x_{[h]+1}^* - x_{[h]}^*)
\]
ahol [.] az alsó-egészrész függvény, x* a rendezett minta eleme.
A függvény neve legyen **fun**, a kimenőváltozó legyen Q.
Egy adott vektor a sort(.) paranccsal rendezhető növekvő sorrendbe.
## Feladat megoldása
```Matlab
function Q = fun(x,q)
    x_rendezett = sort(x);
    n = length(x);
    %Kvantilis kiszámítása
    h = n * q + 0.5;
    h_floor = floor(h); % Alsó-egészrész függvény

    % Kvantilis érték számítása
    if h_floor >= n % Ha h a legnagyobb elemnél van
        Q = x_rendezett(end);
    else
        Q = x_rendezett(h_floor) + (h - h_floor) * (x_rendezett(h_floor + 1) - x_rendezett(h_floor));
    end
end
```
# Negyedik feladat
Készítsen egy Matlab függvényt, amely egy n-elemű x mintavektor esetén visszaadja az alábbi képlet alapján definiált **korrigált empirikus szórásnégyzetet**:
\[
s^{*2} = \frac{1}{n-1} \sum_{i=1}^{n} (x_i - \bar{x})^2
\]

A függvény neve legyen fun, a kimenőváltozó legyen s.
Az s meghatározásához használjon vektorműveleteket!
A var, std, for, while, stb. parancsok tiltottak!
## Feladat megoldása
```Matlab
function s = fun(x)
    n = length(x);          % Minta elemszáma
    x_mean = sum(x) / n;    % Mintaátlag
    kulonbseg = x - x_mean; % Eltérések a mintátlagtól
    s = sum(kulonbseg .^ 2) / (n - 1); % Korrigált szórásnégyzet
end
```

