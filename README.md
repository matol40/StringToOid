# StringToOid

Detta GitHub-projekt är ett sätt att distribuera biblioteket **StringToOid** (ibo-oid) till användare och externa parter som inte sitter på eller har åtkomst till VGR:s interna nätverk (VGR-nät).

Biblioteket används för att automatiskt tolka och validera OID (Object Identifier) från en personidentitet (t.ex. personnummer, samordningsnummer eller reservnummer).

## Vad är OID och varför behövs det?

**OID (Object Identifier)** är en global standard för att unikt identifiera objekt, kodverk och terminologier i informationssystem och ange vem som ansvarar för dem (t.ex. Skatteverket, Inera eller VGR).

### Varför behövs det?
När man anropar VGR:s och Ineras personuppgiftstjänster (PU-tjänster) räcker det inte att enbart skicka personens identitet som en sträng. Tjänsterna kräver att identiteten specificeras med både:
* **`<root>` (OID):** Anger vilket typ av nummer det är och vem som utfärdat det.
* **`<extension>` (ID-sträng):** Själva personidentiteten (t.ex. `191212121212`).

Exempel på hur en identitet representeras i PU-anrop (t.ex. i `GetPersonsForProfile`):
```xml
<urn2:root>1.2.752.129.2.1.3.1</urn2:root>
<urn2:extension>191212121212</urn2:extension>
```

### Hur fungerar biblioteket?
Man skickar in identiteten som en vanlig sträng (t.ex. `"191212121212"`). Biblioteket analyserar strängens uppbyggnad, kontrollerar format och validerar kontrollsiffra (Luhn) och returnerar motsvarande OID. Med både OID och ID-strängen till hands kan anropande system enkelt sätta ihop korrekta förfrågningar mot PU-tjänsterna.

#### OID:ar som stöds

| Huvudman | Beskrivning | Kortnamn | OID (`root`) |
| :--- | :--- | :--- | :--- |
| Skatteverket | Svenskt personnummer | PNR | `1.2.752.129.2.1.3.1` |
| Skatteverket | Samordningsnummer | SNR | `1.2.752.129.2.1.3.3` |
| Inera | Nationell reservidentitet | NRID | `1.2.752.74.9.1` |
| VGR, Inera | Lokal reservidentitet | LRID | `1.2.752.113.11.0.2.1.1.1` |
| VGR, Inera | Lokal reservidentitet (gammalt format) | GRID | `1.2.752.113.11.0.2.1.1.4` |
| - | Ogiltig / okänd identitet | INVALID | - |

## Kom igång

1. Ladda ner distributionspaketet direkt här: [`ibo-oid-1.0.1-dist.zip`](https://github.com/matol40/StringToOid/raw/refs/heads/main/ibo-oid-1.0.1-dist.zip).
2. Packa upp zip-filen.
3. Öppna filen `index.html` (som finns i roten av den upppackade zip-filen) i en webbläsare för alla detaljer, instruktioner, kodexempel och fördjupad information.

> **Notera:** För parter med åtkomst till VGR:s interna nätverk finns biblioteket även att ladda ner via VGR Nexus:  
> [https://nexus.vgregion.se/nexus/repository/releases/se/vgregion/ibo/ibo-oid/1.0.1/ibo-oid-1.0.1-dist.zip](https://nexus.vgregion.se/nexus/repository/releases/se/vgregion/ibo/ibo-oid/1.0.1/ibo-oid-1.0.1-dist.zip)

## Innehåll

Distributionspaketet innehåller bibliotek och verktyg för både Java och .NET:
* **Java:** `lib/ibo-oid-1.0.1.jar` (kräver minst Java 8; inkluderar även ett CLI-verktyg för att validera CSV-filer mot OID).
* **.NET:** `lib/StringToOID.dll` (kräver minst .NET Standard 2.0).
* **Dokumentation:** Fullständig HTML-dokumentation och källkodsvisning.