# SQL Injection Write-up

## Zadání
Cílem bylo ověřit, jestli je vyhledávač na adrese `http://192.168.135.10:5000` zranitelný vůči SQL Injection, zjistit strukturu databáze a získat skrytou vlajku.

## 1. Průzkum
Nejdřív jsem testoval vstupní pole pomocí apostrofu `'`, abych zjistil, jestli aplikace správně ošetřuje vstup. Podle chování stránky bylo vidět, že aplikace není dostatečně zabezpečená a je možné do SQL dotazu zasahovat.

## 2. Zjištění struktury databáze
Potom jsem použil `UNION SELECT` a podařilo se mi vypsat názvy tabulek z databáze. Zobrazily se tabulky:

- `config`
- `users`

Z toho jsem usoudil, že tabulka `config` bude pravděpodobně obsahovat nějaké důležité nastavení nebo citlivé údaje.

## 3. Exfiltrace dat
Nakonec jsem použil tento payload:

```sql
' UNION SELECT 1, key || '=' || value FROM config-- -
