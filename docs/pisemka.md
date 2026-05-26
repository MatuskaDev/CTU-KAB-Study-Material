# Příprava na písemný test

Otázky z minulých testů seřazené tematicky. Odpověď zobrazíš kliknutím na **„Odpověď"**.

!!! tip "Formát písemky"
    - ~6 příkladů, celkem ~30 b (4–10 b za příklad)
    - Mix: pravda/nepravda, výběr z možností, doplňování, výpočet
    - Nejčastější témata: kolize hashů, DES/AES/3DES, entropie, PRNG/BBS/LCG, RSA, certifikáty, BB84

!!! warning "Pozor na typické chyby"
    - 3DES s K₁=K₂=K₃ → **56 b** (ne 168 b!)
    - Podmínka exp. šifry: `gcd(e, m-1) = 1`, **ne** `gcd(e, m) = 1`
    - Digitální podpis **nezajišťuje** důvěrnost – to dělá šifrování
    - RSA je **asymetrická** šifra
    - Se správně zvolenou bází v BB84 je pravděpodobnost správného dekódování **100 %**, ne 50 %

---

## Teorie bezpečnosti a digitální podpis

**Vlastnost nepopiratelnosti elektronického podpisu znamená:**

1. Podepsanou zprávu nelze změnit bez popření podpisu.
2. Vlastník SK může kdykoli prokázat, že mu patří příslušný VK.
3. Podepisující nemá možnost dodatečně popřít, že podpis vytvořil.
4. Platný podpis zprávy může vytvořit pouze vlastník správného VK.

??? success "Odpověď"
    ✅ **(3)**

    > (1) popisuje integritu, (2) popisuje ověření vlastnictví klíče, (4) zaměňuje VK za SK – podpis vytváří vlastník **soukromého** klíče.

---

**Využití digitálního podpisu NEzajistí:**

1. Utajení zprávy
2. Nepopiratelnost
3. Autentizaci
4. Integritu dat

??? success "Odpověď"
    ✅ **(1) Utajení zprávy**

    Digitální podpis zajišťuje integritu, autentizaci a nepopiratelnost. Důvěrnost zajišťuje **šifrování**.

---

**Vyberte pravdivá tvrzení:**

1. Neexistuje bezpečná šifra, která je dokonale nejednoznačná.
2. Bezpečný kryptosystém nemusí být matematicky nedešifrovatelný – stačí výpočetní bezpečnost.
3. Bezpečný kryptosystém musí být vždy matematicky nedešifrovatelný.

??? success "Odpověď"
    ✅ **(2)**

    !!! danger "Oprava chybné odpovědi ze studentských poznámek"
        Tvrzení (1) je **NEPRAVDIVÉ** – dokonale nejednoznačná a zároveň bezpečná šifra existuje: **Vernamova šifra (OTP)**.

---

**Rozhodněte o pravdivosti tvrzení:**

1. Assets zahrnují software, hardware a hrozby (threats).
2. Úroveň rizika je dána pravděpodobností incidentu a dopadem.
3. Úroveň rizika je dána původem hrozby a autentizací.
4. Důvěrnost dat zajišťuje mimo jiné mechanismus digitální podpis.

??? success "Odpověď"
    ✅ **(2)**

    - (1) ✗ – hrozby nejsou assets
    - (3) ✗ – nesprávná definice
    - (4) ✗ – digitální podpis zajišťuje **integritu a nepopiratelnost**, nikoliv důvěrnost

---

## Modulární aritmetika a teorie čísel

**Spočtěte:** $\left|10000000000000000000003^{888888888888888888889}\right|_{10}$

??? success "Odpověď"
    **Výsledek: 3**

    1. $10000000000000000000003 \bmod 10 = 3$
    2. $\varphi(10) = (2-1)(5-1) = 4$
    3. Exponent $\bmod 4$: $888\ldots880 \bmod 4 = 0$, zbyde $9 \bmod 4 = 1$
    4. $3^1 \bmod 10 = \mathbf{3}$

---

**Platí $x \equiv 4 \pmod{5}$ a $x \equiv 3 \pmod{4}$. Kolik je $|x|_{20}$?**

??? success "Odpověď"
    **Výsledek: 19**

    $19 \bmod 5 = 4$ ✓, $19 \bmod 4 = 3$ ✓

---

**Spočtěte:** $\varphi(32)$, $\varphi(64)$, $\gcd(140614,1406)$, $\gcd(21919,219)$, $\gcd(15335,1530)$

??? success "Odpověď"
    - $\varphi(2^5) = \mathbf{16}$
    - $\varphi(2^6) = \mathbf{32}$
    - $\gcd(140614,1406) = \mathbf{2}$
    - $\gcd(21919,219) = \mathbf{1}$
    - $\gcd(15335,1530) = \mathbf{5}$

---

**Vyberte NESPRÁVNÉ možnosti odpovídající $a \equiv b \pmod{m}$:**

1. $|a|_m = |b|$
2. $a + b = k \cdot m,\; k \in \mathbb{Z}$
3. $m \mid (a - b)$

??? success "Odpověď"
    ✅ Nesprávné jsou **(1) a (2)**

    - (1) správně by bylo $|a|_m = |b|_m$; rovnost $|a|_m = |b|$ platí jen pokud $0 \le b < m$
    - (2) správně $a - b = km$, ne $a + b$
    - (3) ✓ přesná definice kongruence

---

**Vyberte SPRÁVNÉ možnosti odpovídající $a \equiv b \pmod{m}$:**

1. $a = km + b,\; k \in \mathbb{Z}$
2. $|a|_m = b$
3. $m \mid (b - a)$

??? success "Odpověď"
    ✅ **(1) a (3)**

    - (2) platí jen pokud $0 \le b < m$

---

## Šifry a operační módy

**Exponenciální šifra: při výběru $e$ a $m$ musí platit ___ . Dešifrovací exponent $d$ vypočítáme jako ___.**

??? success "Odpověď"
    - $m$ prvočíslo, $\;0 < e < m-1$, $\;\gcd(e,\, m-1) = 1$
    - $d = e^{-1} \bmod (m-1)$

    !!! danger "Pozor"
        Podmínka je $\gcd(e,\, \mathbf{m-1}) = 1$, **ne** $\gcd(e, m) = 1$!
        Příklad chyby: $m=29$, $e=7$ → `gcd(7,29)=1` ✓ ale `gcd(7,28)=7≠1` ✗

---

**Šifra 3DES, algoritmus EDE, $K_1 = K_2 = K_3$. Jaká je efektivní velikost klíče? Jak zvýšit bezpečnost?**

??? success "Odpověď"
    **56 bitů** – degraduje na DES.

    Zvýšení bezpečnosti:

    - $K_1 = K_3 \neq K_2$ → **112 b**
    - $K_1 \neq K_2 \neq K_3$ → **168 b**

---

**DES v modu CTR je:**

1. Synchronní šifra
2. Asynchronní šifra
3. Proudová šifra
4. Asymetrická šifra

??? success "Odpověď"
    ✅ **(1) a (3)** – synchronní proudová šifra

---

**Caesarova šifra, posun $k = 5$. Určete předpis pro dešifrování:**

1. $d = (c - 5) \bmod p$
2. $d = (c / 5) \bmod p$
3. $d = (c \cdot 6) \bmod p$
4. $d = (c + 21) \bmod 26$

??? success "Odpověď"
    ✅ **(1)** a **(4)** (varianta 4 platí pouze pro abecedu 26 znaků)

---

**Text délky 32 znaků zašifrovaný transpoziční šifrou. Do kolika sloupců ho lze rozdělit při dešifrování?**

1. 2
2. 6
3. 8
4. 10

??? success "Odpověď"
    ✅ **(1) a (3)** – $32/2=16$ ✓, $32/8=4$ ✓; 6 a 10 nedávají celé číslo.

---

**Které operační módy lze snadno rozluštit při opakovaném použití stejného inicializačního vektoru?**

1. OFB
2. ECB
3. CBC
4. CTR

??? success "Odpověď"
    ✅ **(1) OFB** a **(4) CTR**

    Tyto módy generují proud hesla nezávisle na OT → opakovaný IV = identický proud → útočník získá XOR dvou plaintextů. ECB IV nevyužívá. CBC/CFB jsou citlivé na IV jinak.

---

**Hillova šifra, bloky velikosti 3, abeceda 26 znaků. Co musí platit pro determinant šifrovací matice? Kolik různých bloků OT je možné zašifrovat?**

??? success "Odpověď"
    - $\gcd(\det A,\, 26) = 1$
    - Počet různých bloků: $26^3 = 17\,576$

---

**AES v modu ECB: pokud při přenosu poškodíme jeden bit ŠT, kolik bitů OT bude poškozeno?**

??? success "Odpověď"
    **128 bitů** – celý blok AES.

---

**DES v modu ECB: pokud při přenosu poškodíme jeden bit ŠT, kolik bitů OT bude poškozeno?**

??? success "Odpověď"
    **64 bitů** – celý blok DES.

---

**Transpoziční šifra realizuje:**

1. Konfúzi
2. Difúzi
3. Rozptýlení závislostí
4. Záměnu písmen za jiné

??? success "Odpověď"
    ✅ **(2) Difúzi** a **(3) Rozptýlení závislostí**

---

**Požadavky na Vernamovu šifru (vyberte správné):**

1. Klíč generovaný kryptograficky bezpečným PRNG
2. Klíč generovaný skutečně náhodným generátorem (TRNG)
3. Klíč alespoň tak dlouhý jako zpráva
4. Klíč dostatečně dlouhý, aby nebylo možné v rozumné době najít všechny jeho možnosti

??? success "Odpověď"
    ✅ **(2) a (3)**

---

**Co řadíme mezi šifry dle definice šifrování?**

1. Steganografie
2. Samoopravné kódy
3. Šifrování kódovou knihou
4. Sloupcová transpozice

??? success "Odpověď"
    ✅ **(3) a (4)**

---

**RSA-CRT: soukromý klíč bude tvořen ___. Napište vzorce pro každou složku.**

??? success "Odpověď"
    Soukromý klíč: $(p,\; q,\; d_p,\; d_q,\; q_{\text{inv}})$

    $$d_p = d \bmod (p-1), \quad d_q = d \bmod (q-1), \quad q_{\text{inv}} = q^{-1} \bmod p$$

---

**RSA privátní klíč obsahuje $\{n, e, d, p, q, d_p, d_q, q_{\text{inv}}\}$. Rozhodněte:**

1. $p, q$ lze zahodit a stále budeme schopni zprávy dešifrovat.
2. Ponecháme-li jen $p$, $q$, $e$, stále budeme schopni dešifrovat.
3. Odstraníme-li náhodně jeden parametr, lze ho dopočítat z ostatních.
4. Jedná se o soukromý klíč symetrické šifry RSA.

??? success "Odpověď"
    ✅ **(1), (2), (3)** jsou pravdivá.

    - (1) ✓ – $n$ a $d$ stačí
    - (2) ✓ – z $p, q, e$ odvodíme vše ostatní
    - (3) ✓ – RSA parametry jsou vzájemně odvoditelné
    - (4) ✗ – **RSA je asymetrická šifra!**

---

**Mezi asymetrické šifry patří:**

1. A5/1
2. RSA
3. AES
4. El Gamal

??? success "Odpověď"
    ✅ **(2) RSA** a **(4) El Gamal**

    A5/1 = symetrická proudová šifra (GSM). AES = symetrická bloková šifra.

---

## Algoritmy pro zřízení společného klíče

**Diffie-Hellman. Jak vypočítáme veřejný klíč $Y_A$ a sdílený klíč $K$?**

??? success "Odpověď"
    $$Y_A = a^{k_A} \bmod m, \qquad K = Y_B^{k_A} \bmod m = a^{k_A k_B} \bmod m$$

---

**BB84: Alice pošle qubit 1 na lineární bázi. Eva ho odposlechne (náhodná báze) a přepošle. Bob zvolí lineární bázi. S jakou pravděpodobností dostane Bob hodnotu 1?**

1. 25 %
2. 50 %
3. 75 %
4. Žádná z těchto možností

??? success "Odpověď"
    ✅ **(3) 75 %**

    - P(Eva = stejná báze jako Alice) = 0,5 → Bob dostane 1 s P = 1
    - P(Eva = opačná báze) = 0,5 → Bob dostane 1 s P = 0,5
    - Celkem: $0{,}5 \cdot 1 + 0{,}5 \cdot 0{,}5 = 0{,}75$

---

**Zvolte platnost tvrzení o protokolu BB-84:**

1. Pro detekci odposlechu je potřeba obětovat část klíče.
2. Slouží k distribuci sdíleného klíče.
3. Protokol lze provozovat přes standardní Ethernet (1000BASE-T).
4. Při dekódování qubitu se správně zvolenou bází je 50 % pravděpodobnost přečtení správného bitu.

??? success "Odpověď"
    ✅ **(1) a (2)**

    - (3) ✗ – vyžaduje kvantový kanál (přenos fotonů)
    - (4) ✗ – se **správnou** bází je P = **100 %**; 50 % nastává při špatné bázi

---

## Hašovací funkce

**SHA-1: kolik různých vstupních řetězců může vzniknout?**

??? success "Odpověď"
    $2^{160}$ (délka hashe SHA-1 = 160 bitů)

---

**SHA-512: po kolika pokusech nastane kolize 1. řádu s 50 % pravděpodobností?**

??? success "Odpověď"
    $2^{256}$ (narozeninový útok: $2^{n/2} = 2^{512/2}$)

---

**SHA-256: kolik hashů musíme provést k nalezení kolize 2. řádu (ke konkrétní zprávě)?**

??? success "Odpověď"
    $2^{256}$ (= $2^n$ pro hash délky $n = 256$ b)

---

**SHA-1: provedli jsme $2^{80}$ hashů a máme 50% pravděpodobnost na kolizi ___ řádu.**

??? success "Odpověď"
    **1. řádu** (narozeninový): $2^{80} = 2^{160/2}$.

    Kolize 2. řádu (ke konkrétní zprávě) by vyžadovala $2^{160}$ hashů.

---

**Popište Damgard-Merklovu konstrukci hašovací funkce při použití AES jako kompresní funkce. Uveďte velikost bloku a způsob zpracování zprávy.**

??? success "Odpověď"
    - Délka bloku: **128 bitů** (= blok AES)
    - Zarovnání: přidej bit 1, pak nuly, pak 64bitovou délku zprávy (D-M zesílení)
    - Iterace: $H_i = \text{AES}(H_{i-1},\, M_i)$, kde $H_0 = IV$
    - Výsledný hash = $H_N$ (128 bitů)

---

**Popište hlavní rozdíly mezi MAC a HMAC algoritmem.**

??? success "Odpověď"
    | | MAC | HMAC |
    |-|-----|------|
    | Stavební blok | Bloková šifra | Hašovací funkce |
    | Tvoří ho | Poslední blok ŠT | $H\bigl((K\oplus\text{opad})\|\,H((K\oplus\text{ipad})\|M)\bigr)$ |
    | Odolnost | Méně odolný | Odolný vůči length-extension útoku |

    Oba zajišťují **autentizaci původu dat**, ale **ne nepopiratelnost**.

---

## Entropie a vzdálenost jednoznačnosti

**Vzdálenost jednoznačnosti $\delta_U$ = ___, kde $H(K)$ je ___ a $D$ je ___.**

??? success "Odpověď"
    $$\delta_U = \frac{H(K)}{D}, \qquad D = R - r, \qquad R = \log_2 L$$

    $H(K)$ = entropie klíče, $D$ = redundance jazyka OT, $L$ = velikost abecedy, $r$ = obsažnost jazyka

---

**Kdy je entropie zdroje nejvyšší? Kdy nejnižší?**

??? success "Odpověď"
    - **Nejvyšší:** všech $n$ zpráv stejně pravděpodobných → $H = \log_2 n$
    - **Nejnižší:** jedna zpráva s $p = 1$ → $H = 0$

    !!! danger "Oprava chybné odpovědi ze studentských poznámek"
        „Entropie je zdola omezená délkou zprávy" je **NEPRAVDIVÉ**. Minimum je $H = 0$, ne délka zprávy.

---

**Jaká bude vzdálenost jednoznačnosti pro AES-192, kódování UTF-32?**

??? success "Odpověď"
    - $H(K) = 192$ b
    - $R = 32$ b, $r \approx 1{,}5$ b → $D = 30{,}5$
    - $\delta_U = 192 / 30{,}5 \approx \mathbf{6{,}3}$ znaků

---

**Spočtěte entropii RNG s pravděpodobnostmi:**
P(000) = 1/2, P(001) = 1/4, P(010) = 1/8, P(011) = 1/16, P(100) = 1/16, ostatní = 0

??? success "Odpověď"
    $$H = \tfrac{1}{2}{\cdot}1 + \tfrac{1}{4}{\cdot}2 + \tfrac{1}{8}{\cdot}3 + \tfrac{1}{16}{\cdot}4 + \tfrac{1}{16}{\cdot}4 = 0{,}5 + 0{,}5 + 0{,}375 + 0{,}25 + 0{,}25 = \mathbf{1{,}875 \text{ b}}$$

---

## Generátory náhodných čísel

**Vyberte pravdivá tvrzení o lineárním kongruenčním generátoru (LCG):**

1. Se znalostí 3 vygenerovaných čísel jsme schopni kompromitovat jeho stav.
2. Není bezpečný PRNG, a proto by se nikdy a nikde neměl použít.
3. Je-li známo prvních $k$ bitů, nelze předpovědět $(k+1)$. bit s pravděpodobností úspěchu vyšší než $\frac{1}{2}$.
4. Vyžaduje seed, který by měl mít vysokou entropii.

??? success "Odpověď"
    ✅ **(4)**

    - (1) ✗ – ke kompromitaci stačí znát parametry; tvrzení je nepřesné
    - (2) ✗ – pro nekryptografické účely (simulace, hry) je použitelný
    - (3) ✗ – LCG není kryptograficky bezpečný, next-bit **lze** předpovědět

---

**LCG: $a=9$, $c=5$, $m=32$. První vygenerovaná hodnota je 20. Jaký byl seed? Je perioda generátoru maximální?**

??? success "Odpověď"
    **Seed:**
    $20 = (9s + 5) \bmod 32 \implies 9s \equiv 15 \pmod{32}$

    $9^{-1} \bmod 32 = 25$ (ověř: $9 \cdot 25 = 225 = 7{\cdot}32 + 1$ ✓)

    $s = 25 \cdot 15 \bmod 32 = 375 \bmod 32 = \mathbf{23}$

    **Perioda je maximální** ($= 32$): $\gcd(5,32)=1$ ✓, $2\mid(a-1)=8$ ✓, $4\mid(a-1)=8$ ✓

---

**BBS generátor: $m=77$, seed $= 10$. Z prvních 6 vygenerovaných hodnot vybereme 3. LSB bit. Jaká bude výsledná sekvence? Co vrátí JvN dekorelátor? Je posloupnost kryptograficky bezpečná?**

??? success "Odpověď"
    Výpočet ($x_{i+1} = x_i^2 \bmod 77$, výstup od $x_1$):

    | $i$ | $x_i$ | binárně | 3. LSB |
    |-----|--------|---------|--------|
    | 1 | 23 | `0001 0111` | **1** |
    | 2 | 67 | `0100 0011` | **0** |
    | 3 | 23 | `0001 0111` | **1** |
    | 4 | 67 | `0100 0011` | **0** |
    | 5 | 23 | `0001 0111` | **1** |
    | 6 | 67 | `0100 0011` | **0** |

    Sekvence: **`101010`**

    JvN (páry $10 \to 1$, $10 \to 1$, $10 \to 1$): výstup = **`111`**

    **Kryptograficky bezpečná: NE** – výstup je čistě periodický (23↔67), nesplňuje next-bit test.

---

**Rabin-Miller test: $p = 13$, $a = 2$. Napiš rozklad $p-1$ ve tvaru $2^b \cdot m$.**

??? success "Odpověď"
    $p - 1 = 12 = 2^2 \cdot 3 \implies b = 2,\; m = 3$ (liché) ✓

---

**JvN dekorelátor. Co vznikne ze vstupu `00 01 11 01 10 01`?**

??? success "Odpověď"
    | Pár | Výstup |
    |-----|--------|
    | 00 | zahodit |
    | 01 | **0** |
    | 11 | zahodit |
    | 01 | **0** |
    | 10 | **1** |
    | 01 | **0** |

    Výsledek: **`0010`**

---

## Alice a Bob – bezpečná komunikace

**Alice a Bob mají certifikáty ze stejného stromu a chtějí bezpečně komunikovat v prostředí s aktivními i pasivními útoky. Popište postup zřízení sdíleného klíče a výměnu zpráv.**

??? success "Odpověď"
    **Zřízení sdíleného klíče:**

    1. Alice a Bob si pošlou **certifikáty**
    2. Každý ověří certifikát druhého pomocí **VK kořenové CA**
    3. Jeden vygeneruje náhodný symetrický klíč $K$, zašifruje ho **VK druhého** a podepíše **svým SK**
    4. Příjemce dešifruje svým SK, ověří podpis VK odesílatele

    **Výměna zpráv:**

    - Data se šifrují symetrickým klíčem $K$ (AES) – RSA je příliš pomalé
    - Integrita se zajišťuje HMAC nebo digitálním podpisem

    !!! tip "Klíčový princip"
        Asymetrie (RSA) slouží jen pro **výměnu klíče a autentizaci**. Data šifruje symetrická šifra.

---

## PKI a certifikáty

**Certifikační autorita (CA) je ___, která ___. Ověření certifikátu pomocí ___.**

??? success "Odpověď"
    CA = **důvěryhodná třetí strana**, která **vydává a aktualizuje certifikáty**.

    Ověření: pomocí **veřejného klíče CA** ($VK_{\text{CA}}$).

---

**Jaké jsou 3 nepostradatelné složky certifikátu?**

??? success "Odpověď"
    1. Identifikátor certifikovaného subjektu
    2. Veřejný klíč certifikovaného subjektu
    3. Doba platnosti certifikátu

---

**Pokud chceme HMAC pro autentizaci původu dat, musíme zajistit:**

1. Zřídit veřejné klíče $VK_x$ a $VK_y$
2. Zřídit společný tajný klíč $K$
3. Nemusíme zajistit žádný klíč
4. HMAC pro tento problém nelze využít

??? success "Odpověď"
    ✅ **(2)** Zřídit společný tajný klíč $K$.

---

**Model bezpečnosti OSI zahrnuje ___ bezpečnosti, ___ bezpečnosti a ___ bezpečnost.**

??? success "Odpověď"
    **Služby** bezpečnosti · **Mechanismy** bezpečnosti · **Útoky na** bezpečnost

---

**Jaké jsou 2 hlavní faktory rizika v informační bezpečnosti?**

??? success "Odpověď"
    1. Pravděpodobnost vzniku incidentu informační bezpečnosti
    2. Dopad incidentu

---

**Vyjmenuj 5 kategorií služeb bezpečnosti dle ISO.**

??? success "Odpověď"
    1. Autentizace
    2. Řízení přístupu
    3. Zabezpečení důvěrnosti dat
    4. Zabezpečení integrity dat
    5. Ochrana proti odmítnutí původu dat (nepopiratelnost)

---

## Komplexní otázky (10 b)

**Napište pseudokód Rabin-Millerova testu. Testujte $p = 17$, báze $a = 8$. Zhodnoťte výsledek.**

??? success "Odpověď"
    Rozklad: $p - 1 = 16 = 2^4 \cdot 1 \implies b = 4,\; m = 1$

    ```
    z ← 8^1 mod 17 = 8
    # z ≠ 1 ani 16, pokračuj:
    z ← 8² mod 17 = 64 mod 17 = 13    # ≠ 16, pokračuj
    z ← 13² mod 17 = 169 mod 17 = 16  # = p-1 → STOP
    ```

    **Výsledek:** 17 je **pravděpodobně prvočíslo** ✓

---

**Popište mód CTR (Counter) – princip, vlastnosti, šifrování i dešifrování.**

??? success "Odpověď"
    $$C_i = E_K(\text{nonce} \| i) \oplus P_i \qquad P_i = E_K(\text{nonce} \| i) \oplus C_i$$

    - Převádí blokovou šifru na **synchronní proudovou šifru**
    - Plně **paralelizovatelný** v obou směrech
    - Umožňuje **náhodný přístup** k blokům
    - Porucha 1 bitu ŠT → porucha právě 1 bitu OT
    - Nonce se **nesmí opakovat** se stejným klíčem
