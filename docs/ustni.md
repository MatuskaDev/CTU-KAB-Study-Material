# Ústní zkouška – příprava

Stručné odpovědi na všechny otázky ústní části zkoušky BI-KAB/BI-BEZ (58 otázek).

!!! tip "Tipy k ústní zkoušce"
    - Zkoušejí **definice, principy a vzorce** – ne detailní výpočty
    - Vždy zdůrazni, **proč** věc funguje nebo proč je bezpečná (na jakém těžkém problému stojí)
    - Přichystej si příklady: Caesarova šifra, DES 56b klíč, SHA-256 kolize $2^{128}$, generátor 3 mod 7
    - U každé šifry vědět: symetrická/asymetrická, bloková/proudová, cíl (konfúze/difúze)

---

## Matematické základy

??? question "1. Šifrování vs. kódování"

    **Šifrování** – převod OT → ŠT za účelem *utajení* obsahu před nepovolanými osobami.
    : Příklady: Caesarova šifra, AES, RSA

    **Kódování** – úprava zprávy pro *přenos po kanálu* nebo *reprezentaci dat*, bez záměru utajit.
    : Příklady: ASCII, Unicode, Hammingův kód, paritní bity

    *→ Skripta: [1.0 – Základní pojmy](skripta/01-klasicka.md#10-zakladni-pojmy-v-kryptologii)*

??? question "2. Malá Fermatova věta (MFV) a Eulerova věta (EV)"

    **MFV:** Pro prvočíslo $p$ a $\gcd(a, p) = 1$:

    $$a^{p-1} \equiv 1 \pmod{p}$$

    **EV:** Pro $\gcd(a, m) = 1$:

    $$a^{\varphi(m)} \equiv 1 \pmod{m}$$

    MFV je speciální případ EV pro $m = p$ (prvočíslo), kde $\varphi(p) = p - 1$.

    !!! tip "Praktické využití"
        Při výpočtu $|a^e|_m$ lze exponent redukovat: $a^e \equiv a^{e \bmod \varphi(m)} \pmod{m}$

    *→ Skripta: [5.1 – Matematické základy](skripta/05-asymetricka.md#51-matematicke-zaklady)*

??? question "3. Eulerova funkce"

    $\varphi(n)$ = počet přirozených čísel $\leq n$ nesoudělných s $n$.

    Pro prvočíselný rozklad $n = p_1^{a_1} \cdots p_k^{a_k}$:

    $$\varphi(n) = n \cdot \prod_{i=1}^{k}\!\left(1 - \frac{1}{p_i}\right)$$

    Speciálně: $\varphi(p) = p-1$, $\quad \varphi(p \cdot q) = (p-1)(q-1)$ pro různá prvočísla, $\quad \varphi(p^k) = p^k - p^{k-1}$.

    Příklad: $\varphi(100) = \varphi(4)\cdot\varphi(25) = 2 \cdot 20 = 40$

    *→ Skripta: [5.1 – Matematické základy](skripta/05-asymetricka.md#51-matematicke-zaklady)*

??? question "7. Modulární počítání"

    - **Kongruence:** $a \equiv b \pmod{m}$ ⟺ $m \mid (a-b)$ ⟺ $a = km + b$
    - **Mult. inverze:** $b^{-1} \pmod{m}$ existuje ⟺ $\gcd(b, m) = 1$; hledá se rozšířeným Euklidovým algoritmem
    - **Euklid.:** $\gcd(a, b) = \gcd(b, a \bmod b)$; $\text{lcm}(a, b) = ab/\gcd(a, b)$

    *→ Skripta: [5.1 – Matematické základy](skripta/05-asymetricka.md#51-matematicke-zaklady)*

??? question "12. Vztah EV a MFV"

    MFV je **speciálním případem** EV pro prvočíselný modul. Eulerova věta je **zobecněním** MFV na složené moduly. Pro $m = p$ je $\varphi(p) = p-1$, tedy EV se redukuje na MFV.

    *→ Skripta: [5.1 – Matematické základy](skripta/05-asymetricka.md#51-matematicke-zaklady)*

??? question "19. Multiplikativní inverze mod m"

    $c$ je multiplikativní inverze $a$ v modulu $m$, pokud $a \cdot c \equiv 1 \pmod{m}$.

    **Existence:** právě tehdy, když $\gcd(a, m) = 1$ a $a \not\equiv 0 \pmod{m}$.

    *→ Skripta: [5.1 – Matematické základy](skripta/05-asymetricka.md#51-matematicke-zaklady)*

??? question "33. Generátor mod p"

    Číslo $g$ je generátor (primitivní kořen) modulo $p$, pokud $\{g^1, g^2, \ldots, g^{p-1}\} = \{1, \ldots, p-1\}$.

    Příklad: $3$ je generátor mod $7$:
    $3^1=3,\ 3^2=2,\ 3^3=6,\ 3^4=4,\ 3^5=5,\ 3^6=1 \pmod{7}$

    *→ Skripta: [9.4 – Generátory](skripta/09-klice.md#94-generatory-primitivni-koreny)*

??? question "39. Základní věta aritmetiky"

    Každé přirozené číslo $> 1$ lze **jednoznačně** rozložit na součin prvočísel (seřazených neklesajícně).

    *→ Skripta: [9.5 – Rozklad složených čísel](skripta/09-klice.md#95-rozklad-slozenych-cisel)*

??? question "40. Funkce π(x)"

    $\pi(x)$ = počet prvočísel $\leq x$. Aproximace:

    $$\pi(x) \approx \frac{x}{\ln x}$$

    Důležité proto, abychom věděli, že prvočísel je dostatek a útočník si nemůže předpočítat všechna.

    *→ Skripta: [9.5 – Rozklad složených čísel](skripta/09-klice.md#95-rozklad-slozenych-cisel)*

??? question "41. Nadbytečnost jazyka"

    $$D = R - r, \qquad R = \log_2 L$$

    kde $L$ = počet znaků abecedy, $r$ = obsažnost jazyka (angličtina $\approx 1{,}5$ b/znak).

    Příklad: angličtina, abeceda 26 znaků: $R = 4{,}7$ b/znak, $D = 3{,}2$ b/znak.

    *→ Skripta: [8.3 – Nadbytečnost jazyka](skripta/08-bezpecnost.md#nadbytecnost-jazyka)*

---

## Klasické šifry

??? question "5. Transpoziční šifra"

    Záměna **pořadí znaků** OT (ne jejich hodnot). Cílem je **difúze**.

    Příklady: sloupcová transpozice (zápis do matice po řádcích, čtení po sloupcích), přesmyčky, lišťovky.

    Odolná vůči frekvenční analýze; lze luštit analýzou vzdáleností bigram.

    *→ Skripta: [1.5 – Transpoziční šifry](skripta/01-klasicka.md#15-transpozicni-sifry)*

??? question "11. Substituční šifry"

    Záměna **hodnoty znaků** podle klíče. Cílem je **konfúze**. Prolamují se frekvenční analýzou.

    | Šifra | Vzorec | Poznámka |
    |-------|--------|----------|
    | Caesarova | $c = (p + k) \bmod m$ | Posuvná, monoalfabetická |
    | Afinní | $c = (ap + b) \bmod m$, $\gcd(a,m)=1$ | Multiplikativní + posun |
    | Vigenèrova | klíčové slovo, opakuje se | Polyalfabetická |
    | Hillova | $\mathbf{c} = A\mathbf{p} \bmod m$, $\gcd(\det A, m)=1$ | Bloková, maticová |

    *→ Skripta: [1.1 – Substituční šifry](skripta/01-klasicka.md#11-monoalfabeticke-substitucni-sifry)*

??? question "13. Vigenèrův autokláv"

    **Asynchronní proudová šifra.** Klíč = 1 počáteční znak; každý další znak hesla = předchozí znak ŠT:

    $$c_1 = p_1 + h_1, \qquad c_i = p_i + c_{i-1} \quad (i \geq 2)$$

    Nevýhoda: znalost jediného znaku klíče + ŠT umožňuje dešifrovat celý text.

    *→ Skripta: [2.3 – Synchronní a asynchronní šifry](skripta/02-proudove.md#23-synchronni-a-asynchronni-proudove-sifry)*

??? question "16. Exponenciální šifra"

    Symetrická šifra. Podmínky: $m$ prvočíslo, $0 < e < m-1$, $\gcd(e, m-1) = 1$.

    $$c = p^e \bmod m, \quad p = c^d \bmod m, \quad d = e^{-1} \bmod (m-1)$$

    Bezpečnost stojí na problému **diskrétního logaritmu**. Šifrování i dešifrování = umocňování.

    *→ Skripta: [5.0 – Exponenciální šifra](skripta/05-asymetricka.md#50-exponencialni-sifra)*

??? question "20. Vernamova šifra (One-time pad)"

    Podmínky: klíč **skutečně náhodný** (TRNG), **stejně dlouhý** jako OT, použit **jen jednou**.

    $$c_i = p_i \oplus k_i$$

    Poskytuje **absolutní (informačně-teoretickou) bezpečnost** – ŠT neobsahuje žádnou informaci o OT.

    *→ Skripta: [2.2 – Vernamova šifra](skripta/02-proudove.md#22-vernamova-sifra-a-absolutni-bezpecnost)*

??? question "22. Konfúze a difúze"

    | Vlastnost | Cíl | Realizuje se |
    |-----------|-----|-------------|
    | **Konfúze** | Skrýt vztah OT–klíč–ŠT; ztížit kryptoanalýzu | Substitucí |
    | **Difúze** | Rozptýlit info o OT po celém ŠT; statistická nerozlišitelnost | Transpozicí |

    Moderní šifry kombinují obojí (Feistelova struktura, AES).

    *→ Skripta: [8.3 – Konfúze a difúze](skripta/08-bezpecnost.md#konfuze-a-difuze)*

---

## Blokové šifry

??? question "6. Feistelova šifra"

    Základní struktura mnoha blokových šifer (DES). Blok se rozdělí na $L_0, R_0$; každá runda:

    $$L_{i+1} = R_i, \qquad R_{i+1} = L_i \oplus f(R_i, k_i)$$

    Dešifrování = šifrování s podklíči v **opačném pořadí**. Šifrování ≈ dešifrování → nižší implementační náklady.

    *→ Skripta: [3.2 – Feistelova síť](skripta/03-blokove.md#32-feistelova-sit)*

??? question "14. DES"

    - Feistelova šifra, 64bitové bloky, 56bitový efektivní klíč (64 b celkem – 8 b parity)
    - 16 rund
    - Dnes bezpečnostně nedostatečný (56b klíč, exhaustive search)

    *→ Skripta: [3.3 – DES](skripta/03-blokove.md#33-des-data-encryption-standard)*

??? question "15. 3DES"

    $\text{ŠT} = E_{K_3}(D_{K_2}(E_{K_1}(\text{OT})))$ (EDE)

    | $K_1 = K_2 = K_3$ | 1 klíč | **56 b** – degraduje na DES |
    |--------------------|--------|----------------------------|
    | $K_1 = K_3 \neq K_2$ | 2 klíče | 112 b |
    | $K_1 \neq K_2 \neq K_3$ | 3 klíče | 168 b |

    EDE umožňuje kompatibilitu s DES (pro $K_1 = K_2 = K_3$ je výsledek čistý DES).

    *→ Skripta: [3.4 – 3DES](skripta/03-blokove.md#34-3des-triple-des)*

??? question "23. AES (Advanced Encryption Standard / Rijndael)"

    - Symetrická bloková šifra, bloky **128 b**, klíče 128/192/256 b
    - 10/12/14 rund dle délky klíče
    - Každá runda: **SubBytes** → **ShiftRows** → **MixColumns** → **AddRoundKey**
    - Nahradil DES; dnes standard (např. WPA2)

    *→ Skripta: [3.5 – AES / Rijndael](skripta/03-blokove.md#35-aes-rijndael)*

---

## Operační módy blokových šifer

??? question "36. CBC (Cipher Block Chaining)"

    $$C_i = E_K(P_i \oplus C_{i-1}), \quad C_0 = IV$$

    Rozšiřuje difúzi přes celou zprávu. Nejpoužívanější mód. Paralelní dešifrování ✓, šifrování ✗.

    *→ Skripta: [3.6 – CBC](skripta/03-blokove.md#36-provozni-mody-blokovych-sifer)*

??? question "43. CTR (Counter Mode)"

    $$C_i = E_K(\text{nonce} \| i) \oplus P_i$$

    Převádí blokovou šifru na **synchronní proudovou šifru**. Plně paralelizovatelný v obou směrech. Umožňuje náhodný přístup k blokům.

    *→ Skripta: [3.6 – CTR](skripta/03-blokove.md#36-provozni-mody-blokovych-sifer)*

??? question "46. Přehled módů"

    | Mód | Typ | Paralelní E/D | Porucha 1 bitu ŠT |
    |-----|-----|---------------|-------------------|
    | ECB | bloková | ✓/✓ | 1 blok OT |
    | CBC | bloková | ✗/✓ | 1 blok OT + 1 bit v dalším |
    | CFB | proudová | ✗/✓ | rozsah "paměti" + 1 bit |
    | OFB | proudová | ✗/✗ | 1 bit |
    | CTR | proudová | ✓/✓ | 1 bit |

    *→ Skripta: [3.6 – Provozní módy](skripta/03-blokove.md#36-provozni-mody-blokovych-sifer)*

---

## Proudové šifry

??? question "35. Synchronní vs. asynchronní proudové šifry"

    **Synchronní:** Proud hesla závisí pouze na klíči (a interním stavu), nezávisí na OT ani ŠT.

    - Příklady: DES/AES v CTR, RC4
    - Výpadek 1 bitu ŠT → ztráta synchronizace celého zbytku

    **Asynchronní:** Proud hesla závisí na $n$ předchozích bitech ŠT.

    - Příklady: Vigenèrův autokláv, CBC jako proudová šifra (CFB)
    - Při výpadku bitu ovlivněno jen $n$ následujících bitů → samooprava

    *→ Skripta: [2.3 – Synchronní a asynchronní šifry](skripta/02-proudove.md#23-synchronni-a-asynchronni-proudove-sifry)*

??? question "10. RC4 – heslo"

    Inicializace permutace $S[0..255]$ dle klíče (KSA – Key Scheduling Algorithm). Pak pseudonáhodné generování bajtů hesla (PRGA), XOR s OT. Pracuje s bajty modulo 256.

    *→ Skripta: [2.4 – RC4](skripta/02-proudove.md#24-rc4)*

---

## Hašovací funkce

??? question "8. MD5/SHA – Damgard-Merklova konstrukce"

    Zpráva rozdělena do bloků (512 b pro MD5/SHA-1/SHA-256; 1024 b pro SHA-384/512).  
    Iterace: $H_i = f(H_{i-1}, M_i)$, $H_0 = IV$.

    **Zarovnání (Damgard-Merklovo zesílení):** přidej bit 1, pak nuly, pak 64bitovou délku zprávy → zpráva nemůže být delší než $2^{64}-1$ bitů.

    | Funkce | Délka hashe | Bezpečnost kolize 1. řádu |
    |--------|-------------|--------------------------|
    | MD5 | 128 b | Kompromitována |
    | SHA-1 | 160 b | Kompromitována |
    | SHA-256 | 256 b | $2^{128}$ |
    | SHA-512 | 512 b | $2^{256}$ |

    *→ Skripta: [4.4 – Damgård-Merklova konstrukce](skripta/04-hash.md#44-damgard-merklova-konstrukce)*

??? question "25. Hašovací funkce – definice"

    Jednosměrná funkce $h: \{0,1\}^* \to \{0,1\}^n$ splňující:

    1. **Jednosměrnost** (preimage resistance) – těžké najít $x$ k danému $h(x)$
    2. **Bezkoliznost 2. řádu** – těžké najít $x' \neq x$ takové, že $h(x') = h(x)$; složitost $2^n$
    3. **Bezkoliznost 1. řádu** – těžké najít libovolné $x \neq x'$ se stejným hashem; složitost $2^{n/2}$

    *→ Skripta: [4.1 – Kryptografická hašovací funkce](skripta/04-hash.md#41-kryptograficka-hasovaci-funkce)*

??? question "26–27. Kolize 1. a 2. řádu"

    | Typ | Co hledáme | Složitost (50 % P) |
    |-----|------------|---------------------|
    | **1. řád** | Libovolné 2 zprávy se stejným hashem | $2^{n/2}$ (narozeninový útok) |
    | **2. řád** | Druhou zprávu kolizní s konkrétně zadanou | $2^n$ |

    *→ Skripta: [4.2 – Bezpečnostní vlastnosti](skripta/04-hash.md#42-bezpecnostni-vlastnosti-a-bezkoliznost)*

??? question "28. Narozeninový paradox"

    Ve skupině 23 lidí je $>50\,\%$ pravděpodobnost, že dvě osoby mají narozeniny ve stejný den.

    Zobecnění: pro množinu $m$ hodnot stačí $\approx\!\sqrt{m}$ pokusů k nalezení kolize s 50 % pravděpodobností.

    $\Rightarrow$ u hashe délky $n$ bitů: $2^{n/2}$ hashů k nalezení **kolize 1. řádu** (nás v kryptografii zajímá nejvíce).

    *→ Skripta: [4.3 – Narozeninový paradox](skripta/04-hash.md#43-narozeninovy-paradox)*

??? question "47. HMAC"

    HMAC = hash-based MAC s tajným klíčem:

    $$\text{HMAC}_K(M) = H\bigl((K \oplus \text{opad}) \,\|\, H\bigl((K \oplus \text{ipad}) \,\|\, M\bigr)\bigr)$$

    Oproti MAC (poslední blok ŠT) používá hašovací funkci místo blokové šifry, je odolnější vůči length-extension útokům.

    Zajišťuje **autentizaci původu dat**, **nikoliv** nepopiratelnost.

    *→ Skripta: [4.7 – HMAC](skripta/04-hash.md#47-hmac)*

??? question "48. Orákulum"

    Deterministický stroj podivuhodných vlastností: na stejný vstup vždy stejný výstup.

    *→ Skripta: [4.1 – Model náhodného orákula](skripta/04-hash.md#model-nahodneho-orakula)*

??? question "49. Náhodné orákulum"

    Na **nový** vstup odpovídá náhodně zvoleným výstupem z množiny možných výstupů; na dříve viděný vstup odpovídá stejně jako poprvé. Matematický model ideální hašovací funkce.

    *→ Skripta: [4.1 – Model náhodného orákula](skripta/04-hash.md#model-nahodneho-orakula)*

---

## Asymetrická kryptografie

??? question "24. RSA – matematický princip"

    1. Zvolíme velká prvočísla $p, q$; $n = p \cdot q$
    2. $\varphi(n) = (p-1)(q-1)$
    3. Zvolíme $e$: $\gcd(e, \varphi(n)) = 1$ → **veřejný klíč** $(e, n)$
    4. $d = e^{-1} \bmod \varphi(n)$ → **soukromý klíč** $(d, n)$
    5. Šifrování: $c = m^e \bmod n$ | Dešifrování: $m = c^d \bmod n$

    **Bezpečnost:** faktorizace $n = p \cdot q$ je výpočetně těžký problém (RSA je prokazatelně bezpečný).

    *→ Skripta: [5.4 – RSA](skripta/05-asymetricka.md#54-rsa)*

??? question "37. Exponenciální šifra vs. RSA"

    | | Exponenciální šifra | RSA |
    |-|---------------------|-----|
    | Typ | Symetrická | Asymetrická |
    | Modul | Prvočíslo $m$ | $n = p \cdot q$ |
    | Bezpečnost | Diskrétní logaritmus | Faktorizace |

    Bezpečnost obou je provázaná – jsou přibližně stejně obtížné.

    *→ Skripta: [5.0 – Exponenciální šifra](skripta/05-asymetricka.md#50-exponencialni-sifra)*

??? question "38. RSA-CRT (pomocí Čínské věty o zbytcích)"

    Soukromý klíč: $(p,\, q,\, d_p,\, d_q,\, q_{\text{inv}})$

    $$d_p = d \bmod (p-1), \quad d_q = d \bmod (q-1), \quad q_{\text{inv}} = q^{-1} \bmod p$$

    **Algoritmus dešifrování** (ze šifrového textu $c$):

    1. $m_1 = c^{d_p} \bmod p$
    2. $m_2 = c^{d_q} \bmod q$
    3. $h = q_{\text{inv}}\,(m_1 - m_2) \bmod p$
    4. $m = m_2 + h \cdot q$

    Kroky 1 a 2 jsou datově nezávislé → lze počítat **paralelně**. Výpočet probíhá s čísly poloviční délky → **4× rychlejší** dešifrování než klasické RSA ($O((L/2)^3)$ místo $O(L^3)$, 2 paralelní větve).

    *→ Skripta: [5.5 – RSA-CRT](skripta/05-asymetricka.md#55-rsa-crt)*

??? question "44. Jednosměrná funkce s padacími vrátky"

    Jednosměrná funkce snadno invertovatelná pouze s **tajnou dodatečnou informací** (soukromým klíčem).

    Analogie: poštovní schránka – vložit může kdokoli (šifrování VK), vybírat jen vlastník klíče (dešifrování SK).

    Základ asymetrické kryptografie (RSA, El Gamal, ECC).

    *→ Skripta: [5.4 – RSA](skripta/05-asymetricka.md#54-rsa)*

??? question "51. El Gamal"

    Asymetrická šifra. Vychází z Diffie-Hellmanovy výměny klíče.

    **Příprava klíče (Alice = příjemce):**  
    Zvolí prvočíslo $m$, generátor $g$, tajný klíč $k_A$.  
    Zveřejní trojici $(m,\, g,\, y_A)$, kde $y_A = g^{k_A} \bmod m$.

    **Šifrování (Bob):**  
    Zvolí náhodné $k_B$, spočítá $y_B = g^{k_B} \bmod m$.  
    Spočítá sdílený klíč $K = y_A^{k_B} \bmod m$.  
    Zašifruje: $c = p \cdot K \bmod m$.  
    Odešle Alici dvojici $(y_B,\, c)$.

    **Dešifrování (Alice):**  
    Spočítá sdílený klíč $K = y_B^{k_A} \bmod m = g^{k_A \cdot k_B} \bmod m$.  
    Spočítá $K^{-1} \bmod m$ (rozšířeným Euklidovým algoritmem).  
    Dešifruje: $p = c \cdot K^{-1} \bmod m$.

    Bezpečnost: **diskrétní logaritmus** (z $y_A = g^{k_A}$ nelze snadno získat $k_A$).

    *→ Skripta: [5.6 – ElGamal](skripta/05-asymetricka.md#56-elgamal)*

---

## Dohoda na klíči

??? question "17. Diffie-Hellman pro 3 uživatele"

    Veřejné: prvočíslo $m$, generátor $a$. Tajné klíče: $k_A, k_B, k_C$.

    Probíhá ve 3 kolech výměny, každý v každém kole přidá svůj exponent. Společný klíč: $K = a^{k_A k_B k_C} \bmod m$.

    Podmínky na klíče: $\gcd(k_i, m-1) = 1$ (doporučeno, zvyšuje bezpečnost).

    *→ Skripta: [5.2 – Diffie-Hellman](skripta/05-asymetricka.md#52-diffie-hellman-vymena-klicu)*

---

## Generování klíčů a náhodnost

??? question "42. Rabin-Millerův test prvočíselnosti"

    Rozklad: $p-1 = 2^b \cdot m$, kde $m$ je **liché**.

    ```
    z ← a^m mod p
    if z == 1 nebo z == p-1:  # pravděpodobně prvočíslo
    for j = 0 to b-2:
        z ← z^2 mod p
        if z == p-1: pravděpodobně prvočíslo
    return SLOŽENÉ
    ```

    Pro libovolné složené $n$ jsou alespoň $\frac{3}{4}$ bází svědky složenosti → opakováním snižujeme chybovost.

    *→ Skripta: [9.6 – Testy prvočíselnosti](skripta/09-klice.md#96-testy-prvociselnosti)*

??? question "55. Fermatův test prvočíselnosti"

    Z MFV: $a^{p-1} \not\equiv 1 \pmod{p}$ → $p$ **určitě není prvočíslo**.  
    $a^{p-1} \equiv 1 \pmod{p}$ → $p$ **pravděpodobně** je prvočíslo.

    Slabina: **Carmichaelova čísla** projdou testem pro každou bázi, přesto jsou složená.

    *→ Skripta: [9.6 – Testy prvočíselnosti](skripta/09-klice.md#96-testy-prvociselnosti)*

??? question "54. John von Neumannův dekorelátor"

    Eliminuje nevyváženost výstupu PRNG. Bity se odebírají po 2:

    | Vstup | Výstup |
    |-------|--------|
    | 00, 11 | zahodit |
    | 10 | **1** |
    | 01 | **0** |

    Příklad: vstup `00 01 11 01 10 01` → zahodíme 00, 11 → výstup: **0, 0, 1, 0** = `0010`

    *→ Skripta: [9.10 – TRNG](skripta/09-klice.md#910-skutecne-nahodne-generatory-trng)*

??? question "57. Jak efektivně získat prvočíslo"

    1. Vygeneruj náhodné $p$ požadované délky (MSB = 1 pro garantovanou délku, LSB = 1 pro lichá)
    2. Otestuj dělitelnost malými prvočísly $< 256$ (vyloučí 80 % složených)
    3. Proveď Rabin-Millerův test ≥ 5×

    *→ Skripta: [9.6 – Testy prvočíselnosti](skripta/09-klice.md#96-testy-prvociselnosti)*

---

## Entropie a informace

??? question "31. Entropie"

    $$H(X) = -\sum_{i=1}^{n} p_i \log_2 p_i$$

    - **Minimum:** $H(X) = 0$ → zdroj vysílá jednu zprávu s $p = 1$ (nic se nedozvíme)
    - **Maximum:** $H(X) = \log_2 n$ → všech $n$ zpráv stejně pravděpodobných

    *→ Skripta: [8.3 – Entropie](skripta/08-bezpecnost.md#entropie)*

??? question "32. Vzdálenost jednoznačnosti"

    $$\delta_U = \frac{H(K)}{D}, \qquad D = R - r, \qquad R = \log_2 L$$

    $H(K)$ = entropie klíče, $D$ = redundance jazyka OT, $L$ = velikost abecedy, $r$ = obsažnost jazyka.

    = minimální délka OT, při které lze (teoreticky) jednoznačně určit klíč.

    *→ Skripta: [8.3 – Vzdálenost jednoznačnosti](skripta/08-bezpecnost.md#vzdalenost-jednoznacnosti)*

---

## PKI a certifikáty

??? question "4. Křížová certifikace"

    Umožňuje důvěru mezi **dvěma různými stromy certifikátů**. Kořenové CA si vzájemně podepíší křížové certifikáty → účastníci různých stromů si mohou navzájem ověřovat certifikáty.

    Typy: jednosměrná (A věří B, ne nutně B věří A), obousměrná.

    *→ Skripta: [10.3 – Certifikační strom](skripta/10-pki.md#103-certifikacni-strom)*

??? question "34. Metody zveřejnění veřejných klíčů"

    1. **Přímé zveřejnění** – snadné, náchylné k podvrhnutí
    2. **Veřejný adresář** – spravuje důvěryhodná autorita; hrozí kompromitace správce
    3. **Autorita pro VK** – účastníci žádají o VK ostatních; nonce pro ověření aktuálnosti
    4. **Certifikace** – CA vydá certifikát; stačí si vyměnit certifikáty (nejpoužívanější)

    *→ Skripta: [10.1 – Distribuce veřejných klíčů](skripta/10-pki.md#101-distribuce-verejnych-klicu)*

??? question "50. Certifikát X.509 – klíčové součásti"

    - Formát, sériové číslo
    - Algoritmus podpisu, identita CA
    - Platnost (od – do), identita držitele
    - Veřejný klíč držitele
    - Digitální podpis CA

    *→ Skripta: [10.2 – Formáty certifikátů X.509](skripta/10-pki.md#102-formaty-certifikatu-podle-x509)*

??? question "52. Solení IV"

    U CBC/OFB/CFB/CTR: partnerovi se pošle $IV$, ale k šifrování se použije $IV' = f(IV, K)$ (např. $H(IV \| K)$). Skutečně použitý IV se nikdy neobjeví na komunikačním kanálu.

    *→ Skripta: [3.6 – Metoda solení IV](skripta/03-blokove.md#metoda-soleni-iv)*

---

## Bezpečnostní architektura

??? question "9. Útoky v OSI modelu"

    **Pasivní** (těžko detekovatelné):
    - Odkrývání obsahu zpráv (plaintext odposlech)
    - Analýza toku dat (i šifrovaných – délky, frekvence)

    **Aktivní** (evidentní efekt):
    - Podvrhnutí identity (MitM)
    - Útok opakováním (replay)
    - Modifikace zprávy
    - Odmítnutí služby (DoS/DDoS)

    *→ Skripta: [8.5 – Typy útočníků](skripta/08-bezpecnost.md#85-typy-utocniku)*

??? question "18. Mechanismy bezpečnosti OSI"

    Digitální podpis · Šifrování · Vyplňování mezer · Řízení směrování · Integrita dat · Osvědčení třetím subjektem · Výměna autentizační informace

    *→ Skripta: [8.1 – Hodnocení odolnosti šifry](skripta/08-bezpecnost.md#81-hodnoceni-odolnosti-sifry)*

---

## ECC a kvantová kryptografie

??? question "45. Řád křivky"

    Celkový počet bodů na eliptické křivce $y^2 = x^3 + ax + b \pmod{p}$ (včetně bodu v nekonečnu $\mathcal{O}$).

    *→ Skripta: [6.5 – ECDLP](skripta/06-ecc.md#65-ecdlp-elliptic-curve-discrete-logarithm-problem)*

??? question "53. Heisenbergův princip neurčitosti"

    $\Delta x \cdot \Delta p \geq \hbar/2$ – nelze současně přesně změřit polohu i hybnost.

    V BB84: nelze určit stav qubitu vůči oběma bázím najednou → **odposlech je fyzicky detekovatelný**.

    *→ Skripta: [7.6 – Protokol BB84](skripta/07-kvanty.md#76-protokol-bb84-benett-brassard-1984)*

---

## Ostatní

??? question "21. Solení hesla"

    Sůl = náhodně vygenerovaný řetězec přidávaný k heslu před hašováním. Ukládá se dvojice $(sůl,\, h(\text{heslo} \| sůl))$.

    **Účel:** Obrana proti rainbow tables a slovníkovým útokům; dva uživatelé se stejným heslem mají odlišné hašované hodnoty.

    *→ Skripta: [4.6 – Využití hašovacích funkcí](skripta/04-hash.md#46-vyuziti-hasovacich-funkci)*

??? question "29. Symetrické vs. asymetrické šifrování"

    | | Symetrické | Asymetrické |
    |-|-----------|-------------|
    | Klíče | Stejný klíč E i D | Veřejný + soukromý |
    | Rychlost | Rychlé | Pomalé |
    | Distribuce klíčů | Problém | Řeší certifikáty |
    | Příklady | AES, DES, Vernam, RC4 | RSA, El Gamal, ECC |

    *→ Skripta: [5.4 – RSA](skripta/05-asymetricka.md#54-rsa)*

??? question "30. Kvadratická residua a nonresidua"

    $a$ je kvadratické reziduum mod $n$, pokud $\exists x: x^2 \equiv a \pmod{n}$.

    Základ Rabinovy funkce – výpočet odmocniny mod $n = p \cdot q$ je výpočetně ekvivalentní faktorizaci $n$ → kandidát na jednosměrnou funkci.

    *→ Skripta: [9.2 – Kvadratická residua](skripta/09-klice.md#92-kvadraticka-residua)*

??? question "56. Útoky postranními kanály"

    Neohrožují matematiku algoritmu, ale **fyzickou implementaci**: časování výpočtu, spotřeba energie, elektromagnetické záření, akustika, světelné emise.

    Cíle: klíč, informace o šifrovacím algoritmu, PIN apod.

    *→ Skripta: [11.7 – Prvky zabezpečení](skripta/11-cipove-karty.md#117-prvky-zabezpeceni)*

??? question "58. Typy čipových karet"

    Kontaktní · Bezkontaktní · Kombinované (kontaktní + bezkontaktní) · Elektrické · Elektromagnetické · Optické

    *→ Skripta: [11.2 – Rozhraní](skripta/11-cipove-karty.md#112-rozhrani)*
