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

    *→ Skripta: [5.7 – Digitální podpis](skripta/05-asymetricka.md#57-digitalni-podpis)*

---

**Využití digitálního podpisu NEzajistí:**

1. Utajení zprávy
2. Nepopiratelnost
3. Autentizaci
4. Integritu dat

??? success "Odpověď"
    ✅ **(1) Utajení zprávy**

    Digitální podpis zajišťuje integritu, autentizaci a nepopiratelnost. Důvěrnost zajišťuje **šifrování**.

    *→ Skripta: [5.7 – Digitální podpis](skripta/05-asymetricka.md#57-digitalni-podpis)*

---

**Vyberte pravdivá tvrzení:**

1. Neexistuje bezpečná šifra, která je dokonale nejednoznačná.
2. Bezpečný kryptosystém nemusí být matematicky nedešifrovatelný – stačí výpočetní bezpečnost.
3. Bezpečný kryptosystém musí být vždy matematicky nedešifrovatelný.

??? success "Odpověď"
    ✅ **(2)**

    !!! danger "Oprava chybné odpovědi ze studentských poznámek"
        Tvrzení (1) je **NEPRAVDIVÉ** – dokonale nejednoznačná a zároveň bezpečná šifra existuje: **Vernamova šifra (OTP)**.

    *→ Skripta: [8.2 – Typy bezpečnosti](skripta/08-bezpecnost.md#82-typy-bezpecnosti)*

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

    *→ Skripta: [8.2 – Typy bezpečnosti](skripta/08-bezpecnost.md#82-typy-bezpecnosti)*

---

**Digitální podpis NEzajišťuje (označte správné – tj. co podpis NEPOSKYTUJE):**

1. Integritu
2. Nepopiratelnost
3. Dostupnost
4. Utajení

??? success "Odpověď"
    ✅ **(3) a (4)**

    - (1) ✗ – digitální podpis **zajišťuje** integritu
    - (2) ✗ – digitální podpis **zajišťuje** nepopiratelnost
    - (3) ✓ – dostupnost (availability) není vlastností digitálního podpisu
    - (4) ✓ – utajení (důvěrnost) zajišťuje **šifrování**, nikoliv podpis

    *→ Skripta: [5.7 – Digitální podpis](skripta/05-asymetricka.md#57-digitalni-podpis)*

---

**Vlastnost integrity elektronického podpisu znamená:**

1. Podepsanou zprávu nelze změnit bez zneplatnění podpisu.
2. Digitální podpis je vydán pouze důvěryhodné osobě.
3. Podepisující nemá možnost dodatečně popřít, že podpis vytvořil.
4. Platný podpis zprávy může vytvořit pouze vlastník správného **veřejného** klíče.

??? success "Odpověď"
    ✅ **(1)**

    - (1) ✓ – přesná definice **integrity**: podpis zaručuje, že zpráva nebyla pozměněna
    - (2) ✗ – toto popisuje vlastnost certifikační autority / procesu vydávání certifikátů
    - (3) ✗ – toto popisuje **nepopiratelnost** (non-repudiation)
    - (4) ✗ – podpis **vytváří** vlastník **soukromého** klíče; ověřuje se veřejným klíčem

    *→ Skripta: [5.7 – Digitální podpis](skripta/05-asymetricka.md#57-digitalni-podpis)*

---

## Modulární aritmetika a teorie čísel

**Spočtěte:** $\left|10000000000000000000003^{888888888888888888889}\right|_{10}$

??? success "Odpověď"
    **Výsledek: 3**

    1. $10000000000000000000003 \bmod 10 = 3$
    2. $\varphi(10) = (2-1)(5-1) = 4$
    3. Exponent $\bmod 4$: $888\ldots880 \bmod 4 = 0$, zbyde $9 \bmod 4 = 1$
    4. $3^1 \bmod 10 = \mathbf{3}$

    *→ Skripta: [5.1 – Matematické základy](skripta/05-asymetricka.md#51-matematicke-zaklady)*

---

**Platí $x \equiv 4 \pmod{5}$ a $x \equiv 3 \pmod{4}$. Kolik je $|x|_{20}$?**

??? success "Odpověď"
    **Výsledek: 19**

    $19 \bmod 5 = 4$ ✓, $19 \bmod 4 = 3$ ✓

    *→ Skripta: [9.1 – CRT](skripta/09-klice.md#91-cinska-veta-o-zbytcich-crt)*

---

**Spočtěte:** $\varphi(32)$, $\varphi(64)$, $\gcd(140614,1406)$, $\gcd(21919,219)$, $\gcd(15335,1530)$

??? success "Odpověď"
    - $\varphi(2^5) = \mathbf{16}$
    - $\varphi(2^6) = \mathbf{32}$
    - $\gcd(140614,1406) = \mathbf{2}$
    - $\gcd(21919,219) = \mathbf{1}$
    - $\gcd(15335,1530) = \mathbf{5}$

    *→ Skripta: [5.1 – Matematické základy](skripta/05-asymetricka.md#51-matematicke-zaklady)*

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

    *→ Skripta: [5.1 – Matematické základy](skripta/05-asymetricka.md#51-matematicke-zaklady)*

---

**Vyberte SPRÁVNÉ možnosti odpovídající $a \equiv b \pmod{m}$:**

1. $a = km + b,\; k \in \mathbb{Z}$
2. $|a|_m = b$
3. $m \mid (b - a)$

??? success "Odpověď"
    ✅ **(1) a (3)**

    - (2) platí jen pokud $0 \le b < m$

    *→ Skripta: [5.1 – Matematické základy](skripta/05-asymetricka.md#51-matematicke-zaklady)*

---

**Soustava kongruencí: $x \equiv 6 \pmod{7}$ a $x \equiv 10 \pmod{11}$. Jaká je hodnota $|x|_{77}$? Napište 2 algoritmy používané pro výpočet soustav kongruencí.**

??? success "Odpověď"
    **Výsledek: 76**

    CRT: $M = 77$, $M_1 = 11$, $M_2 = 7$

    $y_1 = M_1^{-1} \bmod 7 = 11^{-1} \bmod 7 = 4^{-1} \bmod 7 = 2\quad$ (ověř: $4 \cdot 2 = 8 \equiv 1 \pmod{7}$ ✓)

    $y_2 = M_2^{-1} \bmod 11 = 7^{-1} \bmod 11 = 8\quad$ (ověř: $7 \cdot 8 = 56 = 5 \cdot 11 + 1$ ✓)

    $$x = (6 \cdot 11 \cdot 2 + 10 \cdot 7 \cdot 8) \bmod 77 = (132 + 560) \bmod 77 = 692 \bmod 77 = \mathbf{76}$$

    Ověření: $76 \bmod 7 = 6$ ✓, $76 \bmod 11 = 10$ ✓

    **Algoritmy:**

    1. **Čínská věta o zbytcích (CRT)** – přímý výpočet přes $M_i$ a jejich inverze
    2. **Rozšířený Eukleidův algoritmus** – pro výpočet modulárních inverzí $y_i$

    *→ Skripta: [9.1 – CRT](skripta/09-klice.md#91-cinska-veta-o-zbytcich-crt)*

---

## Šifry a operační módy

**Exponenciální šifra: při výběru $e$ a $m$ musí platit ___ . Dešifrovací exponent $d$ vypočítáme jako ___.**

??? success "Odpověď"
    - $m$ prvočíslo, $\;0 < e < m-1$, $\;\gcd(e,\, m-1) = 1$
    - $d = e^{-1} \bmod (m-1)$

    !!! danger "Pozor"
        Podmínka je $\gcd(e,\, \mathbf{m-1}) = 1$, **ne** $\gcd(e, m) = 1$!
        Příklad chyby: $m=29$, $e=7$ → `gcd(7,29)=1` ✓ ale `gcd(7,28)=7≠1` ✗

    *→ Skripta: [5.0 – Exponenciální šifra](skripta/05-asymetricka.md#50-exponencialni-sifra)*

---

**Šifra 3DES, algoritmus EDE, $K_1 = K_2 = K_3$. Jaká je efektivní velikost klíče? Jak zvýšit bezpečnost?**

??? success "Odpověď"
    **56 bitů** – degraduje na DES.

    Zvýšení bezpečnosti:

    - $K_1 = K_3 \neq K_2$ → **112 b**
    - $K_1 \neq K_2 \neq K_3$ → **168 b**

    *→ Skripta: [3.4 – 3DES](skripta/03-blokove.md#34-3des-triple-des)*

---

**DES v modu CTR je:**

1. Synchronní šifra
2. Asynchronní šifra
3. Proudová šifra
4. Asymetrická šifra

??? success "Odpověď"
    ✅ **(1) a (3)** – synchronní proudová šifra

    *→ Skripta: [3.6 – Provozní módy](skripta/03-blokove.md#36-provozni-mody-blokovych-sifer)*

---

**Caesarova šifra, posun $k = 5$. Určete předpis pro dešifrování:**

1. $d = (c - 5) \bmod p$
2. $d = (c / 5) \bmod p$
3. $d = (c \cdot 6) \bmod p$
4. $d = (c + 21) \bmod 26$

??? success "Odpověď"
    ✅ **(1)** a **(4)** (varianta 4 platí pouze pro abecedu 26 znaků)

    *→ Skripta: [1.1 – Substituční šifry](skripta/01-klasicka.md#11-monoalfabeticke-substitucni-sifry)*

---

**Text délky 32 znaků zašifrovaný transpoziční šifrou. Do kolika sloupců ho lze rozdělit při dešifrování?**

1. 2
2. 6
3. 8
4. 10

??? success "Odpověď"
    ✅ **(1) a (3)** – $32/2=16$ ✓, $32/8=4$ ✓; 6 a 10 nedávají celé číslo.

    *→ Skripta: [1.5 – Transpoziční šifry](skripta/01-klasicka.md#15-transpozicni-sifry)*

---

**Které operační módy lze snadno rozluštit při opakovaném použití stejného inicializačního vektoru?**

1. OFB
2. ECB
3. CBC
4. CTR

??? success "Odpověď"
    ✅ **(1) OFB** a **(4) CTR**

    Tyto módy generují proud hesla nezávisle na OT → opakovaný IV = identický proud → útočník získá XOR dvou plaintextů. ECB IV nevyužívá. CBC/CFB jsou citlivé na IV jinak.

    *→ Skripta: [3.6 – Provozní módy](skripta/03-blokove.md#36-provozni-mody-blokovych-sifer)*

---

**Hillova šifra, bloky velikosti 3, abeceda 26 znaků. Co musí platit pro determinant šifrovací matice? Kolik různých bloků OT je možné zašifrovat?**

??? success "Odpověď"
    - $\gcd(\det A,\, 26) = 1$
    - Počet různých bloků: $26^3 = 17\,576$

    *→ Skripta: [1.3 – Hillova šifra](skripta/01-klasicka.md#13-polygraficke-substitucni-sifry-hillova-sifra)*

---

**AES v modu ECB: pokud při přenosu poškodíme jeden bit ŠT, kolik bitů OT bude poškozeno?**

??? success "Odpověď"
    **128 bitů** – celý blok AES.

    *→ Skripta: [3.6 – Provozní módy](skripta/03-blokove.md#36-provozni-mody-blokovych-sifer)*

---

**DES v modu ECB: pokud při přenosu poškodíme jeden bit ŠT, kolik bitů OT bude poškozeno?**

??? success "Odpověď"
    **64 bitů** – celý blok DES.

    *→ Skripta: [3.6 – Provozní módy](skripta/03-blokove.md#36-provozni-mody-blokovych-sifer)*

---

**Transpoziční šifra realizuje:**

1. Konfúzi
2. Difúzi
3. Rozptýlení závislostí
4. Záměnu písmen za jiné

??? success "Odpověď"
    ✅ **(2) Difúzi** a **(3) Rozptýlení závislostí**

    *→ Skripta: [1.5 – Transpoziční šifry](skripta/01-klasicka.md#15-transpozicni-sifry)*

---

**Požadavky na Vernamovu šifru (vyberte správné):**

1. Klíč generovaný kryptograficky bezpečným PRNG
2. Klíč generovaný skutečně náhodným generátorem (TRNG)
3. Klíč alespoň tak dlouhý jako zpráva
4. Klíč dostatečně dlouhý, aby nebylo možné v rozumné době najít všechny jeho možnosti

??? success "Odpověď"
    ✅ **(2) a (3)**

    *→ Skripta: [2.2 – Vernamova šifra](skripta/02-proudove.md#22-vernamova-sifra-a-absolutni-bezpecnost)*

---

**Co řadíme mezi šifry dle definice šifrování?**

1. Steganografie
2. Samoopravné kódy
3. Šifrování kódovou knihou
4. Sloupcová transpozice

??? success "Odpověď"
    ✅ **(3) a (4)**

    *→ Skripta: [1.0 – Základní pojmy](skripta/01-klasicka.md#10-zakladni-pojmy-v-kryptologii)*

---

**RSA-CRT: soukromý klíč bude tvořen ___. Napište vzorce pro každou složku.**

??? success "Odpověď"
    Soukromý klíč: $(p,\; q,\; d_p,\; d_q,\; q_{\text{inv}})$

    $$d_p = d \bmod (p-1), \quad d_q = d \bmod (q-1), \quad q_{\text{inv}} = q^{-1} \bmod p$$

    *→ Skripta: [5.5 – RSA-CRT](skripta/05-asymetricka.md#55-rsa-crt)*

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

    *→ Skripta: [5.4 – RSA](skripta/05-asymetricka.md#54-rsa)*

---

**Mezi asymetrické šifry patří:**

1. A5/1
2. RSA
3. AES
4. El Gamal

??? success "Odpověď"
    ✅ **(2) RSA** a **(4) El Gamal**

    A5/1 = symetrická proudová šifra (GSM). AES = symetrická bloková šifra.

    *→ Skripta: [5.4 – RSA](skripta/05-asymetricka.md#54-rsa)*

---

**Transpoziční šifru lze kryptoanalyticky řešit:**

1. Faktorizací délky šifrového textu
2. Hledáním bigramů v šifrovém textu
3. Frekvenční analýzou šifrového textu
4. Frekvenční analýzou otevřeného textu

??? success "Odpověď"
    ✅ **(1) a (2)**

    - (1) ✓ – délka ŠT musí být dělitelná délkou klíče; faktorizace odhalí možné délky klíče
    - (2) ✓ – bigramy v ŠT prozrazují vzory transpoziční šifry
    - (3) ✗ – transpoziční šifra **zachovává četnosti písmen** (pouze mění pořadí); frekvenční analýza jednotlivých znaků klíč neodhalí
    - (4) ✗ – frekvenční analýza OT nepomáhá při útoku pouze na ŠT

    *→ Skripta: [1.5 – Transpoziční šifry](skripta/01-klasicka.md#15-transpozicni-sifry)*

---

**Vyberte pravdivá/nepravdivá tvrzení o Hillově šifře:**

1. Je monoalfabetická (polygrafická substituční šifra).
2. Velikost klíče je nezávislá na velikosti bloku.
3. Dá se luštit pomocí frekvenční kryptoanalýzy (analýzy n-gramů).
4. Jako klíč se dá použít libovolná matice $\mathbb{Z}_L^{N \times N}$, kde $L$ je velikost abecedy a $N$ velikost bloku.

??? success "Odpověď"
    - (1) ✓ – každý blok $N$ znaků se vždy zobrazí na tentýž blok ŠT (monoalfabetická na úrovni n-gramů)
    - (2) ✗ – klíč je matice $N \times N$; pro $N=2$ má 4 prvky, pro $N=3$ má 9 prvků → **závisí na $N$**
    - (3) ✓ – frekvenční analýza n-gramů funguje pro malé $N$
    - (4) ✗ – matice musí splňovat $\gcd(\det A,\, L) = 1$; libovolná matice nemusí být invertovatelná mod $L$

    *→ Skripta: [1.3 – Hillova šifra](skripta/01-klasicka.md#13-polygraficke-substitucni-sifry-hillova-sifra)*

---

**Vyberte pravdivá/nepravdivá tvrzení o RSA a exponenciální šifře:**

1. Jedná se o asymetrické šifry.
2. K urychlení výpočtu lze použít algoritmus Square and Multiply.
3. Můžeme použít stejný exponent $e$ pro více lidí.
4. Používá se různý exponent pro šifrování a dešifrování.

??? success "Odpověď"
    - (1) ✓ – obě jsou asymetrické
    - (2) ✓ – Square and Multiply urychluje modulární umocňování $m^e \bmod n$
    - (3) ✓ – je to běžné (např. $e = 65537$); pozor na Hastadův útok při malém $e$ a více příjemcích se stejnou zprávou
    - (4) ✓ – šifrování exponentem $e$ (veřejný), dešifrování exponentem $d$ (soukromý)

    *→ Skripta: [5.4 – RSA](skripta/05-asymetricka.md#54-rsa)*

---

**Určete pravdivost tvrzení o proudových a blokových šifrách:**

1. U proudových šifer heslo (keystream) závisí pouze na klíči.
2. Operační mód stanovuje, jak probíhá šifrování více bloků OT.
3. Bloková šifra zpracovává OT vždy po jednotlivých znacích, kdežto proudová vždy po jednotlivých bitech.
4. Využitím synchronní proudové šifry docílíme větší difuze oproti asynchronní.

??? success "Odpověď"
    - (1) ✗ – platí pouze pro **synchronní** proudové šifry; u **asynchronních** závisí keystream i na šifrovém textu
    - (2) ✓ – přesná definice operačního módu
    - (3) ✗ – je to **naopak**: bloková šifra zpracovává pevné **bloky**, proudová zpracovává po bitech nebo bytech
    - (4) ✗ – synchronní proudová šifra má **nulovou difuzi** (čistý XOR); větší difuzi má asynchronní varianta

    *→ Skripta: [2.1 – Proudové šifry](skripta/02-proudove.md), [3.6 – Provozní módy](skripta/03-blokove.md#36-provozni-mody-blokovych-sifer)*

---

**Máme hybridní šifru: RSA s modulem délky 2048 bitů a AES-256 v módu CBC. Rozhodněte:**

1. IV bude mít délku 256 bitů.
2. Pro šifrování klíče AES lze použít certifikát adresáta.
3. Zašifrovaný klíč pro AES bude mít délku 2048 bitů.
4. Zašifrovaný klíč pro AES bude mít délku 256 bitů.

??? success "Odpověď"
    - (1) ✗ – AES pracuje s **128bitovým blokem** bez ohledu na délku klíče; **IV = 128 bitů**
    - (2) ✓ – certifikát adresáta obsahuje jeho **VK**, kterým zašifrujeme symetrický klíč AES
    - (3) ✓ – výstup RSA má délku **modulu** = 2048 bitů
    - (4) ✗ – výstup RSA = délka modulu (2048 b), ne délka šifrovaného klíče (256 b)

    *→ Skripta: [5.4 – RSA](skripta/05-asymetricka.md#54-rsa), [3.5 – AES](skripta/03-blokove.md)*

---

**Zpráva $m$ je zašifrována RSA s parametry $(n = 143,\, e = 17)$. Zašifrovanou zprávu $c$ vynásobíme $|6^{17}|_{143} = 41$. Jak se změní původní zpráva $m$ po dešifrování?**

??? success "Odpověď"
    Výsledná dešifrovaná zpráva bude $m' = m \cdot 6 \bmod 143$.

    **Proč:** RSA je **multiplikativně homomorfní**:

    $$c' = c \cdot 41 \bmod 143$$

    Po dešifrování: $m' = (c')^d = c^d \cdot 41^d = m \cdot (6^{17})^d = m \cdot 6^{17d} \bmod n$

    Protože $17d \equiv 1 \pmod{\varphi(n)}$, platí $6^{17d} \equiv 6 \pmod{n}$, tedy $m' = m \cdot 6 \bmod 143$.

    !!! tip "Multiplikativní homomorfismus RSA"
        Tato vlastnost je důvodem, proč se RSA **bez paddingu nepoužívá** pro přímé šifrování dat.

    *→ Skripta: [5.4 – RSA](skripta/05-asymetricka.md#54-rsa)*

---

**FEL a FS komunikují pomocí symetrické šifry s nízkou entropií klíče. V ŠT se některé bloky opakují a poslední blok je vždy stejný. Délka bloku je 16 bajtů. Doplňte:**

- Pravděpodobná použitá šifra
- Použitý operační mód
- Proč je na konci vždy stejný blok
- Jakým způsobem by mohlo dojít k prolomení šifrování

??? success "Odpověď"
    - **Šifra: AES** – bloková šifra s délkou bloku 128 bitů = 16 bajtů
    - **Mód: ECB** – v ECB platí: stejný blok OT + stejný klíč → vždy stejný blok ŠT; proto opakující se bloky OT → opakující se bloky ŠT
    - **Stejný poslední blok:** zprávy mají pravděpodobně stejné zakončení a padding (PKCS#7); poslední blok šifrovaný stejným klíčem = vždy stejný výstup
    - **Prolomení:**
        - Frekvenční analýza bloků ŠT (slovníkový útok)
        - Known-plaintext attack – znalost části OT umožní mapování bloků OT↔ŠT
        - Brute-force na klíč (nízká entropie!)

    *→ Skripta: [3.6 – Provozní módy](skripta/03-blokove.md#36-provozni-mody-blokovych-sifer)*

---

**Uvažujme blokovou šifru pracující v módech a) CTR a b) CBC. Jak ovlivní chyba v jednom bloku ŠT okolní bloky OT?**

??? success "Odpověď"
    **a) CTR:**

    - Chyba v bloku $\hat{C}_i$ se projeví **pouze** v odpovídajícím bloku $P_i$
    - Konkrétně: pouze **bity na stejných pozicích** jako chyba jsou poškozeny (XOR s keystream)
    - Ostatní bloky **nejsou ovlivněny** (keystream závisí na čítači, ne na ŠT)

    **b) CBC:**

    - Chyba v bloku $\hat{C}_i$ ovlivní **dva bloky OT**:
        - $P_i$: celý blok je chybný (výstup $D_K(\hat{C}_i)$ je nepředvídatelný)
        - $P_{i+1}$: chybné jsou **přesně ty bity**, kde byl error v $\hat{C}_i$ (protože $P_{i+1} = D_K(C_{i+1}) \oplus \hat{C}_i$)
    - Bloky $P_{i+2}, P_{i+3}, \ldots$ jsou **správné**

    !!! tip "Shrnutí"
        CTR: chyba → 1 blok, jen odpovídající bity. CBC: chyba → celý blok $i$ + konkrétní bity bloku $i+1$.

    *→ Skripta: [3.6 – Provozní módy](skripta/03-blokove.md#36-provozni-mody-blokovych-sifer)*

---

## Algoritmy pro zřízení společného klíče

**Diffie-Hellman. Jak vypočítáme veřejný klíč $Y_A$ a sdílený klíč $K$?**

??? success "Odpověď"
    $$Y_A = a^{k_A} \bmod m, \qquad K = Y_B^{k_A} \bmod m = a^{k_A k_B} \bmod m$$

    *→ Skripta: [5.2 – Diffie-Hellman](skripta/05-asymetricka.md#52-diffie-hellman-vymena-klicu)*

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

    *→ Skripta: [7.6 – Protokol BB84](skripta/07-kvanty.md#76-protokol-bb84-benett-brassard-1984)*

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

    *→ Skripta: [7.6 – Protokol BB84](skripta/07-kvanty.md#76-protokol-bb84-benett-brassard-1984)*

---

**Popište algoritmy Diffie-Hellman (DH) a ECDH. Zaměřte se na rozdíly mezi nimi.**

??? success "Odpověď"
    **Diffie-Hellman (klasický DH):**

    - Pracuje v multiplikativní grupě $\mathbb{Z}_p^*$ (modulo prvočíslo $p$)
    - $Y_A = g^a \bmod p$, $Y_B = g^b \bmod p$, sdílený klíč $K = g^{ab} \bmod p$
    - Bezpečnost: těžkost **problému diskrétního logaritmu (DLP)** v $\mathbb{Z}_p^*$
    - Typická délka klíče: 2048–4096 bitů

    **ECDH (Elliptic Curve DH):**

    - Pracuje na **eliptické křivce** nad konečným polem $\mathbb{F}_q$
    - $A = a \cdot G$, $B = b \cdot G$, sdílený klíč $K = ab \cdot G$ (skalární násobení bodu)
    - Bezpečnost: těžkost **ECDLP** (problému diskrétního logaritmu na eliptické křivce)

    **Klíčové rozdíly:**

    | | DH | ECDH |
    |-|----|----|
    | Matematická struktura | Multiplikativní grupa $\mathbb{Z}_p^*$ | Aditivní grupa bodů eliptické křivky |
    | Bezpečnostní problém | DLP | ECDLP |
    | Délka klíče pro 128b bezpečnost | ~3072 b | ~256 b |
    | Efektivita | Pomalejší (velká čísla) | Rychlejší (kratší klíče) |

    *→ Skripta: [5.2 – Diffie-Hellman](skripta/05-asymetricka.md#52-diffie-hellman-vymena-klicu), [6. – ECC](skripta/06-ecc.md)*

---

## Hašovací funkce

**SHA-1: kolik různých vstupních řetězců může vzniknout?**

??? success "Odpověď"
    $2^{160}$ (délka hashe SHA-1 = 160 bitů)

    *→ Skripta: [4.5 – SHA-x](skripta/04-hash.md#45-sha-x)*

---

**SHA-512: po kolika pokusech nastane kolize 1. řádu s 50 % pravděpodobností?**

??? success "Odpověď"
    $2^{256}$ (narozeninový útok: $2^{n/2} = 2^{512/2}$)

    *→ Skripta: [4.3 – Narozeninový paradox](skripta/04-hash.md#43-narozeninovy-paradox)*

---

**SHA-256: kolik hashů musíme provést k nalezení kolize 2. řádu (ke konkrétní zprávě)?**

??? success "Odpověď"
    $2^{256}$ (= $2^n$ pro hash délky $n = 256$ b)

    *→ Skripta: [4.2 – Bezpečnostní vlastnosti](skripta/04-hash.md#42-bezpecnostni-vlastnosti-a-bezkoliznost)*

---

**SHA-1: provedli jsme $2^{80}$ hashů a máme 50% pravděpodobnost na kolizi ___ řádu.**

??? success "Odpověď"
    **1. řádu** (narozeninový): $2^{80} = 2^{160/2}$.

    Kolize 2. řádu (ke konkrétní zprávě) by vyžadovala $2^{160}$ hashů.

    *→ Skripta: [4.3 – Narozeninový paradox](skripta/04-hash.md#43-narozeninovy-paradox)*

---

**Popište Damgard-Merklovu konstrukci hašovací funkce při použití AES jako kompresní funkce. Uveďte velikost bloku a způsob zpracování zprávy.**

??? success "Odpověď"
    - Délka bloku: **128 bitů** (= blok AES)
    - Zarovnání: přidej bit 1, pak nuly, pak 64bitovou délku zprávy (D-M zesílení)
    - Iterace: $H_i = \text{AES}(H_{i-1},\, M_i)$, kde $H_0 = IV$
    - Výsledný hash = $H_N$ (128 bitů)

    *→ Skripta: [4.4 – Damgård-Merklova konstrukce](skripta/04-hash.md#44-damgard-merklova-konstrukce)*

---

**Popište hlavní rozdíly mezi MAC a HMAC algoritmem.**

??? success "Odpověď"
    | | MAC | HMAC |
    |-|-----|------|
    | Stavební blok | Bloková šifra | Hašovací funkce |
    | Tvoří ho | Poslední blok ŠT | $H\bigl((K\oplus\text{opad})\|\,H((K\oplus\text{ipad})\|M)\bigr)$ |
    | Odolnost | Méně odolný | Odolný vůči length-extension útoku |

    Oba zajišťují **autentizaci původu dat**, ale **ne nepopiratelnost**.

    *→ Skripta: [4.7 – HMAC](skripta/04-hash.md#47-hmac)*

---

## Entropie a vzdálenost jednoznačnosti

**Vzdálenost jednoznačnosti $\delta_U$ = ___, kde $H(K)$ je ___ a $D$ je ___.**

??? success "Odpověď"
    $$\delta_U = \frac{H(K)}{D}, \qquad D = R - r, \qquad R = \log_2 L$$

    $H(K)$ = entropie klíče, $D$ = redundance jazyka OT, $L$ = velikost abecedy, $r$ = obsažnost jazyka

    *→ Skripta: [8.3 – Vzdálenost jednoznačnosti](skripta/08-bezpecnost.md#vzdalenost-jednoznacnosti)*

---

**Kdy je entropie zdroje nejvyšší? Kdy nejnižší?**

??? success "Odpověď"
    - **Nejvyšší:** všech $n$ zpráv stejně pravděpodobných → $H = \log_2 n$
    - **Nejnižší:** jedna zpráva s $p = 1$ → $H = 0$

    !!! danger "Oprava chybné odpovědi ze studentských poznámek"
        „Entropie je zdola omezená délkou zprávy" je **NEPRAVDIVÉ**. Minimum je $H = 0$, ne délka zprávy.

    *→ Skripta: [8.3 – Entropie](skripta/08-bezpecnost.md#entropie)*

---

**Jaká bude vzdálenost jednoznačnosti pro AES-192, kódování UTF-32?**

??? success "Odpověď"
    - $H(K) = 192$ b
    - $R = 32$ b, $r \approx 1{,}5$ b → $D = 30{,}5$
    - $\delta_U = 192 / 30{,}5 \approx \mathbf{6{,}3}$ znaků

    *→ Skripta: [8.3 – Vzdálenost jednoznačnosti](skripta/08-bezpecnost.md#vzdalenost-jednoznacnosti)*

---

**Spočtěte entropii RNG s pravděpodobnostmi:**
P(000) = 1/2, P(001) = 1/4, P(010) = 1/8, P(011) = 1/16, P(100) = 1/16, ostatní = 0

??? success "Odpověď"
    $$H = \tfrac{1}{2}{\cdot}1 + \tfrac{1}{4}{\cdot}2 + \tfrac{1}{8}{\cdot}3 + \tfrac{1}{16}{\cdot}4 + \tfrac{1}{16}{\cdot}4 = 0{,}5 + 0{,}5 + 0{,}375 + 0{,}25 + 0{,}25 = \mathbf{1{,}875 \text{ b}}$$

    *→ Skripta: [8.3 – Entropie](skripta/08-bezpecnost.md#entropie)*

---

**Šifra má entropii klíče 1200 bitů. Znak jazyka je kódován 19 bity. Zpráva má 80 znaků a ŠT je přesně tak dlouhý, že je na základě OT možný pouze jeden OT (unicity distance). Jaká je obsažnost tohoto jazyka na 1 písmeno?**

??? success "Odpověď"
    **Obsažnost jazyka: $r = 4$ bity/znak**

    1. Vzdálenost jednoznačnosti = délce zprávy: $\delta_U = 80$ znaků
    2. $\delta_U = H(K) / D \implies D = 1200 / 80 = 15$ b/znak
    3. Maximální entropie znaku: $R = 19$ b/znak (19bitové kódování → $2^{19}$ možných symbolů)
    4. Redundance: $D = R - r \implies r = R - D = 19 - 15 = \mathbf{4}$ b/znak

    *→ Skripta: [8.3 – Vzdálenost jednoznačnosti](skripta/08-bezpecnost.md#vzdalenost-jednoznacnosti)*

---

**Generátor RNG generuje: řetězec 000 s $P = \frac{1}{4}$, řetězec 001 s $P = \frac{1}{4}$, ostatních 6 řetězců každý s $P = \frac{1}{12}$. Spočtěte entropii tohoto zdroje.**

??? success "Odpověď"
    $$H = -2 \cdot \tfrac{1}{4} \log_2 \tfrac{1}{4} - 6 \cdot \tfrac{1}{12} \log_2 \tfrac{1}{12}$$

    $$= 2 \cdot \tfrac{1}{4} \cdot 2 + 6 \cdot \tfrac{1}{12} \cdot \log_2 12 = 1 + \tfrac{1}{2}(2 + \log_2 3) \approx 1 + \tfrac{1}{2} \cdot 3{,}585 \approx \mathbf{2{,}79 \text{ b}}$$

    Kontrola: $2 \cdot \tfrac{1}{4} + 6 \cdot \tfrac{1}{12} = \tfrac{1}{2} + \tfrac{1}{2} = 1$ ✓

    *→ Skripta: [8.3 – Entropie](skripta/08-bezpecnost.md#entropie)*

---

**Generátor RNG (3bitové řetězce: P(000) = P(001) = 1/4, ostatní 6 řetězců každý P = 1/12) vstupuje do SHA-256. TRNG generuje 127 bitů. Oba výstupy jsou spojeny (concat) a předány SHA-1. Doplňte schéma – počty bitů a entropie na každém místě:**

```
TRNG  →  127 b  →─────────────────────────────┐
                                               concat → ? b → SHA-1 → ? b
RNG   →    3 b  → SHA-256 → ? b  →────────────┘
```

??? success "Odpověď"

    | Místo | Počet bitů | Entropie |
    |-------|-----------|---------|
    | TRNG výstup | **127 b** | **127 b** (TRNG je skutečně náhodný) |
    | RNG výstup | **3 b** | **≈ 2,79 b** (viz výpočet výše) |
    | SHA-256 výstup | **256 b** | **≈ 2,79 b** |
    | concat výstup | **383 b** | **≈ 129,79 b** |
    | SHA-1 výstup | **160 b** | **≈ 129,79 b** |

    **Zdůvodnění:**

    - **SHA-256(RNG):** deterministická funkce nemůže zvýšit entropii; entropie výstupu = entropie vstupu = 2,79 b (i přesto, že výstup má 256 bitů)
    - **concat:** za předpokladu nezávislosti TRNG a RNG: $H = 127 + 2{,}79 = 129{,}79$ b
    - **SHA-1(concat):** výstup 160 b; entropie vstupu 129,79 b $<$ 160 b $\Rightarrow$ entropie se **zachová**: $H_{\text{out}} \approx 129{,}79$ b

    !!! tip "Klíčové pravidlo"
        Deterministická funkce (hash) **nemůže zvýšit entropii** vstupu; může ji nejvýše zachovat nebo snížit.

    *→ Skripta: [8.3 – Entropie](skripta/08-bezpecnost.md#entropie), [9.9 – BBS / PRNG](skripta/09-klice.md)*

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

    *→ Skripta: [9.8 – LCG](skripta/09-klice.md#98-pseudonahodne-generatory-prng)*

---

**LCG: $a=9$, $c=5$, $m=32$. První vygenerovaná hodnota je 20. Jaký byl seed? Je perioda generátoru maximální?**

??? success "Odpověď"
    **Seed:**
    $20 = (9s + 5) \bmod 32 \implies 9s \equiv 15 \pmod{32}$

    $9^{-1} \bmod 32 = 25$ (ověř: $9 \cdot 25 = 225 = 7{\cdot}32 + 1$ ✓)

    $s = 25 \cdot 15 \bmod 32 = 375 \bmod 32 = \mathbf{23}$

    **Perioda je maximální** ($= 32$): $\gcd(5,32)=1$ ✓, $2\mid(a-1)=8$ ✓, $4\mid(a-1)=8$ ✓

    *→ Skripta: [9.8 – LCG](skripta/09-klice.md#98-pseudonahodne-generatory-prng)*

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

    *→ Skripta: [9.9 – BBS](skripta/09-klice.md#99-blum-blum-shub-bbs)*

---

**Rabin-Miller test: $p = 13$, $a = 2$. Napiš rozklad $p-1$ ve tvaru $2^b \cdot m$.**

??? success "Odpověď"
    $p - 1 = 12 = 2^2 \cdot 3 \implies b = 2,\; m = 3$ (liché) ✓

    *→ Skripta: [9.6 – Testy prvočíselnosti](skripta/09-klice.md#96-testy-prvociselnosti)*

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

    *→ Skripta: [9.10 – TRNG](skripta/09-klice.md#910-skutecne-nahodne-generatory-trng)*

---

**Vyberte pravdivá tvrzení o generátoru Blum-Blum-Shub (BBS):**

1. Pokud známe prvních $k$ bitů, neexistuje algoritmus s polynomiální složitostí, který by dokázal předpovědět $(k+1)$. bit s pravděpodobností $> \frac{1}{2}$.
2. Algoritmus má periodu $+\infty$.
3. Díky tomu, že je kryptograficky bezpečný, nevyžaduje počáteční seed.
4. Čísla se musí generovat sekvenčně (nelze přeskočit na $k$-tý prvek).

??? success "Odpověď"
    ✅ **(1)**

    - (1) ✓ – **next-bit security**: za předpokladu těžkosti faktorizace $m = p \cdot q$ je BBS next-bit bezpečný
    - (2) ✗ – perioda je **konečná** a závisí na volbě $m$
    - (3) ✗ – BBS **vždy vyžaduje seed** $x_0$; kryptografická bezpečnost nesouvisí s potřebou seedu
    - (4) ✗ – $k$-tý prvek lze vypočítat přímo jako $x_k = x_0^{2^k} \bmod m$ pomocí rychlého umocňování

    *→ Skripta: [9.9 – BBS](skripta/09-klice.md#99-blum-blum-shub-bbs)*

---

**BBS generátor: $m = 77$, seed $= 11$. Z každého vygenerovaného čísla vybereme 3. LSB (bit na pozici 2). Jaká bude výsledná sekvence po 8 iteracích? Je generátor kryptograficky bezpečný?**

??? success "Odpověď"
    Výpočet ($x_{i+1} = x_i^2 \bmod 77$, start $x_0 = 11$):

    | $i$ | $x_i$ | binárně | bit 2 |
    |-----|--------|---------|-------|
    | 1 | 44 | `00101100` | **1** |
    | 2 | 11 | `00001011` | **0** |
    | 3 | 44 | `00101100` | **1** |
    | 4 | 11 | `00001011` | **0** |
    | 5 | 44 | `00101100` | **1** |
    | 6 | 11 | `00001011` | **0** |
    | 7 | 44 | `00101100` | **1** |
    | 8 | 11 | `00001011` | **0** |

    Sekvence: **`10101010`**

    **Kryptograficky bezpečná: NE.** Generátor okamžitě vstoupí do cyklu délky 2 ($11 \leftrightarrow 44$); výstup je čistě periodický → porušení next-bit testu.

    *→ Skripta: [9.9 – BBS](skripta/09-klice.md#99-blum-blum-shub-bbs)*

---

**Navrhněte pseudonáhodný generátor čísel s pomocí blokové šifry AES. Popište jeho vlastnosti.**

??? success "Odpověď"
    **AES-CTR PRNG** (standard NIST SP 800-90A: AES-CTR-DRBG):

    $$x_i = \text{AES}_K(\text{nonce} \| i), \quad i = 0, 1, 2, \ldots$$

    Alternativně **AES v OFB módu**: $x_{i+1} = \text{AES}_K(x_i)$

    **Vlastnosti:**

    - Kryptograficky bezpečný (za předpokladu bezpečnosti AES a tajnosti $K$)
    - Deterministický (DPRNG) – stejný klíč + nonce → stejná sekvence
    - Obrovská perioda ($2^{128}$ pro AES-128 v CTR)
    - Rychlý – využívá HW akceleraci AES
    - Vyžaduje bezpečně vygenerovaný klíč $K$ (z TRNG)
    - **Nonce se nesmí opakovat** se stejným klíčem!

    *→ Skripta: [9.8 – PRNG](skripta/09-klice.md#98-pseudonahodne-generatory-prng)*

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

    *→ Skripta: [10.1 – Distribuce veřejných klíčů](skripta/10-pki.md#101-distribuce-verejnych-klicu)*

---

## PKI a certifikáty

**Certifikační autorita (CA) je ___, která ___. Ověření certifikátu pomocí ___.**

??? success "Odpověď"
    CA = **důvěryhodná třetí strana**, která **vydává a aktualizuje certifikáty**.

    Ověření: pomocí **veřejného klíče CA** ($VK_{\text{CA}}$).

    *→ Skripta: [10.1 – Distribuce veřejných klíčů](skripta/10-pki.md#101-distribuce-verejnych-klicu)*

---

**Jaké jsou 3 nepostradatelné složky certifikátu?**

??? success "Odpověď"
    1. Identifikátor certifikovaného subjektu
    2. Veřejný klíč certifikovaného subjektu
    3. Doba platnosti certifikátu

    *→ Skripta: [10.2 – Formáty certifikátů X.509](skripta/10-pki.md#102-formaty-certifikatu-podle-x509)*

---

**Pokud chceme HMAC pro autentizaci původu dat, musíme zajistit:**

1. Zřídit veřejné klíče $VK_x$ a $VK_y$
2. Zřídit společný tajný klíč $K$
3. Nemusíme zajistit žádný klíč
4. HMAC pro tento problém nelze využít

??? success "Odpověď"
    ✅ **(2)** Zřídit společný tajný klíč $K$.

    *→ Skripta: [4.7 – HMAC](skripta/04-hash.md#47-hmac)*

---

**Model bezpečnosti OSI zahrnuje ___ bezpečnosti, ___ bezpečnosti a ___ bezpečnost.**

??? success "Odpověď"
    **Služby** bezpečnosti · **Mechanismy** bezpečnosti · **Útoky na** bezpečnost

    *→ Skripta: [8.2 – Typy bezpečnosti](skripta/08-bezpecnost.md#82-typy-bezpecnosti)*

---

**Jaké jsou 2 hlavní faktory rizika v informační bezpečnosti?**

??? success "Odpověď"
    1. Pravděpodobnost vzniku incidentu informační bezpečnosti
    2. Dopad incidentu

    *→ Skripta: [8.2 – Typy bezpečnosti](skripta/08-bezpecnost.md#82-typy-bezpecnosti)*

---

**Vyjmenuj 5 kategorií služeb bezpečnosti dle ISO.**

??? success "Odpověď"
    1. Autentizace
    2. Řízení přístupu
    3. Zabezpečení důvěrnosti dat
    4. Zabezpečení integrity dat
    5. Ochrana proti odmítnutí původu dat (nepopiratelnost)

    *→ Skripta: [8.2 – Typy bezpečnosti](skripta/08-bezpecnost.md#82-typy-bezpecnosti)*

---

**Vygeneruješ si VK a SK pomocí RSA. Lze (bez újmy na bezpečnosti) zaměnit soukromý a veřejný klíč předtím, než kterýkoli klíč zveřejníš?**

??? success "Odpověď"
    **Matematicky ANO** – RSA je symetrické v obou směrech:

    $$c = m^e \bmod n,\quad m = c^d \bmod n \quad \Leftrightarrow \quad c = m^d \bmod n,\quad m = c^e \bmod n$$

    Toto je základ **digitálního podpisu** (podepisujeme soukromým klíčem, ověřujeme veřejným).

    **Prakticky NE** – ze dvou důvodů:

    1. Znalost $d$ a $n$ umožňuje s vysokou pravděpodobností **faktorizovat $n$** → $d$ nelze zveřejnit
    2. $e$ je standardně malé číslo (65537) kvůli efektivitě šifrování; zveřejnění velkého $d$ jako „VK" by bylo velmi pomalé

    *→ Skripta: [5.4 – RSA](skripta/05-asymetricka.md#54-rsa)*

---

**Výpis RSA z OpenSSL obsahuje: `publicExponent` ($e$), `privateExponent` ($d$), `prime1` ($p$), `prime2` ($q$), `exponent1` ($d_p$), `exponent2` ($d_q$), `coefficient` ($q_{\text{inv}}$). Určete:**

1. Co je potřeba pro šifrování / dešifrování.
2. Co je potřeba pro dešifrování pomocí RSA-CRT.
3. Je potřeba pro 2025bitový modul použít prvočísla délky $45 \times 45$ bitů?

??? success "Odpověď"
    **Šifrování:** $(n,\, e)$ – `publicExponent` + $n$ (= `prime1` × `prime2`)

    **Dešifrování (standardní):** $(n,\, d)$ – `privateExponent`

    **Dešifrování (RSA-CRT):** `prime1` ($p$), `prime2` ($q$), `exponent1` ($d_p$), `exponent2` ($d_q$), `coefficient` ($q_{\text{inv}}$)

    **Pro 2025bitový modul, prvočísla délky $45 \times 45$ bitů:**
    ✗ **NE.** Pro $|n| \approx 2025$ bitů potřebujeme dvě prvočísla přibližně **poloviční délky** ($p \approx q \approx 1012$ bitů).

    !!! warning "Pozor"
        $45 \times 45 = 2025$ je $45^2$, ale délka modulu ≈ délka($p$) + délka($q$); dvě 45bitová prvočísla dávají ~90bitový modul, nikoli 2025bitový!

    *→ Skripta: [5.4 – RSA](skripta/05-asymetricka.md#54-rsa), [5.5 – RSA-CRT](skripta/05-asymetricka.md#55-rsa-crt)*

---

**Proč musí mít výstupní buffer funkce `EVP_EncryptUpdate` velikost $n + \text{block\_size} - 1$, pokud vstupní buffer má velikost $n$? Ukažte na jednoduchém příkladu.**

??? success "Odpověď"
    **Důvod:** `EVP_EncryptUpdate` drží **interní buffer** pro neúplné bloky. Pokud v bufferu zbývalo z předchozího volání až $\text{block\_size} - 1$ bajtů, přidání $n$ nových bajtů může vyvolat výstup až $n + \text{block\_size} - 1$ bajtů.

    **Příklad** (AES-128, `block_size = 16`):

    - Interní buffer po předchozím volání: **15 bajtů**
    - Nové volání přidá: **1 bajt**
    - Interní buffer nyní: $15 + 1 = 16$ bajtů → celý blok se zpracuje → výstup = **16 bajtů**
    - Kontrola: $n + \text{block\_size} - 1 = 1 + 16 - 1 = 16$ ✓

    *→ Skripta: [3.5 – AES](skripta/03-blokove.md)*

---

**Certifikáty: CA1 je kořenová CA, CA2 vydává certifikáty uživatelům. Popište postup vydání certifikátu pro Alici. Popište obsah certifikátů a řetězec potřebný pro validaci.**

??? success "Odpověď"
    **Postup vydání:**

    1. Alice vygeneruje pár klíčů $(VK_A, SK_A)$
    2. Alice vytvoří **CSR** (Certificate Signing Request): obsahuje $VK_A$, identitu, podpis $SK_A$
    3. CA2 ověří identitu Alice a podepíše CSR svým $SK_{CA2}$ → vznikne certifikát $C_A$

    **Obsah certifikátů:**

    | Certifikát | Vydavatel | Předmět | Podpis |
    |------------|-----------|---------|--------|
    | $C_A$ | CA2 | Alice + $VK_A$ + doba platnosti | $SK_{CA2}$ |
    | $C_{CA2}$ | CA1 | CA2 + $VK_{CA2}$ + doba platnosti | $SK_{CA1}$ |
    | $C_{CA1}$ | CA1 (self-signed) | CA1 + $VK_{CA1}$ | $SK_{CA1}$ |

    **Řetězec validace:**

    $$C_A \xrightarrow{\text{ověř } VK_{CA2}} C_{CA2} \xrightarrow{\text{ověř } VK_{CA1}} C_{CA1} \text{ (důvěryhodný kořen, předinstalovaný)}$$

    *→ Skripta: [10.2 – Formáty certifikátů X.509](skripta/10-pki.md#102-formaty-certifikatu-podle-x509)*

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

    *→ Skripta: [9.6 – Testy prvočíselnosti](skripta/09-klice.md#96-testy-prvociselnosti)*

---

**Popište mód CTR (Counter) – princip, vlastnosti, šifrování i dešifrování.**

??? success "Odpověď"
    $$C_i = E_K(\text{nonce} \| i) \oplus P_i \qquad P_i = E_K(\text{nonce} \| i) \oplus C_i$$

    - Převádí blokovou šifru na **synchronní proudovou šifru**
    - Plně **paralelizovatelný** v obou směrech
    - Umožňuje **náhodný přístup** k blokům
    - Porucha 1 bitu ŠT → porucha právě 1 bitu OT
    - Nonce se **nesmí opakovat** se stejným klíčem

    *→ Skripta: [3.6 – Provozní módy](skripta/03-blokove.md#36-provozni-mody-blokovych-sifer)*

---

**RSA-CRT: $p = 13$, $q = 23$, $e = 137$. Spočtěte hodnoty soukromého klíče.**

??? success "Odpověď"
    **Krok 1: Parametry RSA**

    - $n = p \cdot q = 13 \cdot 23 = 299$
    - $\varphi(n) = (p-1)(q-1) = 12 \cdot 22 = 264$

    **Krok 2: Soukromý exponent** $d = e^{-1} \bmod \varphi(n) = 137^{-1} \bmod 264$

    Rozšířený Eukleidův algoritmus:

    ```
    264 = 1·137 + 127
    137 = 1·127 + 10
    127 = 12·10 + 7
    10  = 1·7   + 3
    7   = 2·3   + 1
    → zpětná substituce: 1 = 41·264 − 79·137
    ```

    $d = -79 \bmod 264 = \mathbf{185}$ (ověř: $137 \cdot 185 = 25345 = 96 \cdot 264 + 1$ ✓)

    **Krok 3: RSA-CRT parametry**

    $$d_p = d \bmod (p-1) = 185 \bmod 12 = \mathbf{5}$$
    $$d_q = d \bmod (q-1) = 185 \bmod 22 = \mathbf{9}$$
    $$q_{\text{inv}} = q^{-1} \bmod p = 23^{-1} \bmod 13 = 10^{-1} \bmod 13 = \mathbf{4}$$
    (ověř: $10 \cdot 4 = 40 = 3 \cdot 13 + 1$ ✓)

    **Soukromý klíč RSA-CRT:** $(p=13,\ q=23,\ d_p=5,\ d_q=9,\ q_{\text{inv}}=4)$

    *→ Skripta: [5.5 – RSA-CRT](skripta/05-asymetricka.md#55-rsa-crt)*
