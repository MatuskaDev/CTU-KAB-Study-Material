# 9. Generování klíčů

!!! abstract "Cíle kapitoly"
    - Pochopit Čínskou větu o zbytcích a umět ji aplikovat
    - Znát kvadratická residua, Legendreův a Jacobiho symbol, Eulerovo kritérium
    - Znát generátory (primitivní kořeny) a jak je hledat
    - Rozumět algoritmům faktorizace čísel
    - Projít Solovay-Strassenův, Lehmannův a Rabin-Millerův test prvočíselnosti
    - Znát rady pro praktické generování prvočísel a silná prvočísla
    - Rozlišit PRNG od TRNG; znát LCG, BBS a Von Neumannův dekorelátor
    - Znát statistické testy náhodnosti

---

## 9.1 Čínská věta o zbytcích (CRT)

!!! info "Věta 30 — Čínská věta o zbytcích"
    Nechť $m_1, m_2, \ldots, m_r$ jsou vzájemně nesoudělná kladná celá čísla. Potom soustava kongruencí
    
    $$x \equiv a_1 \pmod{m_1}, \quad x \equiv a_2 \pmod{m_2}, \quad \ldots, \quad x \equiv a_r \pmod{m_r}$$
    
    má **jediné řešení** modulo $M = m_1 \cdot m_2 \cdots m_r$.

Řešení: Nechť $M_i = M / m_i$. Pak $x = \left|\ \sum_{i=1}^r |x|_{m_i} M_i y_i\ \right|_M$, kde $y_i$ jsou řešení kongruencí $M_i y_i \equiv 1 \pmod{m_i}$.

!!! example "Příklad"
    Mějme zbytky čísla $x$: $|x|_3 = 1$, $|x|_5 = 2$, $|x|_7 = 3$ → $M = 3 \cdot 5 \cdot 7 = 105$.
    
    Nechť $M_3 = 7 \cdot 5 = 35$, $M_5 = 3 \cdot 7 = 21$, $M_7 = 3 \cdot 5 = 15$, kde $35y_3 \equiv 1 \pmod{3}$, $21y_5 \equiv 1 \pmod{5}$ a $15y_7 \equiv 1 \pmod 7$.
    
    Řešením těchto kongruencí dostáváme pro $y_3 = 2$, $y_5 = 1$ a $y_7 = 1$ a tedy pro $x$ platí:
    
    $$x = \left|\ |x|_3 M_3 y_3 + |x|_5 M_5 y_5 + |x|_7 M_7 y_7\ \right|_M = |1 \cdot 35 \cdot 2 + 2 \cdot 21 \cdot 1 + 3 \cdot 15 \cdot 1|_{105} = |157|_{105} = 52$$

**Využití v kryptografii:** RSA-CRT (rychlé dešifrování), exponencování, výpočet kořenů polynomů nad složenými moduly.

---

## 9.2 Kvadratická residua

### Definice

!!! info "Definice — Kvadratické residuum"
    Pokud $m$ je kladné celé číslo, pak celé číslo $a$ je **kvadratické residuum** modulo $m$, když $\gcd(a, m) = 1$ a kongruence $x^2 \equiv a \pmod{m}$ má nějaké řešení.
    
    Když tato kongruence nemá žádné řešení → $a$ je **kvadratické nonresiduum** modulo $m$.

!!! info "Věta 31 — Kvadratické residuum modulo prvočíslo"
    Nechť $p$ je liché prvočíslo a $a$ je celé číslo nedělitelné $p$. Potom kongruence $x^2 \equiv a \pmod{m}$ má buď **přesně 2 vzájemně nekongruentní řešení** modulo $p$ nebo **nemá žádné řešení**.

!!! example "Příklad pro $p = 7$"

    $$|1^2|_7 = |1|_7, \quad |2^2|_7 = |4|_7, \quad |3^2|_7 = |2|_7$$

    $$|4^2|_7 = |2|_7, \quad |5^2|_7 = |4|_7, \quad |6^2|_7 = |1|_7$$
    
    Každé kvadratické residuum se vyskytuje **2×**. Kvadratická residua mod 7: {1, 2, 4}. Kvadratická nonresiduua mod 7: {3, 5, 6}.

### Vlastnosti

- Pro liché prvočíslo $p$ existuje $\frac{p-1}{2}$ kvadratických residuí modulo $p$ a stejný počet kvadratických nonresiduí modulo $p$.
- Když $a$ je kvadratickým residuem modulo prvočíslo $p$ → existují přesně **2 kořeny odmocniny** výrazu $|x^2|_p$ a to:
    1. číslo $a$ v intervalu $(0, \frac{p-2}{2})$ a
    2. číslo $|-a|_p$ v intervalu $(\frac{p-2}{2}, p-1)$.
- V případě $n$, které je součinem 2 lichých prvočísel $p$ a $q$, bude počet kvadratických residuí mod $n$ roven $\frac{(p-1)(q-1)}{4}$.
- V tomto případě vytváří 4 kvadratická residua tzv. **úplnou odmocninu modulo $n$** (perfect square mod $n$).
- Aby kvadratické residuum bylo „odmocnina modulo $n$", musí být odmocninou také kvadratické residua modulo $p$ a modulo $q$.

!!! info "Věta 32 — Kvadratické residuum složeného modulu"
    Nechť $n = p_1^{\alpha_1} \cdot p_2^{\alpha_2} \cdots p_k^{\alpha_k}$, je kanonický rozklad $n$, kde $2 < p_1 < p_2 < \cdots < p_k$ jsou prvočísla a $\alpha_1, \ldots, \alpha_k$ jsou přirozená čísla. Potom $a$ je kvadratickým residuem modulo $n \Leftrightarrow a$ je kvadratické residuum modulo $p_1^{\alpha_1}, p_2^{\alpha_2}, \ldots, p_k^{\alpha_k}$ (platí z čínské věty o zbytcích).

!!! example "Příklad: $x^2 \equiv a \pmod{15}$, kde $15 = 5 \cdot 3$"
    
    | $\lvert x^2\rvert_{15}$ | $\lvert x^2\rvert_5$ | $\lvert x^2\rvert_3$ | kořeny |
    |---|---|---|---|
    | $\lvert 1^2\rvert_{15}=1$ | $\lvert 1\rvert_5$ → 1. kořen | $\lvert 1^2\rvert_3=\lvert 1\rvert_3$ → 1. kořen | $\gcd(1,15)=1$ → QR |
    | $\lvert 4^2\rvert_{15}=1$ | $\lvert 1\rvert_5$ → 1. kořen | $\lvert 4^2\rvert_3=\lvert 1\rvert_3$ → 1. kořen | |
    | $\lvert 9^2\rvert_{15}=\lvert 6\rvert_{15}$ | $\gcd(6,15)=3$ | | nevyhovuje $\gcd(a,n)=1$ |
    
    - 1, 4 jsou 4-násobná kvadratická residua; 9, 10, 6 nesplňují podmínku $\gcd(a,n) = 1$
    - 2, 3, 5, 7, 8, 11, 12, 13, 14 jsou kvadratická nonresiduua
    - Pro $n = 5 \cdot 7 = 35$ je 6 kvadratických residuí: 1, 4, 9, 11, 16, 29 — každé má přesně 4 kořeny odmocniny

---

## 9.3 Legendreův a Jacobiho symbol

### Legendreův symbol

!!! info "Definice — Legendreův symbol"
    Nechť $p$ je liché prvočíslo, dále mějme celé číslo $a$ a platí $p \nmid a$ → definujeme Legendreův symbol následovně:
    
    $$\left(\frac{a}{p}\right) = \begin{cases} 1 & \text{když } a \text{ je kvadratickým residuem} \\ -1 & \text{když } a \text{ je kvadratickým nonresiduem} \end{cases}$$

!!! info "Věta 33 — Eulerovo kritérium"
    Nechť $p$ je liché prvočíslo, $a$ je celé kladné číslo a platí $p \nmid a$:
    
    $$\left(\frac{a}{p}\right) \equiv a^{\frac{p-1}{2}} \pmod{p}$$

**Zjednodušující předpisy pro výpočet Legendreovy funkce:**

1. Když $a = 1$ → $\left(\frac{a}{p}\right) = 1$.
2. Když $a$ je sudé → $\left(\frac{a}{p}\right) = \left(\frac{a/2}{p}\right) \cdot (-1)^{\frac{p^2-1}{8}}$.
3. Když $a > 1$ je liché → $\left(\frac{a}{p}\right) = \left(\frac{|p|_a}{a}\right) \cdot (-1)^{\frac{(a-1)(p-1)}{4}}$.

Pomocí těchto zjednodušujících předpisů lze efektivněji určit, zda je $a$ kvadratickým residuem modulo $p$, kde $p$ je prvočíslo.

!!! example "Příklady"
    $\left(\frac{1}{5}\right) = \left(\frac{4}{5}\right) = 1$ a $\left(\frac{2}{5}\right) = \left(\frac{3}{5}\right) = -1$

### Jacobiho symbol

Jacobiho symbol je zobecněním Legendreovy funkce pro **složené moduly**. Definuje se pro celé číslo $a$ a lichý celočíselný modul $n$.

!!! info "Definice — Jacobiho symbol"
    Nechť $n$ je liché celé číslo s kanonickým rozkladem $n = p_1^{\alpha_1} \cdot p_2^{\alpha_2} \cdots p_k^{\alpha_k}$, kde $p_1 < p_2 < \cdots < p_k$ jsou prvočísla a $\alpha_1, \ldots, \alpha_k$ jsou přirozená čísla. Dále nechť $a$ je celé číslo nesoudělné s $n$ platí:
    
    $$\left[\frac{a}{n}\right] = \left[\frac{a}{p_1^{\alpha_1} \cdot p_2^{\alpha_2} \cdots p_k^{\alpha_k}}\right] = \left(\frac{a}{p_1}\right)^{\alpha_1} \left(\frac{a}{p_2}\right)^{\alpha_2} \cdots \left(\frac{a}{p_k}\right)^{\alpha_k}$$

!!! example "Příklady"
    1. $\left[\frac{2}{45}\right] = \left[\frac{2}{3^2 \cdot 5}\right] = \left(\frac{2}{3}\right)^2 \left(\frac{2}{5}\right) = (-1)^2 (-1) = -1$.
    2. $\left[\frac{2}{15}\right] = \left(\frac{2}{3}\right)\left(\frac{2}{5}\right) = (-1)(-1) = 1$ → Jaké $x$ pro $x^2 \equiv 2 \pmod{15}$? (Neexistuje! Jacobiho symbol $\neq$ Legendreův symbol!)

!!! warning "Pozor na Jacobiho symbol"
    $\left[\frac{a}{n}\right] = +1$ **neznamená** nutně, že $a$ je QR mod $n$! Platí jen pro prvočísla (Legendreův symbol). Vlastnosti kvadratických residuí se využívají v testech pro vyhledávání prvočísel.

---

## 9.4 Generátory (primitivní kořeny)

!!! info "Definice — Generátor"
    Pokud $p$ je prvočíslo a celé číslo $g$ je menší než $p$ a bude-li dále pro každé číslo $b \in \langle 1, p-1 \rangle$ existovat nějaké číslo $a$ takové, že platí $g^a \equiv b \pmod{p}$ → číslo $g$ je **generátor** modulo $p$, tj. $g$ je k $p$ **primitivní**.

!!! example "Příklad: $p = 7$, $g = 3$"
    $|3^6|_7 = 1, \quad |3^2|_7 = 2, \quad |3^1|_7 = 3, \quad |3^4|_7 = 4, \quad |3^5|_7 = 5, \quad |3^3|_7 = 6$
    
    Každé číslo od 1 do 6 se dá vyjádřit jako $|3^a|_7$. Pro $p = 7$ jsou generátory čísla **3 a 5**. Čísla 2, 4 a 6 nejsou generátory.

Hledání generátorů je obecně **obtížný problém**. Generátory modulo prvočíslo $p$ hledáme tak, že náhodně zvolíme číslo z intervalu $\langle 2, p-1 \rangle$ a testujeme je. V případě znalosti kanonického rozkladu čísla $(p-1)$ je testování jednodušší.

!!! info "Věta 34 — Hledání generátorů"
    Nechť $p$ je prvočíslo a $p - 1 = p_1^{\alpha_1} \cdot p_2^{\alpha_2} \cdots p_k^{\alpha_k}$, je kanonický rozklad $p - 1$, kde $p_1 < p_2 < \cdots < p_k$ jsou prvočísla a $\alpha_1, \ldots, \alpha_k$ jsou přirozená čísla. Celé číslo $g$ je generátorem modulo $p$, pokud pro všechny hodnoty $p_1, p_2, \ldots, p_k$ platí:
    
    $$\left|g^{\frac{p-1}{p_i}}\right|_p \neq 1$$

!!! example "Příklad: $p = 13$, $p - 1 = 12 = 3 \cdot 2^2$"
    Pro testování čísla **2** jako generátoru vypočítáme:
    - $\left|2^{\frac{12}{3}}\right|_{13} = |2^4|_{13} = |16|_{13} = 3$. Žádný z výsledků není roven 1 → testujeme dál.
    - $\left|2^{\frac{12}{2^2}}\right|_{13} = |2^3|_{13} = 8$. Také není 1 → **číslo 2 je generátorem modulo 13**.
    
    Pro testování čísla **3** jako generátoru:
    - $\left|3^{\frac{12}{3}}\right|_{13} = |3^4|_{13} = |81|_{13} = 3$. Není 1 → testujeme dál.
    - $\left|3^{\frac{12}{4}}\right|_{13} = |3^3|_{13} = |27|_{13} = 1$ → **3 nemůže být generátorem modulo 13**.

---

## 9.5 Rozklad složených čísel

- Rozklad čísel na prvočinitele ∈ nejstarší problémy teorie čísel.
- Rozklad není obtížný, ale je **časově náročný**.

### Známé algoritmy pro rozklad čísel

| Algoritmus | Zkratka | Rychlost |
|-----------|---------|---------|
| **Síto číselného pole** — Number Field Sieve | NFS | Nejrychlejší pro 110+ místních čísel |
| **Kvadratické síto** — Quadratic Sieve | QS | Rychlý pro čísla do 110 dekadických číslic |
| **Eliptická metoda** — Elliptic Curve Method | ECM | Do 43 místních čísel |
| Pollardův algoritmus Monte Carlo + Algoritmus řetězových zlomků | | Méně používané |
| **Zkusmé dělení** — Trial Division | TD | Nejstarší, testování každého prvočísla ≤ $\sqrt{n}$ |

### Vztah faktorizace a výpočtu odmocnin

- Pokud $n$ je součin 2 prvočísel → výpočet kořenů odmocniny modulo $n$ je z hlediska náročnosti výpočtu rovna faktorizaci $n$.
- Pokud **známe** prvočíselný rozklad $n$ → lze snadno spočítat kořeny odmocniny modulo $n$.
- Jinak je výpočet obtížný, jako rozklad čísla na prvočinitele.

!!! note "Příklad velikosti prostoru prvočísel"
    $\pi(2^{512}) \approx 10^{151}$. Vesmír má $\approx 10^{77}$ atomů. Kdyby každý atom spotřeboval od počátku vzniku vesmíru až do dnes každou $\mu\text{s}$ 1 miliardu prvočísel → by to bylo dohromady $10^{109}$ prvočísel.

**Správný postup** generování prvočísel nezačíná jejich náhodným generováním a následným rozkladem na prvočinitele. Správný postup je **testování vygenerovaných čísel na prvočíselnost**. Testy na prvočíselnost určí s danou pravděpodobností skutečnost, že vygenerované číslo je prvočíslo.

---

## 9.6 Testy prvočíselnosti

### Solovay-Strassenův test

Test čísla $p$ na prvočíselnost:

1. Vybereme náhodné liché $a < p$.
2. Když $\gcd(a, p) \neq 1$ → $p$ **není prvočíslo**.
3. Vypočítáme $j = \left|a^{\frac{p-1}{2}}\right|_p$.
4. Když $j \neq \left(\frac{a}{p}\right)$ → $p$ **určitě není prvočíslo**.
5. Když $j = \left(\frac{a}{p}\right)$ → **pravděpodobnost**, že $p$ je složené, je $\leq 50\%$.
---
- $a$, které dosvědčí, že $p$ není prvočíslo, říkáme **svědek** (*Witness*).
- Když $p$ je složené → pravděpodobnost vystupování náhodného čísla $a$ jako svědka je $\geq 50\%$.
- Opakováním testu $t$ krát pokaždé s jinou hodnotou $a$ docílíme, že pravděpodobnost toho, že složené $p$ projde všemi testy jako prvočíslo, je menší než $2^{-t}$.

---

### Lehmannův test

Test čísla $p$ na prvočíselnost:

1. Vybereme náhodné liché $a < p$.
2. Vypočítáme $j = \left|a^{\frac{p-1}{2}}\right|_p$.
3. Když $j \not\equiv \pm 1 \pmod{p}$ → $p$ **určitě není prvočíslo**.
4. Když $j \equiv \pm 1 \pmod{p}$ → pravděpodobnost, že $p$ je složené, je $\leq 50\%$.
---
- Jednoduší test na prvočíselnost.
- Opět: pravděpodobnost composite p passing t tests < $2^{-t}$; přitom se musí vyskytnout minimálně jednou hodnota $-1$ (krok 2 až 4).

---

### Rabin-Millerův test

Zvolíme náhodně $p$ a spočítáme $b$ a $m$ tak, aby platilo: $p = 1 + 2^b m$, kde $m$ musí být liché.

1. Vybereme náhodné liché $a < p$.
2. Nechť $j = 0$ a $z \leftarrow |a^m|_p$.
3. Když $z = 1$ → $p$ může být prvočíslem; k další iteraci.
4. Dokud $z \neq p - 1$ a $j \leq b - 2$ → opakuj $z \leftarrow |z^2|_p$, $j \leftarrow j + 1$.
5. Když $z \neq p - 1$ → $p$ **určitě není prvočíslo**.
---
- Zjednodušená verze testu na prvočíselnost doporučeného normou DSS.
- Pravděpodobnost průchodu složeného čísla testem jako prvočísla **klesá rychleji** než u předchozích testů.
- $\frac{3}{4}$ hodnot $a$ lze tvrdit, že mohou vystupovat v roli **svědků**.
- Znamená to, že složené číslo nepronikne $t$ testy s pravděpodobností **$\leq 4^{-t}$**.

| $t$ | Pravděpodobnost chyby |
|-----|----------------------|
| 10 | $< 10^{-6}$ |
| 20 | $< 10^{-12}$ |
| 40 | $< 10^{-24}$ |

!!! example "Příklad: $p = 561 = 3 \times 11 \times 17$ (Carmichaelovo číslo)"
    $561 - 1 = 560 = 2^4 \cdot 35$ → $b = 4$, $m = 35$
    
    Test s $a = 2$: $z = 2^{35} \bmod 561 = 263$
    
    $263 \neq 1$ a $263 \neq 560$ → pokračujeme:
    - $j=0$: $z = 263^2 \bmod 561 = 166$, $166 \neq 560$
    - $j=1$: $z = 166^2 \bmod 561 = 67$, $67 \neq 560$
    - $j=2$: $z = 67^2 \bmod 561 = 1$, $1 \neq 560$, $j=2 > b-2=2$ → **JISTĚ SLOŽENÉ** ✗

---

### Rady pro generování prvočísel

Praktický postup generování $n$-bitového prvočísla:

1. **Vygeneruj náhodné číslo** $p$ s požadovanou délkou bitů $n$.
2. **Nastav MSB = LSB = 1:** MSB = 1 zaručí požadovanou délku, LSB = 1 zaručí liché číslo.
3. **Prověř dělitelnost malými prvočísly** (prvočísla < 1000). Testování lichého $p$ na prvočíselnost čísly 3, 5 a 7 vyloučí **54 % složených čísel**; testování s prvočísly < 256 vyloučí **80 % složených čísel**.
4. **Proveď Rabin-Millerův test** s náhodně generovanými čísly $a$. Volíme menší $a$. Opakujeme minimálně **5-krát**.
5. **V případě, že $p$ v některém testu nevyhoví, vygenerujeme jiné $p$.**

Implementace takovéto metody trvá v závislosti na délce prvočísla **řádově sekundy až desítky sekund**.

---

### Silná prvočísla

Když $n$ má být součinem 2 **silných prvočísel** $p$ a $q$ → silná prvočísla mají mít vlastnosti ztěžující rozklad čísla $n$ na prvočinitele:

- $\gcd(p-1)$ a $(q-1)$ má být malý.
- $(p-1)$ a $(q-1)$ mají mít velké prvočísla $p'$ a $q'$.
- $(p'-1)$, $(q'-1)$, $(p'+1)$ a $(q'+1)$ mají mít velké prvočísla.
- $(p-1)/2$ a $(q-1)/2$ mají být prvočísla.

!!! warning "Poznámka k silným prvočíslům"
    Použití silných prvočísel je předmětem diskusí: **délka prvočísel je důležitější než jejich struktura**. Struktura může být na škodu náhodnosti.

---

## 9.7 Náhodná čísla v kryptografii

### Motivace

Mnoho kryptografických aplikací vyžaduje **náhodná čísla**:

- Generování kryptografických klíčů
- Generování čísel *nonce*, *salt*, výplní (*padding*)
- Vernamova šifra (*one-time pad*)

Vyžadovaná „kvalita" náhodnosti se u různých aplikací liší:

- *Nonce* v některých protokolech stačí **jedinečné**
- Generování klíčů vyžaduje **vyšší kvalitu**
- Záruka nerozluštitelnosti Vernamovy šifry platí jen v případě, že klíč byl získán ze skutečně náhodného zdroje s **vysokou entropií**

!!! danger "Základní princip"
    „**Kryptosystém je jen tak silný, jak silný je jeho nejslabší článek.**"
    
    Chybně navržený nebo chybně použitý generátor náhodných čísel může představovat **fatální slabinu** celého kryptosystému.

### Pojmy

- **Náhodné číslo** je číslo vygenerované procesem, který má **nepředvídatelný výsledek** a jehož průběh nelze přesně reprodukovat. Tomuto procesu říkáme *generátor náhodných čísel* (RNG — Random Number Generator).
- V počítači se čísla reprezentují pomocí bitů → často pracujeme s **náhodnými bity** resp. *generátory náhodných bitů* a *posloupnostmi (řetězci) náhodných bitů*.

### Statistické vlastnosti náhodných posloupností

Od náhodných posloupností očekáváme **dobré statistické vlastnosti**:

- **Rovnoměrné rozdělení** — všechny hodnoty jsou generovány se stejnou pravděpodobností
- **Nezávislost** — jednotlivé generované hodnoty jsou *nezávislé* — není mezi nimi žádná korelace

Důležitým pojmem je **entropie**.

### Entropie generátorů

Veličina *entropie* popisuje **míru náhodnosti** — jak obtížné je hodnotu (náhodné číslo, náhodnou posloupnost, řetězec náhodných bitů) uhodnout.

Entropie se vždy vztahuje k útočníkovi a jeho schopnostem (či neschopnostech) předpovědět vygenerovanou hodnotu. Pokud útočník následující generovanou hodnotu s jistotou zná, entropie je nulová (a nulová je i bezpečnost aplikace, která takto generovanou náhodnou hodnotu využívá).

!!! info "Kdy je entropie generátoru náhodných bitů maximální?"
    Entropie generátoru je maximální, pokud se pro danou délku (počet bitů) generují všechny možné posloupnosti, každá z nich se stejnou pravděpodobností.

---

## 9.8 Pseudonáhodné generátory (PRNG)

Počítače pracují deterministicky → jak generovat náhodná čísla?

!!! info "Generátor pseudonáhodných čísel (PRNG)"
    Algoritmus, jehož výstupem je posloupnost, která sice ve skutečnosti **není** náhodná, ale která se **zdá být** náhodná, pokud útočníkovi nejsou známy některé parametry generátoru.

Vlastnosti:

- Algoritmické → snadno realizovatelné
- Obvykle **rychlé**
- Zpravidla mají dobré statistické vlastnosti
- Ale: výstup je **předvídatelný**

### Lineární kongruenční generátor (LCG)

Jeden z nejstarších a nejznámějších způsobů generování pseudonáhodných čísel je **lineární kongruenční generátor**:

$$X_{n+1} = (aX_n + c) \bmod m \tag{1}$$

kde $X$ je posloupnost pseudonáhodných čísel, $m > 0$ je modul (často mocnina dvou), $a$ je násobitel, $c$ je inkrement a $X_0$ je počáteční hodnota (*seed*).

Pseudonáhodná posloupnost $X$ se opakuje nejvýše po $m$ iteracích. Tohoto maxima dosáhneme, pokud jsou splněny:

- Čísla $c$ a $m$ jsou nesoudělná
- $a - 1$ je dělitelné všemi prvočiniteli $m$
- Pokud $4 | m$, pak také $4 | a - 1$

!!! danger "LCG není kryptograficky bezpečný"
    - Pokud se generovaná čísla použijí jako souřadnice bodů v $n$-rozměrném prostoru, výsledné body budou ležet na nejvýše $m^{1/n}$ hyperrovinách.
    - Když $m$ je mocnina dvou, nízké bity $X$ mají mnohem kratší periodu než celá posloupnost.
    - **Lineární kongruenční generátor není kryptograficky bezpečný.**

### Kryptograficky bezpečné PRNG

Požadavky na kryptograficky bezpečné pseudonáhodné generátory:

- **„Next-bit test"**: Je-li známo prvních $k$ bitů náhodné posloupnosti, neexistuje žádný algoritmus s polynomiální složitostí, který by dokázal předpovědět $(k+1)$-tý bit s pravděpodobností úspěchu vyšší než $\frac{1}{2}$.
- **„State compromise"**: I když je zjištěn vnitřní stav generátoru (ať už celý nebo zčásti), nelze zpětně zrekonstruovat dosavadní vygenerovanou náhodnou posloupnost. Navíc, pokud do generátoru za běhu vstupuje další entropie, nemělo by být možné ze znalosti vnitřního stavu předpovědět vnitřní stav v následujících iteracích.

Příklady realizace kryptograficky bezpečných PRNG:

- **Bezpečná bloková šifra v režimu čítače**: Náhodně zvolit klíč (*seed*) a počáteční hodnotu čítače $i$. Postupně šifrovat hodnoty $i, i+1$, atd.
- **Kryptograficky bezpečná hešovací funkce aplikovaná na čítač**: Náhodně zvolit počáteční hodnotu čítače $i$. Postupně hashovat $i, i+1$, atd.
- **Proudové šifry** jsou v zásadě PRNG, s jejichž výstupem se XORuje plaintext.
- **Algoritmy založené na teorii čísel**, u kterých byl proveden (alespoň nějaký) důkaz bezpečnosti.

---

## 9.9 Blum-Blum-Shub (BBS)

Příkladem PRNG, u kterého se má za to, že je kryptograficky bezpečný, je algoritmus **Blum-Blum-Shub**:

$$X_{n+1} = X_n^2 \bmod m \tag{2}$$

- Modul $m = pq$ je součinem dvou velkých prvočísel $p$ a $q$.
- Počáteční prvek (*seed*) je $X_0 > 1$. Mělo by platit, že $p, q \equiv 3 \pmod{4}$ a $\gcd(\varphi(p-1), \varphi(q-1))$ by měl být malý.
- Výstupem zpravidla není přímo hodnota $X_n$, ale její **parita nebo několik nejméně významných bitů**.

**Vlastnosti:**

- **Pomalý**
- Poměrně silný důkaz bezpečnosti (spojuje ji s výpočetní náročností faktorizace celých čísel)
- Lze přímo spočítat $i$-tý prvek posloupnosti:
- 
$$X_i = \left(X_0^{2^i \bmod (p-1)(q-1)}\right) \bmod m \tag{3}$$

!!! warning "PRNG potřebuje skutečně náhodný seed"
    Zmíněné PRNG vyžadují náhodný a tajný vstup, *seed*:

    - Bez nějaké skutečné náhody se stejně neobejdeme.
    - Kvalita PRNG se odvíjí i od kvality hodnoty *seed*.
    - Entropie výstupu PRNG: dána entropií, která vstupuje (*seed*), **algoritmus samotný nikdy nemůže entropii zvyšovat**.

---

## 9.10 Skutečně náhodné generátory (TRNG)

Společná vlastnost kryptograficky bezpečných PRNG: Neobejdou se bez parametrů (zejm. *seed*), které je třeba zvolit náhodně. **PRNG samy o sobě v kryptografii nestačí** — je třeba umět generovat skutečně náhodná čísla resp. bity.

!!! info "Generátory skutečně náhodných čísel (TRNG)"
    TRNG (*True Random Number Generator*) využívají **zdroj entropie**, kterým je zpravidla nějaký fyzikální jev nebo vnější vliv. Například:

    - Radioaktivní rozpad (projekt HotBits)
    - Atmosférický šum (viz projekt random.org)
    - Tepelný šum, např. na analogových součástkách
    - Chování uživatele (pohyb myši, prodlevy při psaní na klávesnici)

**Vlastnosti generátorů skutečně náhodných čísel:**

- Výstup není předvídatelný, i když známe všechny parametry
- Výstup má zpravidla **horší statistické vlastnosti** → je nutné následné zpracování
- Implementace je složitější, často vyžaduje **dodatečný dedikovaný hardware**
- Zdroj entropie je třeba **průběžně testovat**, časem se mohou zhoršit jeho vlastnosti

### Post-processing TRNG

Následné zpracování (*post-processing*) má za cíl vylepšit statistické vlastnosti TRNG, zejména:

- **Odstranění nevyváženosti jedniček a nul** (*bias*) a zajištění rovnoměrného rozdělení
- **Extrakce entropie** — zvýšení entropie výstupních bitů za cenu snížení rychlosti jejich generování (*bitrate*)

**Von Neumannův dekorelátor** — schopen eliminovat nevyváženost a snížit korelovanost výstupu:

| Vstup | Výstup |
|-------|--------|
| `00`, `11` | — (vstup se zahodí) |
| `01` | `0` |
| `10` | `1` |

Bity se odebírají po dvou. Další možnosti:

- Výstup TRNG se XOR-uje s výstupem kryptograficky silného PRNG
- Sloučení (XOR) výstupů dvou nebo více různých TRNG (*software whitening*)
- Hešování výstupu TRNG kryptograficky kvalitní hešovací funkcí

---

## 9.11 Testování náhodných generátorů

K ověření vlastností náhodných generátorů se používají **statistické testy**. Testy ověřují, zda generovaná posloupnost splňuje některé vlastnosti náhodné posloupnosti.

!!! warning "Pozor na interpretaci testů"
    Statistickými testy lze ukázat, že daný generátor nejspíše **NENÍ** kvalitní, ale **nelze prokázat**, že JE kvalitní. Pokud generátor „projde" všemi testy, je pořád možné, že obsahuje slabinu, kterou testy (vzhledem k tomu, jak jsou postaveny) neodhalily.

Statistické testy jsou založeny na **testování statistických hypotéz** na určité hladině významnosti. Nulovou hypotézou je, že testovaná posloupnost je náhodná. Testy vrací **$p$-hodnotu**, která vyjadřuje sílu důkazů proti nulové hypotéze. Pokud tato $p$-hodnota překročí určitou mez, považujeme nulovou hypotézu za neplatnou.

### Příklady statistických testů

| Test | Popis |
|------|-------|
| **Frekvenční test** | Testuje, zda posloupnost bitů obsahuje přibližně stejný počet nul jako jedniček (celá posloupnost i dílčí podposloupnosti) |
| **„Runs" test** | Testuje počet a délka řetězců stejných po sobě jdoucích bitů (samých 1 nebo samých 0) odpovídá náhodné posloupnosti |
| **Test hodností matic** | Zaměřuje se na hodnoty disjunktních podmatic, cílem je odhalit lineární závislost podposloupností pevné délky |
| **Spektrální test** | Diskrétní Fourierova transformace, snaží se odhalit periodicitu |
| **Maurerův universální statistický test** | Testuje, zda lze posloupnost výrazněji bezztrátově zkomprimovat; výrazně komprimovatelná sekvence neobsahuje dostatek entropie |

### Sady testů (baterie)

| Sada | Autoři | Počet testů |
|------|--------|------------|
| **Diehard** | George Marsaglia | 12 různých testů, poměrně silných |
| **Dieharder** | Robert G. Brown | Re-implementace testů Diehard + další |
| **NIST** | National Institute of Standards and Technology | 16 testů |

Tyto sady byly nicméně vyvinuty převážně pro testování PRNG. Při testování TRNG je třeba **důkladně analyzovat zdroj entropie** a navrhnout a provést cílené testy, které by odhalily případné slabiny specifické pro tento zdroj entropie.

---

## Shrnutí kapitoly

!!! abstract "Rychlý přehled"
    - **CRT:** soustava kongruencí → jediné řešení mod $M = \prod m_i$
    - **Kvadratická residua:** $x^2 \equiv a \pmod p$ má 2 řešení nebo žádné; pro prvočíslo $(p-1)/2$ residuí
    - **Legendreův symbol:** $a^{(p-1)/2} \bmod p \in \{1, -1\}$ → QR nebo QNR
    - **Jacobiho symbol:** zobecnění pro složené moduly; $\left[\frac{a}{n}\right]=1$ neznamená QR!
    - **Generátor:** $g$ je generátor mod $p$ pokud $g^{(p-1)/p_i} \not\equiv 1 \pmod p$ pro všechna prvočísla $p_i | (p-1)$
    - **Faktorizace:** NFS nejrychlejší; testování > generování + rozklad
    - **Solovay-Strassen / Lehmann:** chyba $\leq 2^{-t}$; Rabin-Miller: chyba $\leq 4^{-t}$
    - **Generování prvočísel:** MSB=LSB=1, test na malá prvočísla, ≥5× Rabin-Miller
    - **PRNG:** deterministický, rychlý, předvídatelný; LCG není kryptograficky bezpečný
    - **BBS:** $X_{n+1} = X_n^2 \bmod m$; bezpečnost = faktorizace; pomalý
    - **TRNG:** fyzikální šum, nepředvídatelný; post-processing: Von Neumannův dekorelátor
    - **Testování:** Frekvenční, Runs, spektrální, Maurer; sady Diehard, NIST

!!! question "Klíčové otázky ke zkoušce"
    1. Formulujte CRT a spočítejte příklad.
    2. Co je kvadratické residuum? Kolik jich je modulo prvočíslo $p$?
    3. Co je Legendreův symbol a jak ho spočítat (Eulerovo kritérium)?
    4. Jak se liší Legendreův a Jacobiho symbol?
    5. Co je generátor (primitivní kořen) modulo $p$? Jak testovat, zda $g$ je generátor?
    6. Vyjmenujte algoritmy pro faktorizaci čísel a jejich použití.
    7. Popište Rabin-Millerův test. Jaká je pravděpodobnost chyby?
    8. Jaké jsou praktické kroky generování prvočísla? Co jsou silná prvočísla?
    9. Co je PRNG? Proč LCG není kryptograficky bezpečný?
    10. Co je TRNG? Co je Von Neumannův dekorelátor a proč ho potřebujeme?
    11. Co testují statistické testy náhodnosti? Proč nestačí je jen „projít"?
