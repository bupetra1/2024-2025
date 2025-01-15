
### 1. **CSS Kiválasztók Alapjai**
- **Definíció:** A kiválasztók meghatározzák, hogy mely HTML elemekre vonatkoznak a stílusok.
- **Kisbetű-nagybetű érzékenység:** Az ASCII tartományban az elemnevek, attribútumnevek és -értékek kivételével kis- és nagybetűk egyenértékűek.

---

### 2. **Egyszerű Kiválasztók**
#### a. **Típus Kiválasztó**
- Az elem neve alapján választja ki az elemeket.  
  **Példa:**  
  ```css
  p { color: red; }
  ```
  Minden `<p>` elem szövege piros lesz.

#### b. **Osztály Kiválasztó**
- Az osztály neve alapján választja ki az elemeket.  
  **Példa:**  
  ```css
  .highlight { background-color: yellow; }
  ```
  Az összes `.highlight` osztályú elem háttérszíne sárga lesz.

#### c. **ID Kiválasztó**
- Az elem azonosítóját (`id`) használja a stílus megadására.  
  **Példa:**  
  ```css
  #header { font-size: 24px; }
  ```
  A `header` azonosítójú elem betűmérete 24 pixel lesz.

#### d. **Attribútum Kiválasztó**
- Az elemek attribútumai alapján választja ki az elemeket.  
  **Típusok:**
  - `[attr]`: Minden elem, amely rendelkezik az adott attribútummal.  
    **Példa:**  
    ```css
    [title] { color: blue; }
    ```
  - `[attr=value]`: Az elemek, amelyek attribútumának értéke pontosan megegyezik.  
    **Példa:**  
    ```css
    [type="button"] { background-color: green; }
    ```

#### e. **Pszeudo-osztályok**
- Az elemek állapota vagy speciális tulajdonságai alapján választja ki őket.  
  **Példa:**  
  ```css
  a:hover { text-decoration: underline; }
  ```
  Az `a` elem alá lesz húzva, amikor az egér fölé kerül.

---

### 3. **Kombinátorok**
- **Leszármazott Kombinátor (`whitespace`)**  
  Csak azokat az elemeket választja ki, amelyek más elemek leszármazottai.  
  **Példa:**  
  ```css
  div p { color: red; }
  ```
  A `<div>`-eken belüli `<p>` elemek szövege piros lesz.

- **Gyermek Kombinátor (`>`)**  
  Csak a közvetlen gyermekeket választja ki.  
  **Példa:**  
  ```css
  ul > li { font-weight: bold; }
  ```
  Az `<ul>` közvetlen gyermekeiként szereplő `<li>` elemek félkövérek lesznek.

- **Szomszéd Testvér Kombinátor (`+`)**  
  Azokat az elemeket választja ki, amelyek közvetlenül egy másik elem után következnek.  
  **Példa:**  
  ```css
  h1 + p { margin-top: 0; }
  ```
  Az első `<p>` elem, amely egy `<h1>` után következik, nem kap margót felül.

- **Általános Testvér Kombinátor (`~`)**  
  Minden testvér elemet kiválaszt, amely az adott elem után található, de nem közvetlen következőként.  
  **Példa:**  
  ```css
  h1 ~ p { color: grey; }
  ```

---

### 4. **Pszeudo-osztályok Részletesen**
#### a. **Dinamikus Pszeudo-osztályok**
- `:hover`: Amikor az egér az elem fölött van.  
  **Példa:**  
  ```css
  button:hover { background-color: lightblue; }
  ```

- `:focus`: Az aktuálisan fókuszban lévő elem.  
  **Példa:**  
  ```css
  input:focus { border-color: blue; }
  ```

- `:active`: Amikor az elem éppen aktiválva van (pl. kattintás közben).  
  **Példa:**  
  ```css
  a:active { color: red; }
  ```

#### b. **Szerkezeti Pszeudo-osztályok**
- `:first-child`: Az első gyermeke egy szülőelemnek.  
  **Példa:**  
  ```css
  p:first-child { font-weight: bold; }
  ```

- `:nth-child(n)`: Az adott sorszámú gyermek.  
  **Példa:**  
  ```css
  li:nth-child(2) { color: green; }
  ```

- `:empty`: Az üres elemek.  
  **Példa:**  
  ```css
  div:empty { display: none; }
  ```

---

### 5. **Pszeudo-elemek**
- **Definíció:** Olyan dokumentumrészek formázására használhatók, amelyek más módon nem érhetők el.  
- **Példák:**
  - `::first-line`: Egy elem első sora.  
    ```css
    p::first-line { font-style: italic; }
    ```

  - `::first-letter`: Egy elem első karaktere.  
    ```css
    p::first-letter { font-size: 2em; }
    ```

  - `::before` és `::after`: Generált tartalom hozzáadása.  
    ```css
    div::before { content: "Start: "; }
    div::after { content: " End."; }
    ```

---

### 6. **Specifikusság és Prioritás**
- Azonos stílusok esetén a specifikusság határozza meg, hogy melyik stílus érvényesül.
  - Inline stílusok: a legspecifikusabbak.
  - ID kiválasztók: nagyobb prioritás, mint az osztályok vagy típusok.
  - Osztályok, attribútumok, pszeudo-osztályok: kisebb prioritással bírnak.
  - Típus kiválasztók és pszeudo-elemek: a legkisebb prioritás.

---
