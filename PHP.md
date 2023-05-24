# PHP

- [PHP](#php)
  - [ÚVOD](#úvod)
  - [ZÁKLADY](#základy)
    - [Základní příkazy](#základní-příkazy)
    - [Definice prvků](#definice-prvků)
  - [HTTP POŽADAVKY](#http-požadavky)
    - [Metoda](#metoda)
    - [URL](#url)
    - [Hlavičky](#hlavičky)
  - [API](#api)
  - [ŘETĚZCE](#řetězce)
    - [funkce pro práci s řetězci](#funkce-pro-práci-s-řetězci)
  - [POLE](#pole)
    - [Indexové](#indexové)
    - [Asociativní](#asociativní)
    - [Funkce pro práci s poli](#funkce-pro-práci-s-poli)
  - [FUNKCE](#funkce)
  - [TŘÍDY](#třídy)
  - [SESSION](#session)
    - [základní práce](#základní-práce)
    - [práce s daty](#práce-s-daty)
  - [COOKIES](#cookies)
    - [základní práce](#základní-práce-1)
    - [pokročilé práce](#pokročilé-práce)

## ÚVOD
> PHP probíhá na straně serveru
>
> Slouží k propojení webu s databází

## ZÁKLADY
**Vloženi PHP kódu do HTML**

```php
<?php
    //kód
?>
```

### Základní příkazy
>není case-sensitive

`echo` - výpis na obrazovku

`if` - podmínka

`while, for` - cykly

### Definice prvků
>je case-sensitive

`$prom` - proměnná (není nutné deklarovat dat. typ, case-se)

`$array = array("apple", "Karel", "Minecraft")` - pole

`$string = "nějaký text"` - řetězec

`function nazev_funkce()` - funkce

`class nazev_tridy` . třída
<br>

## HTTP POŽADAVKY

slouží k komunikaci mezi klientem a serverem

>- Metoda - udává co s objektem provést na serveru
>
>- URL - jednoznačně určuje požadovaný objekt na serveru
>
>- Hlavičky(headers) - přenáší části HTTP, odpovědi a různé další informace
>
>- Tělo požadavku - obsahuje data poslaná na server

---

### Metoda

`$_GET` - získává informace ze serveru

`$_POST` - posílá data na server

`$_DELETE` - maže data ze serveru

`$_PUT` - aktualizuje data na serveru

<br>

**Ukázky kódu**

---

### URL

|Funkce|Popis|
|:---:|:---:|
|parse_url()|rozdělí URL na části|
|http_build_query()|vytvoří řetězec s parametry pro GET|
|$_GET[]| parametry předané v URL po otazníku|
|urlencode() / rawurlencode()|zakóduje řetězec pro použití v URL|
|$_SERVER['REQUEST_URI']|obsahuje cestu k aktuálnímu skriptu|

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

### Hlavičky

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

## API

> API (Application Programming Interface) je sada definovaných funkcí, protokolů a nástrojů, které umožňují komunikaci a interakci mezi různými softwarovými aplikacemi.
> 
> API může být ve formě webového rozhraní (například RESTful API), knihoven nebo sady příkazů a funkcí, které jsou poskytovány programovacím jazykem. API poskytuje definované metody pro získávání, manipulaci a správu dat nebo služeb.
>
> API je důležité pro vývoj webových aplikací, mobilních aplikací, integrace s externími službami a mnoho dalších případů, kdy je potřeba propojit a interoperabilita mezi různými systémy.

**Ukázka kódu**

```php
// Nastavení URL koncového bodu API
$apiUrl = 'https://api.example.com/data';

// Vytvoření HTTP požadavku
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, $apiUrl);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

// Volitelné: Nastavení parametrů požadavku (např. GET parametry, hlavičky apod.)
curl_setopt($ch, CURLOPT_HTTPHEADER, [
    'Authorization: Bearer YOUR_API_KEY',
]);

// Odeslání požadavku na API a získání odpovědi
$response = curl_exec($ch);

// Kontrola úspěšnosti požadavku
if ($response === false) {
    die('Chyba při komunikaci s API: ' . curl_error($ch));
}

// Zpracování odpovědi
$data = json_decode($response, true);

// Kontrola úspěšného získání dat
if (is_array($data)) {
    // Data byla úspěšně získána, můžete s nimi dále pracovat
    // ...
} else {
    // Chyba při zpracování odpovědi API
    // ...
}

// Uzavření HTTP spojení
curl_close($ch);
```

## ŘETĚZCE
> Používají se jednoduché nebo dvojité uvozovky
> Možne kombinovat s jinými dat. typy pomocí `.`

```php
$num = 123;
$string = "Číslo je:" . $num;
```
### funkce pro práci s řetězci

|Funkce|Popis|
|:---:|:---:|
|strlen($str)|délka řetězce|
|trim($str)|odstraní bílé znaky|
|htmlspecialchars()|konvertuje speciální znaky HTML (zabraňuje XSS útokům)|
|strtlower($str)|převede na malé písmena|
|ucfirst($str)|převede první písmeno na velké|
|ucwords($str)|převede první písmena všech slov na velké|

## POLE
>Může být indexové nebo asociativní

### Indexové
>použíté jsou celočíselné hodnoty
>nulové indexováním (začíná 0)

`$pole[0] $pole[5]` - k přístupu k datům se používají indexy

### Asociativní
>umožňuje přiřazení klíče, obvykle se jedná o řetězce, ale můžou to být i jiné dat. typy
>ukládají se data s názvem (např. jméno, druh, pozice)
>k hodnotě se přistupuje podle daného klíče

`$pole[klic]`

**Tvorba asociativního pole**
```php
$asociativni_pole = array
(
  "key1" => "hodnota1"
  "key2" => "hodnota2"
  "key3" => "hodnota3"
);
```

### Funkce pro práci s poli

|Funkce|Popis|
|:---:|:---:|
|count()|počet prvků|
|array_push() |nová hodnota na konci pole|
|array_unshift()|nová hodnota na začátek pole|
|array_merge()|spojí pole|

## FUNKCE

>vestavěné nebo uživatelské
>využívá se, když se část kódu opakovaně vyskytuje

*definování funkce*
```php
function nazev_funkce()
{
  //kód
  return;
}

function parametr($a)
{
  //kód
  return
}

parametr("něco");
```

## TŘÍDY

## SESSION

`$_SESSION` - superglobální proměnná

### základní práce

`session_start` - vytvoří session

`session_abort` - zrušení session

`session_destroy` - zruší session a odstraní data z ní

`session_restart` - obnoví session

`session_name` - pojmenuje session

### práce s daty

`session_status` - vrací hodnoty

`session_unset` - uvolní proměnné

`session_write_close` - zapíše hodnoty a ukončí session

## COOKIES

Slouží k ukládání informací o uživateli z předchozích interakcí. Udrží uživatele přihlášeno, sledují návštěvnost, personalizují obsah atd.

Cookies jsou přenášeny pomocí hlaviček.

### základní práce

`setcookie(name, value, expire, path, domain, secure, httponly)` - funkce pro vytvoření cookie s danými parametry, které nejsou povinné
`$_COOKIE[prom]` - přístup k hodnotě cookie s daným názvem

`isset($_COOKIE[prom])` - ověření zda existuje

`unset($_COOKIE[name])` - zrušení cookie

### pokročilé práce

`time()` - služí k určení expirace

`urlencode() / urldecode()` - kódování a dekódování cookies