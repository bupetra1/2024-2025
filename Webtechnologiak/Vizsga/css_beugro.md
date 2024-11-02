# CSS kiválasztók

**A CSS kiválasztók mintaillesztésre szolgálnak. Meghatározzák, hogy egy szabály mely elemekre vonatkozik.**
 
 Kisbetű-nagybetű éréketlenség az ASCII tartományban (ekvivalensek az [a-z] és [A-Z] karakterek) az olyan részek kivételével, melyek nem a CSS hatálya alá esnek (elemnevek, attribútumnevek és -értékek).

>**Egyszerű kiválasztó**
>
>Egyetlen típus kiválasztó, általános kiválasztó, attribútum kiválasztó, osztály kiválasztó, ID-kiválasztó vagy pszeudo-osztály.
>```css
>div - általános kiválasztó
>[rel=stylesheet] - attribútum kiválasztó
>.copyright - HTML osztály kiválasztó
>#logo - ID kiválasztó
>:lang(hu) - Pszeudo osztály kiválasztó
>```

>**Kombinátor**
>
>Egy CSS-kiválasztó több egyszerű kiválasztót is tartalmazhat. Az egyszerű kiválasztók közé kombinátort kell beépíteni.
>```cs
>whitespace - leszármazott kombinátor
>'>' - Gyermek kombinátor
>'+' - Szomszéd testvér kombinátor
>'~' - Általános kombinátor
>```

>**Egyszerű kiválasztók sorozata**
>
>Egymást követő egyszerű kiválasztók, melyek között nincsenek kombinátorok.
>Típus kiválasztóval vagy általános kiválasztóval kezdődnek és nem tartalmaznak további típus kiválasztókat vagy általános kiválasztókat.
>```css
>div
>h2#status
>link[rel=stylesheet][type=text/css]
>p.copyrigth
>*lang(hu) - *:univerzális kiválasztó
>tr:nth-child(odd)
>li:not(:last-child)
>```

>**Kiválasztó**
>
>Egyszerű kiválasztók sorozatainak olyan sorozata, melyeket kombinátorok választanak el. Legalább egy sorozat alkotja.
>Pszeudo-elem at utolsó egyszerű kiválasztó sorozat végéhez adható hozzá, de legfeljebb csak egy!
>```css
>p - 1 szekvencia bekezdés
>a img - olyan img elem ami leszármazottja a-nak
>h1 ~ table - ugyanahhoz a szülőhöz tartoznak
>div#main > h1 - h1 gyermeke a div#main-nek
>div > h1 + p
>q::before
>```
## Kombinátor
### Leszármazott kombinátor
**Egyszerű kiválasztók két sorozatát elválasztó whitespace.**

Ha P és Q egyszerű kiválasztók két sorozata, akkor a P Q kiválasztóra a Q-ra illeszkedő olyan elemek illeszkednek, *melyek a P-re illeszkedő elem leszármazottai*.

```css
thead th {
    background-color: darkgrey;
}
```
### Gyermek kombinátor
**Egyszerű kiválasztók két sorozatát elválasztó '>' karakter.**

Ha P és Q egyszerű kiválasztók két sorozata, akkor a P > Q kiválasztóra a Q-ra illeszkedő olyan elemek illeszkednek, *melyek a P-re illeszkedő elemek gyermekei.*
```css
nav > div {
    display: inline;
}
p > img:only-child {
    margin-left: 0;
}
```
### Szomszéd testvér kombinátor
**Egyszerű kiválasztók két sorozatát elválasztó '+' karakter.**

Ha P és Q egyszerű kiválasztók két sorozata, akkor a P + Q kiválasztóra a Q-ra illeszkedő olyan elemek illeszkednek, *melyek a P-re illeszkedő elemet követnek közvetlenül* a dokumentumban.
- Az illeszkedő elemeknek ugyanaz kell, hogy legyen a szülője.
- Közöttük megengedettek olyan konstrukciók, melyek nem elemek, például szöveg és megjegyzések, ezek figyelmen kívül hagyása.
```css
h1 + p {
    text-indent: 0;
}
```
### Általános testvér kombinátor (CSS3)
**Egyszerű kiválasztók két sorozatát elválasztó '-' karakter.**

Ha P és Q egyszerű kiválasztók két sorozata, akkor a P ~ Q kiválasztóra a Q-ra illeszkedő olyan elemek illeszkednek, *melyek a P-re illeszkedő elemet követnek (nem felétlenül) közvetlenül* a dokumentumban.
- Az illeszkedő elemeknek ugyanaz kell, hogy legyen a szülője.
```css
img ~ span {
    color: red;
}
```
## Kiválasztók típusai
### Típus kiválasztó
Egy CSS minősített név, a gyakorlatban tipikusan egy azonosító. A megfelelő nevű elemek illeszkednek rá.
```css
p {color: red } - A p elemek színe legyen piros
a { text-decoration: none} - Ha az elem link, akkor nem lesz aláhúzva
```
### Általános kiválasztó
Általános kiválasztónak nevezzük a * formájú kiválasztót.
Minden elem illeszkedik rá.
Elhagyható olyan egyszerű kiválasztóból, mely további komponenseket is tartalmaz.
>**Ekvivalens kiválasztók** 
>```css
>*#nav = #nav
>*.important = .important
>*[title] = [title]
>```

>**Nem ajánlott elhagyni, az olvashatóság végett** 
>```css
>div *:first-child = div :first-child
>div *: first-child != div:first-child
>```
### Attribútum kiválasztók
Az attribútum kiválasztókban érték azonosító vagy sztring. Tehát például a következők ekvivalensek:
```cs
[dir=rtl]
[dir='rtl']
[dir="rtl"]
```
**Fajtái**
>**[att]**: az att attribútummal rendelkező elemek illeszkednek rá

>**[att=érték]**: olyan elemek illeszkednek rá, melyek att attribútumának értéke pontosan érték
>```css
>style[type=italic] {
>    font-style: italic;
>}
>style[type=bold] {
>    font-weight: bold;
>}
>style[type=normal] {
>    font-style: normal;
>    font-weight: normal;
>}
>```

>**[att~=érték]**: olyan elemek illeszkednek rá, melyek att attribútumának értéke whitespace karakterekkel elválasztott olyan szavak egy listája, melyek mindegyik megegyezik érték-kel
>```css
>  a[title~="cica"] {
>    background-color : yellow;
>    }
>```

>**[att|=érték]**: olyan elemek illeszkednek rá, melyek att attribútumának értéke pontosan megegyezik érték-kel, vagy pedig az érték- karaktersorozattal kezdődik. Olyan attribútumokhoz használják, melyek értékeként nyelvváltozatok (pl. en-US, en-GB) jelenhetnek meg.
>
>Azonban az xml:lang attribútumhoz és a HTML lang attribútumához a :lang(C) pszeudo-osztályt kell használni.
>```css
>a[hreflang|=en]{
>    text-decoration: line-through;
>}
>```
**A CSS3 által bevezetett attribútum kiválasztók**
- [att^=érték]: olyan elemek illeszkednek rá, melyek att attribútumának értéke az érték előtaggal kezdődik
- [att$=érték]: olyan elemek illeszkednek rá, melyet att attribútumának értéke az érték utótaggal végződik
- [att*=érték]: olyan elemek illeszkednek rá, melyek att attribútumának értékében legalább egyszer előfordul érték.