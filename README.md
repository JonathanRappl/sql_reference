# Nordwind-Datenbank

## Beschreibung der Datenbank
Die *Nordwind-Datenbank* ist eine Beispiel-Datenbank, die mit Microsoft Access ausgeliefert wird. Sie zeigt, wie eine Firma ihre Bestellungen, Kunden und Lieferanten mit einer Datenbank verwalten kann.

## Entitätstypen (Datenbank-Tabellen)
Die Datenbank hat sieben wichtige Tabellen:

- **Lieferanten** verkaufen Artikel und sind bestimmten Kategorien zugeordnet.
- **Kunden** bestellen Artikel.
- **Bestellungen** werden von den Mitarbeitern der Firma bearbeitet.
- **Versandfirmen** liefern die Bestellungen aus.

## Beziehungen zwischen den Tabellen
- Ein **Lieferant** kann viele Artikel liefern, aber jeder Artikel kommt nur von einem Lieferanten.
- Eine **Kategorie** enthält viele Artikel, aber ein Artikel gehört nur zu einer Kategorie.
- Ein **Artikel** kann in mehreren Bestellungen vorkommen, und eine Bestellung kann mehrere Artikel enthalten (*n:m-Beziehung*).
- Ein **Kunde** kann mehrere Bestellungen aufgeben, aber jede Bestellung gehört nur einem Kunden.
- Ein **Mitarbeiter** bearbeitet mehrere Bestellungen, aber jede Bestellung wird nur von einem Mitarbeiter bearbeitet.
- Eine **Versandfirma** liefert mehrere Bestellungen aus, aber jede Bestellung wird nur von einer Versandfirma geliefert.

# Tabellenübersicht der Nordwind-Datenbank

## **Lieferant**  
| LieferantenNr | Firma | Kontaktperson | Position | Straße | Ort | Region | PLZ | Land | Telefon | Telefax | Homepage |
|--------------|-------|--------------|----------|--------|-----|--------|-----|------|---------|---------|----------|

## **Kunde**  
| KundenCode | Firma | Kontaktperson | Position | Straße | Ort | Region | PLZ | Land | Telefon | Telefax |
|------------|-------|--------------|----------|--------|-----|--------|-----|------|---------|---------|

## **Versandfirma**  
| FirmenNr | Firma | Telefon |
|----------|-------|---------|

## **Personal**  
| PersonalNr | Nachname | Vorname | Position | Anrede | Geburtsdatum | Einstellung | Straße | Ort | Region | PLZ | Land | TelefonPrivat | DurchwahlBüro | Bemerkungen | Vorgesetzter |
|------------|---------|--------|----------|-------|-------------|-------------|--------|-----|--------|-----|------|--------------|-------------|------------|-------------|

## **Kategorie**  
| KategorieNr | Kategoriename | Beschreibung |
|------------|--------------|--------------|

## **Artikel**  
| ArtikelNr | Artikelname | ↑LieferantenNr | ↑KategorieNr | Liefereinheit | Einzelpreis | Lagerbestand | BestellteEinheiten | Mindestbestand | Auslaufartikel |
|-----------|------------|---------------|--------------|--------------|------------|-------------|----------------|--------------|--------------|

## **Bestellung**  
| BestellNr | ↑KundenCode | ↑PersonalNr | Bestelldatum | Lieferdatum | Versanddatum | ↑FirmenNr | Frachtkosten | Empfänger | Straße | Ort | Region | PLZ | Bestimmungsland |
|----------|------------|------------|------------|------------|------------|----------|------------|----------|--------|-----|--------|-----|----------------|

## **Bestelldetails**  
| ↑BestellNr | ↑ArtikelNr | Einzelpreis | Anzahl | Rabatt |
|-----------|-----------|------------|--------|--------|
