---
hide:
  - toc
---

# Přehled algoritmů

Kompaktní referenční tabulky pro rychlé opakování před zkouškou.

---

## Šifrovací algoritmy

| Algoritmus | Typ | Klíč | Blok | Kola | Základ bezpečnosti | Status |
|------------|-----|------|------|------|--------------------|--------|
| **Caesar** | Mono-alfa sub. | 5b (1–25) | 1 znak | – | Posun v abecedě | ❌ Triviální |
| **Afinní** | Mono-alfa sub. | $(a,b)$, 312 klíčů | 1 znak | – | Substituce | ❌ Trivální |
| **Vigenère** | Poly-alfa sub. | $V$ znaků | – | – | DLP abecedy | ❌ Kasiski/Friedman |
| **DES** | Bloková (Feistel) | 56b | 64b | 16 | S-boxy | ❌ Zastaralý |
| **3DES-EDE** | 3×DES | 112/168b | 64b | 48 | Faktorizace (eff.) | ⚠️ Deprecated |
| **AES-128** | Bloková (SP-síť) | 128b | 128b | 10 | AES bezp. | ✅ Bezpečný |
| **AES-192** | Bloková (SP-síť) | 192b | 128b | 12 | AES bezp. | ✅ Bezpečný |
| **AES-256** | Bloková (SP-síť) | 256b | 128b | 14 | AES bezp. | ✅ Bezpečný |
| **RC4** | Proudová (S-box) | 1–256B | – | – | S-box permutace | ❌ PROLOMEN |
| **ChaCha20** | Proudová (ARX) | 256b | – | 20 | ARX | ✅ Bezpečný |
| **Salsa20** | Proudová (ARX) | 256b | – | 20 | ARX | ✅ Bezpečný |
| **A5/1** | Proudová (LFSR) | 64b | – | – | LFSR | ❌ PROLOMEN 2009 |

---

## Provozní módy blokových šifer

| Mód | Randomizace | Paral. šif. | Paral. dešif. | Integrita | Chyba se šíří |
|-----|-------------|-------------|---------------|-----------|---------------|
| ECB | ❌ | ✅ | ✅ | ❌ | Ne |
| CBC | ✅ (IV) | ❌ | ✅ | ❌ | Ano (1 blok) |
| CFB | ✅ (IV) | ❌ | ✅ | ❌ | Ano |
| OFB | ✅ (IV) | ❌ | ❌ | ❌ | Ne |
| CTR | ✅ (nonce) | ✅ | ✅ | ❌ | Ne |
| **GCM** | ✅ | ✅ | ✅ | **✅ AEAD** | Ne |

---

## Hašovací funkce

| Funkce | Výstup | Blok | Kola | Kolize (teor.) | Status |
|--------|--------|------|------|----------------|--------|
| MD5 | 128b | 512b | 64 | $2^{18}$ | ❌ PROLOMEN |
| SHA-1 | 160b | 512b | 80 | $2^{63}$ | ❌ PROLOMEN 2017 |
| **SHA-256** | **256b** | **512b** | **64** | **$2^{128}$** | **✅** |
| SHA-512 | 512b | 1024b | 80 | $2^{256}$ | ✅ |
| SHA-3 (Keccak) | 224–512b | var. | 24 | $2^{n/2}$ | ✅ |

---

## Asymetrické algoritmy

| Algoritmus | Základ bezpečnosti | Klíč (128b sym.) | Použití | Ohrožen Shorem? |
|------------|--------------------|------------------|---------|-----------------|
| RSA | Faktorizace | 3072b | Šifrování, podpis | ✅ ANO |
| DH | DLP | 3072b | Výměna klíčů | ✅ ANO |
| ElGamal | DLP | 3072b | Šifrování, podpis | ✅ ANO |
| DSA | DLP | 3072/256b | Podpis | ✅ ANO |
| **ECDH** | ECDLP | **256b** | Výměna klíčů | ✅ ANO |
| **ECDSA** | ECDLP | **256b** | Podpis | ✅ ANO |
| **ML-KEM** | Lattice (Kyber) | 800–1568B | Výměna klíčů | ❌ NE ✅ |
| **ML-DSA** | Lattice (Dilithium) | var. | Podpis | ❌ NE ✅ |

---

## Délky klíčů — bezpečnostní ekvivalence

| Symetrická bezpečnost | AES | RSA/DH | ECC |
|-----------------------|-----|--------|-----|
| 80 bitů | 80b ⚠️ | 1024b ⚠️ | 160b ⚠️ |
| 112 bitů | 112b | 2048b | 224b |
| **128 bitů** | **128b** | **3072b** | **256b** |
| 192 bitů | 192b | 7680b | 384b |
| 256 bitů | 256b | 15360b | 521b |

---

## Vlastnosti hašovacích funkcí

| Vlastnost | Definice | Útok | Složitost |
|-----------|----------|------|-----------|
| Preimage resistance | Ze $h$ nelze najít $m$: $H(m)=h$ | Hrubá síla | $O(2^n)$ |
| 2nd preimage resistance | Ze $m$ nelze najít $m'\neq m$: $H(m')=H(m)$ | Hrubá síla | $O(2^n)$ |
| **Collision resistance** | Nelze najít libovolná $m\neq m'$ s kolizí | **Narozeninový paradox** | **$O(2^{n/2})$** |

---

## Klíčové formule — tahák

### Klasické šifry
$$c = (p+k) \bmod 26 \quad\text{(Caesar)}$$
$$c = (ap+b) \bmod 26, \;\gcd(a,26)=1 \quad\text{(Afinní)}$$
$$\vec{c} = K\vec{p} \bmod 26 \quad\text{(Hill)}$$

### RSA
$$c = m^e \bmod n \qquad m = c^d \bmod n \qquad ed \equiv 1 \pmod{\phi(n)}$$

### DH / ElGamal
$$A = g^a \bmod p, \quad B = g^b \bmod p, \quad K = A^b = B^a = g^{ab} \bmod p$$

### ECC sčítání bodů
$$s = \frac{y_Q-y_P}{x_Q-x_P} \bmod p \quad (P\neq Q), \qquad s = \frac{3x_P^2+a}{2y_P} \bmod p \quad (2P)$$
$$x_R = s^2 - x_P - x_Q \bmod p, \qquad y_R = s(x_P-x_R)-y_P \bmod p$$

### SHA-256
$$T_1 = h+\Sigma_1(e)+Ch(e,f,g)+K_t+W_t, \quad T_2 = \Sigma_0(a)+Maj(a,b,c)$$

### HMAC
$$\text{HMAC}_K(M) = H\!\bigl((K^+\!\oplus\text{opad}) \,\|\, H\!\bigl((K^+\!\oplus\text{ipad}) \,\|\, M\bigr)\bigr)$$

### Vzdálenost jednoznačnosti
$$\delta_U = \frac{H(K)}{D}, \quad D = R - r \quad\text{(redundance jazyka)}$$

### Rabin-Miller
$$p - 1 = 2^b \cdot m, \quad z = a^m \bmod p, \quad \text{chyba} \leq 4^{-t}$$

---

## Časová osa — kompromitované algoritmy

| Rok | Událost |
|-----|---------|
| 1997 | DES prolomen hrubou silou (Deep Crack, $22.5h) |
| 2001 | NIST vyhlásil AES (Rijndael) jako standard |
| 2004 | MD5 koli – Wang & Yu |
| 2005 | SHA-1 teoretická kolize – Wang |
| 2007 | RC4 zakázán pro nové systémy (IETF) |
| 2009 | A5/1 prolomen (Nohl, Rainbow tables FPGA) |
| 2012 | Sony PS3 exploit (DSA konstantní k) |
| 2015 | FREAK útok (export RSA 512b) |
| 2017 | SHA-1 collision (SHAttered — Google & CWI) |
| 2019 | RC4 zakázán v TLS (RFC 7465) |
| 2022 | 3DES deprecated NIST |
| 2024 | NIST vydal ML-KEM, ML-DSA (post-kvantové standardy) |
