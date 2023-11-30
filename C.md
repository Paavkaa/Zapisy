# C

- [C](#c)
  - [Úvod](#úvod)
  - [Základy](#základy)
    - [Preprocesor](#preprocesor)
    - [Kompilátor](#kompilátor)
    - [Linker](#linker)
    - [Knihovny](#knihovny)
    - [Proměnné](#proměnné)
      - [Lokální](#lokální)
      - [Globální](#globální)
      - [Dynamické](#dynamické)
    - [Základní funkce](#základní-funkce)
      - [Vstupně-výstupní funkce:](#vstupně-výstupní-funkce)
      - [Práce s pamětí:](#práce-s-pamětí)
      - [Matematické:](#matematické)
      - [Matematické a logické operátory](#matematické-a-logické-operátory)
      - [Řídící struktury:](#řídící-struktury)
      - [Práce s časem](#práce-s-časem)
    - [Generování čísel](#generování-čísel)
    - [Oblasti paměti](#oblasti-paměti)
      - [Halda (Heap)](#halda-heap)
      - [Zásobník (Stack)](#zásobník-stack)
  - [Ukazatele (Pointer)](#ukazatele-pointer)
    - [Vlastnosti ukazatelů](#vlastnosti-ukazatelů)
  - [Pole](#pole)
    - [Základní operace s poli](#základní-operace-s-poli)
  - [Řetězce (String)](#řetězce-string)
  - [Struktury](#struktury)
    - [Deklarování struktur](#deklarování-struktur)
      - [Použití typedef](#použití-typedef)
      - [Struktura ve struktuře](#struktura-ve-struktuře)
    - [Přístup k hodnotám ze struktury](#přístup-k-hodnotám-ze-struktury)
  - [ENUM](#enum)
    - [definice ENUM](#definice-enum)
    - [použití ENUMu](#použití-enumu)
    - [explicitní přiřazení hodnot](#explicitní-přiřazení-hodnot)
  - [UNION](#union)
    - [práce s UNIONem](#práce-s-unionem)
    - [výhody](#výhody)
  - [Práce se soubory](#práce-se-soubory)
    - [Ukázka kódu](#ukázka-kódu)


## Úvod

> Kompilovaný jazyk
> 
> Typovaný jazyk - proměnné musí být udávany s datovým typem
> 
> Standartní knihovna - základní funkce, které fungují ve všech kompilátorech
> 
> Možné využití ukazatelů
> 
> Má preprocesor, to umožňuje použití maker
>
> identifikátor = jakýkoliv název (proměnná, funkce, makro...)

## Základy

### Preprocesor

> kód bere jako text
>
> Odstraňuje poznámky
>
> zpracovává vše začínající `#`

**Hlavičkový soubor**

> Textový soubor
>
> Obsahuje příkazy pro preprocesor

### Kompilátor

> Řeší syntatické chyby

### Linker

> Zpracuje zkompilovaný kód
>
> Vytváří .EXE soubor
>
> Řeší logické chyby

### Knihovny

`#include <stdio.h>` - uloženo na místě nainstalování kompilátoru
`#include "mojeknohovna.h"` - uloženo rámci projektu

### Proměnné

> Je nunté definovat datový typ proměnné

#### Lokální

> Deklarují se rámci bloku, existují pouze v daném bloku (ohraničen {})
>
> Každá instance funkce, nebo rekurzivní volání ma svou sadu lokálních proměnných

#### Globální

> Deklarace mimo jakoukoliv funkci
>
> Platí rámci všech funkcí od místa deklarování

|Název|Viditelnost|Platnost|Deklarace|
|:---:|---|---|---|
|auto|funkce/blok deklarace|po dobu běhu funkce/bloku|`výchozí typ`|
|intern|funkce/blok deklarace, přednost před extern|po dobu běhu programu (nenastavuje se původní hodnota)|`static`|
|extern|celý program, i mezi soubory|po dobu běhu programu, mezi všemi soubory|`extern`|

#### Dynamické

> Alokace na haldě pomocí malloc(), calloc(), realloc()
>
> Existují po dobu, dokud nejsoou uvolněny pomocí free()
>
> Slouží k práci s daty mezi bloky
>
> Práce s ukazateli


**Základní datové typy**

  |Zápis|Popis|
  |:---:|---|
  |int|celé číslo|
  |float/double|číslo|
  |char|znak|
  |bool|logické hodnoty|
  
### Základní funkce

#### Vstupně-výstupní funkce:

`printf()` - Výpis do konzole

`scanf()` - Čtení z konzole

`getchar()` - Načte jedno znakové vstupní písmeno ze standardního vstupu.

`putchar()` - Vypíše jedno znakové písmeno na standardní výstup.

`fgets()` - Načte řádek textu ze souboru

`fputs()` - Vypíše řádek textu do souboru

#### Práce s pamětí:

`malloc()` - Alokace paměti na haldě

`calloc()` - Alokace a inicializace paměti na haldě

`realloc()` - Změna velikosti alokované paměti na haldě

`free()` - Uvolnění alokované paměti

#### Matematické:

`sqrt()` - Odmocnina

`pow()` - Mocnina

`abs()` - Absolutní hodnota

`sin() cos() tan()` - Goniometrické funkce

`rand()` - Generování celých náhodných čísel

#### Matematické a logické operátory
`+, -, *, /, %` - Aritmetické

`++, --` - Přirovnávací 

```c
int i = 5, a = 3;
i++; // i = 6
++i; // i = 6

a = a + ++i; // a = 9
a = a + i++; // a = 8, i se zvětší až po použití ve výpočtu
```

`==, !=, >, <, >=, <=` - Relační

`&&, ||, !` - Logické

#### Řídící struktury:

**Podmínky**

> if, else if, else

```c
if(podmínka)
{
    //kód proběhne pokud byla podmínka splněná
}
else if(podmínka)
{
    //kód proběhne pokud předchozí podmínka nebyla splněná a tahle podmínka byla splněná
}
else
{
    //proběhne pokud nebyla žádná podmínka splněna
}
```

**Větvení**

> switch, case, default

```c
switch(volba) //volba - nejčastěji int nebo char, slouží k výběru case s danou hodnotou
    case 1:
        {
            // volba je int    
        }
        break; // ukončí switch po vykonání daného case, jinak by proběhly všechny následující
    case '1':
         {
            //volba je char
         }
         break;
    default:
        {
            // pokud volba nejde přiřadit k žádnému case
        }
```

**Cykly**

> for, while, do while

```c
for(dat_typ i; i < hodnota; i++) //(počáteční hodnota, podmínka cyklu, krok zvětšení proměnné)
{
    //kód
}

while(podmínka) // kontrola podmínky proběhne na začátku
{
    //kód
}

do
{
    //kód
} while(podmínka); // kontrola podmínky proběhne na konci -> kód proběhne min. jednou
```

#### Práce s časem
`time()` - Získání času
`ctime()` - Převod času na text

### Generování čísel

> knihovna <time.h>

**Inicializace generátoru**
```c
srand(time(NULL));
```

**Generování celého čísla**
```c
int cislo = random(); // náhodné číslo

int cislo = rand() % 10; // číslo v rozmezí 0 až 9

int cislo = rand() % (horniMez - dolniMez + 1) + dolniMez; //číslo omezeni horní a dolní mezí
```

### Oblasti paměti

#### Halda (Heap)

> Dynamicky alokovaná pamět
>
> Funkce malloc(), calloc(), realloc()
>
> Uvolnění paměti free(), jinak může dojít k úniku paměti (memory leak)

#### Zásobník (Stack)

> Správa a volání  funkcí a lokálních proměnných
>
> Princip LIFO (Last-In-First-Out) - nejnovější záznamy jsou umístěny na vrcholu zásobníku a jsou zpracovány jako první

## Ukazatele (Pointer)

> Práce s pamětí
>
> Proměnná, která ukládá adresu jiné proměnné, objektu
>
> Přistupuje k hodnotám, aniž bychom měli samotnou proměnnou/objekt

### Vlastnosti ukazatelů

> Ukazatel má před názvem `*`
>
> Přiřazuje se mu adresa proměnné - označena `&`
>
> Pokud se pracuje s adresou proměnné, na které pointer ukazuje, tak se `*` nepíše
>
> Při práci s hodnotami v proměnné, na kterou pointer ukazuje se `*` píše

1. Deklarace ukazatele
```c
int x = 10;
int *ptr; // Deklarace ukazatele na celočíselnou hodnotu

ptr = &x; // Přiřazení adresy proměnné x ukazateli ptr
```
2. Inicializace
```c
int x = 10;
int *ptr = &x; // Inicializace ukazatele ptr adresou proměnné x
```
3. Dereferencování (přístup)
```c
int x = 10;
int *ptr = &x;

*ptr = 20; // Změna hodnoty na adrese ukazatele ptr
```
5. Manipulace
```c
int x = 10;
int *ptr = &x;

ptr++; // Inkrementace ukazatele ptr
```
6. Null ukazatel
> ukazatel neukazuje na žádnou platnou adresu
    
```c
int *ptr = NULL; // Inicializace ukazatele jako null ukazatel
```

## Pole 

> Datová struktura, ukládá stejný typ prvků
>
> Tvořeno pevným počtem

**Deklarace**
```c
dat_typ pole[vel];
```

*Dynamické pole*
```c
int vel;
int *pole;

printf("Zadejte velikost pole: ");
scanf("%d", &vel);

pole = (int *)malloc(vel * sizeof(int));

//kód

free(pole);

return 0;
```

**Přistup k prvku**
```c
int cislo = pole[n];
```
**Změna hodnoty prvku**
```c
pole[n] = 10;
```

### Základní operace s poli

**Výpis**
```c
for (int i = 0; i < 5; i++) {
    printf("%d ", cisla[i]); // Výpis všech prvků pole
}
```

**Zjištění největšího prvku**

```c
int max = cisla[0];

for (int i = 1; i < pocetPrvku; i++) {
    if (cisla[i] > max) {
        max = cisla[i]; // Porovnání a aktualizace největšího prvku
    }
}
```

**Kopírování pole**
```c
int kopie[5];

for (int i = 0; i < pocetPrvku; i++) {
    kopie[i] = cisla[i]; // Kopírování hodnot prvků do nového pole
}
```

## Řetězce (String)

> Posloupnost znaků uložených v paměti
> 
> Jedná se o pole znaků
> 
> Knihovna: <string.h>

**Deklarace**
```c
char str1[] = "Hello world";

char str2[];
strcpy(str2, "Goodbye world");
```
*Deklarace dynamického řetězce*

```c
char *str;
int n = 10;

str = (char *)malloc(n * sizeof(char));
```

**Délka**
```c
int length = strlen(str);
```

>třetí paramentr u funkcí určuje maximální počet znaků, se kterým se bude pracovat 

**Kopírování**

>src se zkopíruje do dest

```c
strcpy(dest, src);
strncpy(dest, src, n);
```

**Spojování**

>src se přidá nakonec dest

```c
strcat(dest, src);
strncat(dest, src, n);
```
**Porovnání**

>Při shodě vrací 0, jinak 1

```c
int result = strcmp(str1, str2);
strncmp(str1, str2, n);
```

**Hledání podřetězce**

>Vrátí ukazatel na první výskyt substr v str

```c
char *ptr = strstr(str, substr);
```

## Funkce

>

## Struktury

> Umožňují vytvořit vlastní datové typy
>
> Seskupuje související datové prvky do jedné entity

`struct` - datový typ struktury

`typedef` - slouží k vlastnímu pojmenování struktury (není nutné psát poté datový typ)

**Výhody**

- Organizace souvisejících dat
- Přehlednost kódu
- Předávání struktur jako argument funkce

**Nevýhody**
- Nutnost správně přistupovat k dátům
- Ruční správa paměti
- Omezená podpora dědičnosti

### Deklarování struktur

```c
struct Osoba // název struktury
{
    //proměnné rámci struktury
    int vek;
    char jmeno[50];
    char prijmeni[50];
} Karel // deklarace proměnné při vytvoření struktury

struct Osoba Jana; // dodatečná deklarace proměnné typu struktura Osoba 
```

#### Použití typedef

> Pro přehlednost kódu, usnadní přístup ke struktuře

```c
typedef struct
{
    int vek;
    char jmeno[50];
    char prijmeni[50];
} Osoba; // název struktury se dává nakonec

Osoba Jarmila; // deklarace proměnné typu Osoba
```

#### Struktura ve struktuře

> Vnořené struktury umožňují hierarchické organizování dat, což usnadňuje reprezentaci složitých datových modelů
>
> Čitelnost a udržovatelnost: Kód se stává čitelnějším, protože struktury ve strukturách lépe odrážejí vztahy mezi daty

```c
#include <stdio.h>
#include <string.h>

// Struktura pro autora
struct Autor {
    char jmeno[50];
    char prijmeni[50];
};

// Struktura pro knihu
struct Kniha {
    char nazev[100];
    struct Autor autor;
    int rokVydani;
};

int main() {
    // Vytvoření instance struktury Kniha
    struct Kniha kniha1;

    // Inicializace hodnot
    strcpy(kniha1.nazev, "Pánský klub");
    strcpy(kniha1.autor.jmeno, "Chuck");
    strcpy(kniha1.autor.prijmeni, "Palahniuk");
    kniha1.rokVydani = 1996;

    // Výpis informací o knize
    printf("Název knihy: %s\n", kniha1.nazev);
    printf("Autor: %s %s\n", kniha1.autor.jmeno, kniha1.autor.prijmeni);
    printf("Rok vydání: %d\n", kniha1.rokVydani);

    return 0;
}
```

### Přístup k hodnotám ze struktury

`.` - operátor pro přístup k hodnotám

```c
Osoba.vek = 20;

strcpy(Osoba.jmeno, "Pepa");
```

`->` - operátor pro přístup k hodnotám pomocí ukazatele

```c
struct Osoba Karel;
struct Osoba *ptrOsoba;

ptrOsoba = &Karel

ptrOsoba->vek = 20;
strcpy(ptrOsoba->jmeno, "Pepa");
```

## ENUM

> zkratka pro enumerace
>
> Enumerace umožňují vytvářet srozumitelný kód tím, že pojmenují hodnoty, které mohou mít pouze omezený počet různých variant
>

### definice ENUM
> seznam konstant
>
> nulté indexování jako u polí

```c
enum Dny { Pondeli, Utery, Streda, Ctvrtek, Patek, Sobota, Nedele };
```

### použití ENUMu

> deklarace proměnné typu enum

```c
enum Dny dnes = Pondeli;
```

### explicitní přiřazení hodnot

```c
enum Dny { Pondeli = 1, Utery = 2, Streda = 3, Ctvrtek = 4, Patek = 5, Sobota = 6, Nedele = 7 };
```

## UNION

> umožňuje sdílet stejnou oblast paměti pro více datových typů
>
> může uchovat pouze jednu hodnotu ze svých členů najednou

### práce s UNIONem

```c
union MojeUnion {
    int celeCislo;
    double desetinneCislo;
    char retezec[20];
};

union MojeUnion u;
u.celeCislo = 42;

printf("Cele cislo: %d\n", u.celeCislo);
printf("Velikost unionu: %lu bytu\n", sizeof(union MojeUnion));
```

### výhody

> šetří paměť
>
> využívá se při komunikaci s hardwarem, nebo při práci s binárními daty
>
> převod mezi datovými typy nebo ukládání různých typů v jednom datovém bloku

```c
#include <stdio.h>

union Hodnota {
    int celeCislo;
    double desetinneCislo;
    char znak;
};

int main() {
    union Hodnota v;

    v.celeCislo = 42;
    printf("Cele cislo: %d\n", v.celeCislo);

    v.desetinneCislo = 3.14159; // vždy dojde k přepsání hodnoty, pracuje se s jedným datovým typem v daný okamžik
    printf("Desetinne cislo: %lf\n", v.desetinneCislo);

    v.znak = 'A';
    printf("Znak: %c\n", v.znak);

    return 0;
}
```
## Práce se soubory

> umožňuje <stdio.h>
>
> umožňuje čtení a zápis

### Ukázka kódu

```c

// otevření souboru
FILE *soubor;
soubor = fopen("mojefile.txt", "r"); // Pokud se soubor nepodaří otevřít, není uložena žádna hodnota, proto je NULL
if (soubor == NULL) {
    printf("Nepodarilo se otevrit soubor.\n");
    return 1;
}

char text[100];
fscanf(soubor, "%s", text); // Čtení slova ze souboru

fprintf(soubor, "Hello, World!\n"); // Zápis řetězce do souboru

if (feof(soubor)) {
    printf("Konec souboru dosazen.\n");
}

fclose(soubor); // Ukončení vazby se souborem

```

**Práce s binárním souborem**

```c
struct Zaznam {
    int cislo;
    char jmeno[50];
};

// Čtení binárních dat ze souboru
fread(&zaznam, sizeof(struct Zaznam), 1, soubor);

// Zápis binárních dat do souboru
fwrite(&zaznam, sizeof(struct Zaznam), 1, soubor);
```
`&zaznam` - adresa struktury
`sizeof(struct Zaznam)` - vrací velikost struktury
`1` - určuje počet
`soubor` - specifikuje otevřený soubor, ze kterého budou data čtena