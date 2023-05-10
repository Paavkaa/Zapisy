# PHP

- [PHP](#php)
  - [Úvod](#úvod)
  - [Základy](#základy)
    - [Základní příkazy](#základní-příkazy)
  - [HTTP požadavky](#http-požadavky)
      - [**Metoda**](#metoda)
      - [**URL**](#url)
      - [**Hlavičky**](#hlavičky)
  - [SESSION](#session)
  - [COOKIES](#cookies)

## Úvod
> PHP probíhá na straně serveru
>
> Slouží k propojení webu s databází
> 
> Syntaxe velmi podobna jazyku C

## Základy
**Vloženi PHP kódu do HTML**

```php
<?php
    //kód
?>
```

### Základní příkazy

`echo` - výpis na obrazovku

`if` - podmínka

`while, for` - cykly

`function nazev_funkce()` - funkce

`$prom` - proměnná (není nutné deklarovat dat. typ)

`$array = array("apple", "Karel", "Minecraft")` - pole

`$string = "nějaký text"` - řetězec

<br>

## HTTP požadavky

slouží k komunikaci mezi klientem a serverem

>- Metoda - udává co s objektem provést na serveru
>
>- URL - jednoznačně určuje požadovaný objekt na serveru
>
>- Hlavičky(headers) - přenáší části HTTP, odpovědi a různé další informace
>
>- Tělo požadavku - obsahuje data poslaná na server

---

#### **Metoda**

`$_GET` - získává informace ze serveru

`$_POST` - posílá data na server

`$_DELETE` - maže data ze serveru

`$_PUT` - aktualizuje data na serveru

<br>

**Ukázky kódu**

---

#### **URL**

`parse_url()` - rozdělí URL na jednotlivé části (protokol, doménu, cestu, atd.), které vrátí v poli

`urlencode()` - zakóduje řetězec pro použití v URL, nahradí
 speciální znaky přepíše na hexadecimální

`http_build_query()` - vytvoří řetězec s parametry pro GET na základě asociativného pole

`$_GET[]` - parametry předané v URL po otazníku (např. ?parametr=hodnota)

`$_SERVER['REQUEST_URI']` - obsahuje cestu k aktuálnímu skriptu

`rawurlencode()` - zákoduje string pro URL, ale zachová důležité speciální znaky

`basename()` - vrátí název souboru/adresáře z dané cesty

`dirname()` - vrátí adresář z dané cesty

<br>

**Ukázky kódu**

URL: https://www.example.com/products.php?id=123&category=books

*získání parametru z url*

```php
$id = $_GET['id'];
$category = $_GET['category'];
```

>**$_GET** - bere informace z URL
>
> https://www.example.com/products.php?<mark style="background: lightblue;"> id=123</mark>&category=books
>
> **$_GET['id']** - bere informace ze zvýrazněné části adresy

*přesměrování*
```php
$new_url = "https://www.example.com/new-page.php";
header("Location: $new_url");
//nebo
header("Location: https://www.example.com/new-page.php");
exit;
```
>**Location** - slouží k přesměrování

*získáni URL adresy*
```php
$url = "https://".$_SERVER['HTTP_HOST'].$_SERVER['REQUEST_URI'];
```
>**$_SERVER['HTTP_HOST']** - pole s názvem hostitelského serveru
>
>**$_SERVER['REQUEST_URI']** - pole obsahující řetězec parametrů GET

---

#### **Hlavičky**

`header()` - nastavuje hlavičku HTTP (např. přesměrování, nebo informace COOKIES)

`header_remove()` - odstraní hlavičku

`header_sent()` - kontroluje, zda byla hlavička poslána

`http_response_code()` - nastavuje status odpovědi na danou hodnotu

>**Content-type** - určuje typ obsahu (např. text, aplikace, obrázek)
>
>**Content-Lenght** - udává délku v bitech
>
>**Cache-Control** - určuje, jak má být obsah ukládán (mezipaměť pc atd.)
>
>**User-Agent** - má informace o prohlížeči nebo jiném klientovi, který posílá požadavek
>
>**Referer** - má URL adresu ze které byl požadavek odeslán
>
>**Accept** - určuje typ obsahu, který klient přijme (např. text, aplikace, obrázek)
>
>**Authorization** - ověřovací údaje (např. přihlašovací jméno a heslo)

<br>

 **Ukázky kódu**

*přesměrování pomocí header()*
```php
header("location: https://www.example.com/newpage.php");
exit();
```
>**location** - přesměruje na danou URL adresu

*nastavení hlavičky pro soubor ke stažení*
```php
header('Content-Disposition: attachment; filename="downloaded_file.pdf"');
readfile('path/to/file.pdf');
```
>**Content-Disposition** - ovlivňuje jak prohlížeč zobrazí soubor (inline - zobrazit, attachmnet - stáhnout)
>
>**filename** - název souboru

## SESSION
*základní práce*

`session_start` - vytvoří session

`session_abort` - zrušení session

`session_destroy` - zruší session a odstraní data z ní

`session_restart` - obnoví session

`session_name` - pojmenuje session

*práce s daty*

`session_status` - vrací hodnoty

`session_unset` - uvolní proměnné

`session_write_close` - zapíše hodnoty a ukončí session

## COOKIES

Slouží k ukládání informací o uživateli z předchozích interakcí. Udrží uživatele přihlášeno, sledují návštěvnost, personalizují obsah atd.

Cookies jsou přenášeny pomocí hlaviček
