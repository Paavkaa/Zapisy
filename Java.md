# JAVA
- [JAVA](#java)
  - [Základy](#základy)
    - [Výpis a načtení](#výpis-a-načtení)
    - [Datové typy](#datové-typy)
    - [Generátor čísel](#generátor-čísel)
    - [Podmínky](#podmínky)
    - [Cykly](#cykly)
  - [Funkce](#funkce)

## Základy

### Výpis a načtení

`System.out.println()` - výpis (IJ zkratka `sout`)

`Scanner vstup = new Scanner(System.in, charset "nazev_charset");` - do proměnné se uloží Scanner pro načtení z klávesnice

`<dat. typ> prom = vstup.next<dat. typ>()` - uložení vstupu do proměnné

```java
Scanner input = new Scanner(System.in, Windows-1250);
int a = input.nextInt();
String b = input.nextLine();
```
### Datové typy

`int` - celé číslo

`double` - realné číslo

`char` - znak

`String` - řetězec

`List` - seznam

`void` - datový typ, nevracející hodnotu

> pole, objekty

### Generátor čísel
`<dat. typ> prom = rand.next<dat. typ>(dolni_mez, horni_mez)`, `<dat. typ> prom = rand.next<dat. typ>(horni_mez)` - generování náhodného čísla daného datového typu
```java
double prom = rand.nextDouble(1, 50) // realná čísla v intervalu <1;50)
```

### Podmínky
**Ternární operátor**
```java
System.out.println(a > b? "A > B": "B > A");
int x = (a > b? a:b);
String y= (a > b? "A > B": "B > A");
```

**If**
```java
if()
{
    //kód
}
else if
{
    //kód
}
else
{
    //kód
}
```

### Cykly
**While**
```java
while()
{
    //kód
}
```
**Do while**
```java
do
{

} while();
```
**For**
```java
for(<dat. typ> prom == hodnota; prom <=> mez; prom++)
{

}
```
## Funkce

> Přetížení - existuje více funkcí se stejným názvem, funkce se volí podle datových typů parametrů

`public static <dat. typ> <název funkce>` - hlavička funkce

```java
    public static double prumer(int a,int b)
    {
        return (a+b)/2.0;
    }
    public static double prumer(int a,double b)
    {
        return (a+b)/2;
    }

    public static double prumer(int a,double b, int c)
    {
        return (a+b+c)/3;
    }
```