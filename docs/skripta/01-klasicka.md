# 1. Klasická kryptografie

!!! abstract "Cíle kapitoly"
    - Pochopit princip substituce a transpozice
    - Umět zašifrovat/dešifrovat všechny klasické šifry
    - Znát útoky a slabiny každé šifry
    - Rozumět pojmu **klíčový prostor** a frekvenční analýze

Klasická kryptografie operuje nad přirozeným jazykem (abeceda A–Z = čísla 0–25). Bezpečnost závisí na tajnosti algoritmu nebo klíče, nikoli na matematicky tvrdém problému.

---

## 1.1 Caesarova šifra

### Definice

!!! info "Formule"
    **Šifrování:** $c = (p + k) \bmod 26$

    **Dešifrování:** $p = (c - k) \bmod 26$

    $p$ = číselná hodnota plaintext písmene (A=0, B=1, …, Z=25), $k$ = klíč (posun).

### Příklad — $k = 3$

Každé písmeno posuneme o 3 dopředu v abecedě (K→N, R→U, …):

| Plaintext  | K  | R  | Y  | P  | T  | O  |
|------------|----|----|----|----|----|----|
| Hodnota    | 10 | 17 | 24 | 15 | 19 | 14 |
| +3 mod 26  | 13 | 20 | 1  | 18 | 22 | 17 |
| Ciphertext | **N** | **U** | **B** | **S** | **W** | **R** |

```mermaid
flowchart LR
    A["Plaintext: KRYPTO"] --> B["Klíč k=3\n(posun +3)"]
    B --> C["mod 26 pro každý znak"]
    C --> D["Ciphertext: NUBSWR"]
    style A fill:#1e3a2f,stroke:#34d399,color:#e2e8f0
    style D fill:#3d1515,stroke:#f87171,color:#e2e8f0
```

### Analýza bezpečnosti

!!! danger "Bezpečnost: Triviálně slabá"
    - **Klíčový prostor:** pouze **25 klíčů** → hrubá síla v sekundách
    - **Frekvenční analýza:** nejčastější písmeno v angličtině je E → hledáme, čemu odpovídá
    - Klíč lze určit z jediného zachyceného znaku

!!! tip "Zkouška"
    Umět ručně zašifrovat/dešifrovat slovo. Znat velikost klíčového prostoru (25). Vědět, proč je to nezabezpečené.

---

## 1.2 Afinní šifra

### Definice

!!! info "Formule"
    **Šifrování:** $c = (a \cdot p + b) \bmod 26$

    **Dešifrování:** $p = a^{-1} \cdot (c - b) \bmod 26$

    Klíč = dvojice $(a, b)$. Podmínka: $\gcd(a, 26) = 1$.

### Podmínka klíče — proč $\gcd(a, 26) = 1$?

Pokud $\gcd(a, 26) \neq 1$, mapování není bijekce — více písmen se zobrazí na stejný znak, dešifrování je nejednoznačné.

**Povolené hodnoty $a$:** {1, 3, 5, 7, 9, 11, 15, 17, 19, 21, 23, 25} → **12 hodnot**

**Velikost klíčového prostoru:** $12 \times 26 = \mathbf{312}$ klíčů

### Příklad — $a = 5$, $b = 8$, šifrování 'A'

$$c = (5 \cdot 0 + 8) \bmod 26 = 8 \Rightarrow \text{'I'}$$

### Výpočet inverzního prvku $a^{-1}$

Hledáme $x$ tak, aby $a \cdot x \equiv 1 \pmod{26}$ — rozšířený Euklidův algoritmus.

!!! example "Příklad: $5^{-1} \bmod 26$"
    Hledáme $x$: $5x \equiv 1 \pmod{26}$
    
    Zkusíme: $5 \times 21 = 105 = 4 \times 26 + 1$ → zbytek 1 ✓
    
    $5^{-1} \bmod 26 = \mathbf{21}$

!!! question "Typická zkouška"
    „Zašifrujte slovo XYZ afinní šifrou s klíčem $(a, b)$. Jak dešifrovat?"
    
    Postup: převést na čísla → aplikovat formuli → převést zpět. Nezapomeňte na podmínku $\gcd(a,26)=1$.

---

## 1.3 Hillova šifra

### Definice

!!! info "Formule (pro blok délky $n$)"
    **Šifrování:** $\vec{c} = K \cdot \vec{p} \pmod{26}$

    **Dešifrování:** $\vec{p} = K^{-1} \cdot \vec{c} \pmod{26}$

    $K$ = čtvercová klíčová matice $n \times n$, $\vec{p}$ = vektor $n$ plaintext písmen.

### Podmínka invertibility

Matice $K$ musí být invertibilní mod 26: $\gcd(\det(K), 26) = 1$.

### Příklad — bigramy ($n=2$), klíč $K = \begin{pmatrix}3 & 3 \\ 2 & 5\end{pmatrix}$, plaintext "HE"

**Krok 1 — Převod na vektory:**
$$\vec{p} = \begin{pmatrix}H \\ E\end{pmatrix} = \begin{pmatrix}7 \\ 4\end{pmatrix}$$

**Krok 2 — Maticové násobení:**
$$K \cdot \vec{p} = \begin{pmatrix}3 & 3 \\ 2 & 5\end{pmatrix} \begin{pmatrix}7 \\ 4\end{pmatrix} = \begin{pmatrix}3\cdot7 + 3\cdot4 \\ 2\cdot7 + 5\cdot4\end{pmatrix} = \begin{pmatrix}33 \\ 34\end{pmatrix}$$

**Krok 3 — Redukce mod 26:**
$$\begin{pmatrix}33 \\ 34\end{pmatrix} \bmod 26 = \begin{pmatrix}7 \\ 8\end{pmatrix} \Rightarrow \begin{pmatrix}H \\ I\end{pmatrix}$$

Ciphertext: **"HI"**

### Inverze matice mod 26

$$K^{-1} = \det(K)^{-1} \cdot \text{adj}(K) \pmod{26}$$

Pro $K = \begin{pmatrix}3 & 3 \\ 2 & 5\end{pmatrix}$:

- $\det(K) = 3 \cdot 5 - 3 \cdot 2 = 9$
- $9^{-1} \bmod 26 = 3$ (protože $9 \cdot 3 = 27 \equiv 1$)
- $\text{adj}(K) = \begin{pmatrix}5 & -3 \\ -2 & 3\end{pmatrix} \equiv \begin{pmatrix}5 & 23 \\ 24 & 3\end{pmatrix} \pmod{26}$

!!! tip "Zkouška"
    Hillova šifra bývá na zkoušce jako výpočetní příklad. Procvičte maticové násobení mod 26 a výpočet inverze.

---

## 1.4 Vigenèrova šifra

### Definice

!!! info "Formule"
    $$c_i = (p_i + k_{i \bmod V}) \bmod 26$$

    Klíčové slovo délky $V$ se **cyklicky opakuje** přes celý plaintext.

### Příklad — klíč "KEY", plaintext "KRYPTOGR"

| Pozice | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 |
|--------|---|---|---|---|---|---|---|---|
| Plaintext | K(10) | R(17) | Y(24) | P(15) | T(19) | O(14) | G(6) | R(17) |
| Klíč (KEY↺) | K(10) | E(4) | Y(24) | K(10) | E(4) | Y(24) | K(10) | E(4) |
| Součet mod 26 | 20 | 21 | 22 | 25 | 23 | 12 | 16 | 21 |
| Ciphertext | **U** | **V** | **W** | **Z** | **X** | **M** | **Q** | **V** |

### Vlastnosti a bezpečnost

- **Klíčový prostor:** $26^V$ možností — výrazně větší než Caesar
- **Vzdálenost jednoznačnosti:** $\delta_U = \frac{H(K)}{D}$, kde $D = 3.2$ b/znak (angličtina) → pro $V=4$: $\delta_U = \frac{4 \cdot \log_2 26}{3.2} \approx 5.9$ znaků

### Útok: Kasiskiho test

Pokud se v ciphertextu opakuje stejný vzor, jeho vzdálenost je pravděpodobně násobkem $V$.

!!! example "Kasiskiho test"
    Ciphertext: `...THE...abc...THE...abc...`
    
    Vzdálenost mezi `THE` a druhým `THE` = 12
    
    $\text{gcd}(12, ...) \Rightarrow V | 12 \Rightarrow V \in \{1, 2, 3, 4, 6, 12\}$
    
    Pak pro každou pozici mod $V$ zvlášť → Caesarova šifra → frekvenční analýza.

### Útok: Index koincidence (Friedman)

$$IC = \frac{\sum_{i=0}^{25} n_i(n_i - 1)}{N(N-1)}$$

- Angličtina: $IC \approx 0.065$
- Náhodný text: $IC \approx 0.038$
- Vigenèrův šifrový text: $IC \approx 0.038$ + korekce závisí na $V$

$$V \approx \frac{0.065 - 0.038}{IC - 0.038}$$

!!! tip "Zkouška"
    Znát obě metody útoku, umět odvodit délku klíče. Znát vzorec pro vzdálenost jednoznačnosti.

---

## 1.5 Sloupcová transpozice

### Princip

Transpozice **nemění** znaky (žádná konfúze), pouze **mění jejich pořadí** (difúze). Frekvenční vzory jsou zachovány.

### Příklad — klíč "3 1 4 2"

```
Plaintext:   K R Y P T O G R A F I E

Seřadíme do mřížky (4 sloupce):
Číslo sl.:   3   1   4   2
Sloupce:     K   R   Y   P
             T   O   G   R
             A   F   I   E

Bereme sloupce v pořadí 1,2,3,4:
  Sloupec 1: R O F
  Sloupec 2: P R E
  Sloupec 3: K T A
  Sloupec 4: Y G I

Ciphertext: ROF PRE KTA YGI → ROFPREKTA YGI
```

### Dvojitá transpozice

Aplikujeme transpozici dvakrát (s různými nebo stejnými klíči) → výrazně vyšší bezpečnost.

!!! tip "Zkouška"
    Umět provést transpozici ručně. Vědět, že transpozice = difúze bez konfúze.

---

## Shrnutí kapitoly

!!! abstract "Rychlý přehled"

    | Šifra | Klíč | Klíčový prostor | Útok |
    |-------|------|----------------|------|
    | Caesar | $k$ | 25 | Hrubá síla, frekv. analýza |
    | Afinní | $(a,b)$ | 312 | Hrubá síla |
    | Hill | matice $K$ | velký | Known-plaintext |
    | Vigenère | slovo délky $V$ | $26^V$ | Kasiski, Friedman + frekv. |
    | Transpozice | permutace | $n!$ | Frekv. analýza (vzory zachovány) |

!!! question "Klíčové otázky ke zkoušce"
    1. Zašifrujte „HELLO" Caesarovou šifrou s $k=13$ (ROT13).
    2. Proč musí být $\gcd(a, 26) = 1$ u afinní šifry?
    3. Jak Kasiskiho test odhalí délku klíče Vigenèrovy šifry?
    4. Jaký je rozdíl mezi konfúzí a difúzí? Která platí pro transpozici?
