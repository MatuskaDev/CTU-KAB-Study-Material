# 11. Čipové karty

---

## APDU – komunikace ISO 7816

### Formát příkazu a odpovědi

=== "Command APDU"
    ```
    CLA | INS | P1 | P2 | [Lc | DATA | Le]
    ```
    
    | Pole | Délka | Popis |
    |------|-------|-------|
    | CLA | 1 B | Třída instrukce |
    | INS | 1 B | Kód instrukce |
    | P1, P2 | 2 B | Parametry |
    | Lc | 0/1/3 B | Délka dat příkazu |
    | DATA | Lc B | Data příkazu |
    | Le | 0/1/3 B | Očekávaná délka odpovědi |

=== "Response APDU"
    ```
    [DATA] | SW1 | SW2
    ```
    
    | Status Word | Význam |
    |-------------|--------|
    | `90 00` | OK – úspěch |
    | `6A 82` | Soubor nenalezen |
    | `69 83` | Authentication method blocked |
    | `63 Cx` | Counter = x, operace selhala |

### Příklad – SELECT aplikace

```
00  A4  04  00  06  41 42 43 44 45 46
│   │   │   │   │   └── AID = ABCDEF (6 bytů)
│   │   │   │   └────── Lc = 6
│   │   │   └────────── P2 = 00
│   │   └────────────── P1 = 04 (select by name)
│   └────────────────── INS = A4 (SELECT)
└────────────────────── CLA = 00
```

---

## Souborový systém ISO 7816-4

```mermaid
flowchart TD
    MF["MF – Master File\nFID: 3F00\n(kořen)"]
    MF --> DF1["DF – Dedicated File\n(adresář/aplikace)"]
    MF --> DF2["DF – Dedicated File"]
    DF1 --> EF1["EF – Elementary File\n(transparentní data)"]
    DF1 --> EF2["EF – Elementary File\n(záznamy)"]
    DF2 --> EF3["EF"]
```

### Typy Elementary Files

| Typ | Popis |
|-----|-------|
| **Transparent** | Binární data, přístup přes offset + délka |
| **Linear Fixed** | Záznamy pevné délky |
| **Linear Variable** | Záznamy proměnné délky |
| **Cyclic** | Cyklický buffer záznamů |

---

## Secure Messaging

```mermaid
flowchart LR
    subgraph SecMsg["Secure Messaging"]
        CMD["Příkaz"] --> MAC_C["Výpočet MAC\n(HMAC / CBC-MAC)"]
        CMD --> ENC_C["Šifrování dat\n(3DES / AES)"]
        MAC_C & ENC_C --> TLV["TLV struktura\n(Tag-Length-Value)"]
        TLV --> SEND["Odeslání APDU"]
    end
```

!!! info "TLV (Tag-Length-Value)"
    Každé datové pole je zakódováno jako:
    ```
    Tag (1-3 B) | Length (1-3 B) | Value (Length B)
    ```
    
    Příklad:
    ```
    87 11 01 <16 bytů šifrovaných dat>
    8E 08 <8 bytů MAC>
    ```

### Základní bezpečnostní funkce čipové karty

| Funkce | Popis |
|--------|-------|
| **PIN ověření** | Ochrana přístupu (blokace po N neúspěších) |
| **Secure Channel** | Šifrovaná + autentizovaná komunikace |
| **Key Diversification** | Unikátní klíče pro každou kartu |
| **Anti-tampering** | Fyzická ochrana (mesh, zener diody, senzory) |
