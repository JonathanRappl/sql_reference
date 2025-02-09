# SQL Grundlagen  

SQL (Structured Query Language) ist eine Sprache zur Verwaltung und Abfrage von Daten in relationalen Datenbanken.  

1. [Genereller Aufbau einer Query](#genereller-aufbau-einer-query)
2. [SELECT](#select)  
   - [Distinct](#distinct)  
   - [Berechnungen in SELECT](#berechnungen-in-select)  
   - [Aggregatfunktionen](#aggregatfunktionen)  
   - [AS (Alias)](#as-alias)  
3. [FROM](#from)  
   - [Inner Join](#inner-join)  
   - [GROUP BY](#group-by)  
4. [WHERE](#where)  
   - [Vergleichsoperatoren](#vergleichsoperatoren)  
   - [Logische Operatoren](#logische-operatoren)  
   - [BETWEEN](#between)  
   - [LIKE](#like)  
   - [IN](#in)  
5. [ORDER BY](#order-by)  
6. [LIMIT](#limit)  

## Genereller Aufbau einer Query  

Eine SQL-Abfrage besteht aus mehreren Teilen:  

```sql
SELECT spalten  
FROM tabelle  
WHERE bedingung  
GROUP BY spalte  
HAVING gruppenbedingung  
ORDER BY spalte  
LIMIT anzahl;
```

Jeder Teil der Query hat eine spezifische Aufgabe:  
- **SELECT** – Bestimmt, welche Spalten zurückgegeben werden  
- **FROM** – Gibt die Tabelle(n) an, aus denen Daten geholt werden  
- **WHERE** – Filtert die Ergebnisse nach bestimmten Bedingungen  
- **GROUP BY** – Gruppiert die Ergebnisse  
- **HAVING** – Filtert die Gruppen  
- **ORDER BY** – Sortiert die Ergebnisse  
- **LIMIT** – Begrenzung der Anzahl zurückgegebener Zeilen  

---

## SELECT  

Der `SELECT`-Befehl gibt Daten aus einer Tabelle zurück.  

### Distinct  

Mit `DISTINCT` können doppelte Werte entfernt werden:  

```sql
SELECT DISTINCT spalte FROM tabelle;
```

Gibt alle eindeutigen Werte aus der angegebenen Spalte zurück.  

### Berechnungen in SELECT  

SQL erlaubt Berechnungen direkt in der Abfrage:  

```sql
SELECT preis * 1.2 AS neuer_preis FROM produkte;
```

Hier wird der Preis um 20 % erhöht und als `neuer_preis` ausgegeben.  

### Aggregatfunktionen  

Aggregatfunktionen berechnen Werte über mehrere Zeilen hinweg:  

```sql
SELECT  
    SUM(preis) AS gesamtpreis,  
    COUNT(*) AS anzahl,  
    MIN(preis) AS niedrigster_preis,  
    MAX(preis) AS hoechster_preis,  
    AVG(preis) AS durchschnittspreis  
FROM produkte;
```

`SUM()`, `COUNT()`, `MIN()`, `MAX()`, `AVG()` werden oft mit `GROUP BY` verwendet.  

### AS (Alias)  

Mit `AS` können Spalten oder Berechnungen umbenannt werden:  

```sql
SELECT preis AS kosten FROM produkte;
```

`preis` wird als `kosten` in der Ausgabe angezeigt.  

---

## FROM  

Der `FROM`-Teil gibt an, aus welchen Tabellen die Daten stammen.  

### Inner Join  

Mit `INNER JOIN` werden zwei Tabellen über eine gemeinsame Spalte verknüpft:  

```sql
SELECT kunden.name, bestellungen.bestellnummer  
FROM kunden  
INNER JOIN bestellungen ON kunden.id = bestellungen.kunden_id;
```

Gibt alle Kunden und ihre Bestellnummern zurück.  

Wir können auch `WHERE` benutzen für das gleiche Resultat.

```sql
SELECT kunden.name, bestellungen.bestellnummer  
FROM kunden, bestellungen 
WHERE kunden.id = bestellungen.kunden_id;
```

### GROUP BY  

Mit `GROUP BY` können Zeilen gruppiert werden, um Aggregatfunktionen anzuwenden:  

```sql
SELECT kategorie, COUNT(*) AS anzahl  
FROM produkte  
GROUP BY kategorie;
```

Gibt die Anzahl der Produkte pro Kategorie aus.  

---

## WHERE  

Mit `WHERE` werden Zeilen gefiltert, die bestimmten Bedingungen entsprechen.  

### Vergleichsoperatoren  

- `=` (gleich)  
- `!=` oder `<>` (ungleich)  
- `>` (grösser als)  
- `<` (kleiner als)  
- `>=` (grösser gleich)  
- `<=` (kleiner gleich)  

```sql
SELECT * FROM produkte WHERE preis > 100;
```

Gibt alle Produkte mit einem Preis über 100 aus.  

### Logische Operatoren  

- `AND` – Beide Bedingungen müssen erfüllt sein  
- `OR` – Mindestens eine Bedingung muss erfüllt sein  
- `NOT` – Negiert eine Bedingung  

```sql
SELECT * FROM produkte WHERE preis > 50 AND lagerbestand > 0;
```

Gibt nur Produkte mit Preis > 50 UND Lagerbestand > 0 aus.  

### BETWEEN  

`BETWEEN` wird für Bereichsabfragen verwendet:  

```sql
SELECT * FROM produkte WHERE preis BETWEEN 50 AND 100;
```

Gibt alle Produkte mit einem Preis zwischen 50 und 100 aus.  

### LIKE  

Mit `LIKE` können Zeichenketten gesucht werden:  

```sql
SELECT * FROM kunden WHERE name LIKE 'M%';
```

Gibt alle Kunden zurück, deren Name mit "M" beginnt.  

Wildcards:  
- `%` – Beliebige Anzahl an Zeichen  
- `_` – Genau ein Zeichen  

### IN  

Mit `IN` können mehrere Werte geprüft werden:  

```sql
SELECT * FROM produkte WHERE kategorie IN ('Elektronik', 'Bücher', 'Kleidung');
```

Gibt alle Produkte zurück, die zu einer der angegebenen Kategorien gehören.  

---

## ORDER BY  

`ORDER BY` sortiert die Ergebnisse:  

```sql
SELECT * FROM produkte ORDER BY preis DESC;
```

Sortiert Produkte nach Preis absteigend (`DESC` für absteigend, `ASC` für aufsteigend).  

---

## LIMIT  

Mit `LIMIT` kann die Anzahl der zurückgegebenen Zeilen begrenzt werden:  

```sql
SELECT * FROM produkte LIMIT 10;
```

Gibt maximal 10 Produkte zurück.  

```sql
SELECT * FROM produkte LIMIT 10, 5;
```

Überspringt die ersten 10 Zeilen und gibt die nächsten 5 aus.  
