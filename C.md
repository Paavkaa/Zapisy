# C

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

## Základy

### Proměnné

> Je nunté definovat datový typ proměnné

#### Lokální

> Deklarují se rámci bloku, existují pouze v daném bloku (ohraničen {})
>
> Každá instance funkce, nebo rekurzivní volání ma svou sadu lokálních proměnných

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
  
### Funkce

#### Vstupně-výstupní funkce:

`printf` - Výpis do konzole

`scanf` - Čtení z konzole

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

#### Matematické a logické operace:

`+, -, *, /, %` - Aritmetické operace

`++, --` - Přičítání a odčítání

`==, !=, >, <, >=, <=` - Porovnávací operace

`&&, ||, !` - Logické operace

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
```****

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
