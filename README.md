# OSTRAJava #

OSTRAJava má za cíl pozvednout kvalitu (nejen ostravského) programování. Na rozdíl od Javy vychází přímo z ostravského nářečí, tedy jazyka který obyčejní lidé používají. Typický ostravský horník pak nebude mít problém přejít od těžby rudy ke klávesnici. Jazyk tak mimo jiné řeší i problém nezaměstnanosti na moravsko-slezsku.

## Syntaxe ##

### Příklad 1 - Hello world ###
Zde je typický Hello world program v OSTRAJavě.
```
#!java
banik pyco

tryda Ostrava{
    rynek(){
        Konzola.pravit("Toz vitaj") pyco
    }
} 

fajront pyco

```

* Všechny soubory OSTRAJavy začínají klíčovým slovem **banik**. 
* Všechny soubory OSTRAJavy končí klíčovým slovem **fajront**, označující konec směny.
* Každý statement programu musí být ukončen klíčovým slovem **pyco**. Nahrazuje tedy v javě používaný středník.
* Hlavní třída programu se vždy jmenuje **Ostrava**(jak jinak) a hlavní metoda se vždy jmenuje **rynek**
* Pozn.: OSTRAJava je case in-sensitive a nedoporučuje se používat diakritiku, jinými slovy s **malym a kratkym**

### Typy ###
OSTRAJava obsahuje 4 primitivní typy:

* **cyslo** - integer
* **bul** - boolean
* **chachar** - char
* **cyslo_desetinne** - float

Hodnoty:

* *fajne* - true
* *nyt* - false
* *chuj* - null

Základní knihovna OSTRAJavy také obsahuje třídy

* **Dryst** - ekvivalent String.  
* **Bazmek** - vsechny tridy dedi implicitne z teto tridy. Obsahuje metody naDryst() a kantuje(Bazmek b), ekvivalent pro toString() a equals(Object o)
* **Citac** - cteni ze souboru
* **Konzola** - vypis do konzole
* **Bafr** - jednoduchý buffer na čtení charů

### Deklarace ###
Deklaraci je nutno začít klíčovým slovem **toz**

```
#!java
toz cyslo i = 1 pyco
```


### Podmínky ###
Pro vytvoření podmínky použijeme konstrukt **kaj**  - **kajtez** - **boinak**

Jednotlivé výrazy můžeme spojovat pomocí boolenovského **bo** (or) a **aj** (and) 

```
#!java
toz bul a pyco
toz bul b pyco

//...

kaj (a == fajne bo b == fajne){
   // ...
} kajtez (a == nyt aj b == fajne){
   // ...
} boinak {
   // ...
}

```

### Cykly ###
Cyklus má OSTRAJava pouze jeden. Pomocí **rubat** vytvoříme while.

Rubat cyklus se dá přeřušit pomocí **zdybat** (break) a nebo přeskočit jeden cyklus pomocí **dlabat** (continue)

```
#!java

toz cyslo i = 0 pyco

rubat (i < 5){
    kaj (i == 4){
      zdybat pyco 
   }
   //...
   i = i+1 pyco
}

``` 

### Příklad 2 ###
Následuje jednoduchý příklad na čtení ze souboru

```
#!java
banik pyco

tryda Priklad2 {
   nacti(Dryst nazevSouboru){

        toz Citac c = zrob Citac() pyco
        c.otevr(nazevSouboru) pyco

        toz Dryst radka pyco
        radka = c.citajRadku() pyco

        rubat (radka != chuj){
            // ...
            radka = c.citajRadku() pyco
        }
        c.zavr() pyco
    }
}

fajront pyco 

```

### Dědičnost ###

```
#!java
banik pyco

tryda Obdelnik{
   toz cyslo dylka pyco
   toz cyslo vyska pyco

   Obdelnik(cyslo dylka, cyslo vyska){
      joch.dylka = dylka pyco
      joch.vyska = vyska pyco
   }
}

tryda Stverec fagan od Obdelnik{
    Stverec(cyslo velikost){
       forant(velikost, velikost) pyco
    }
} 

tryda Ostrava{
   rynek(){
      toz Stverec s = zrob Stverec(5) pyco 
   }
}

fajront pyco

```

OSTRAJava je samozřejmě jazyk objektový. Pokud chceme uvést třídu z které chceme dědit použijeme konstrukt **fagan od**.

**joch** slouží jako reference na vlastní instanci tedy ekvivalent this

**forant** tedy předák na šichtě slouží jako reference na rodiče, tedy ekvivalent super

### Metody ###
Navratový typ metody se píše stejně jako v javě před název metody. Pro metodu s prázdným návratovým typem není třeba psát nic. 

Pro návrat hodnot je použito klíčové slovo **davaj**

```
#!java
tryda Buu{
   cyslo fuu(Dryst text){
       //...
       davaj text.dylka pyco
   }
}
```

## Implementace ##

Implementováno momentálně je:

* Compiler
* * Pokročilá typová kontrola (přiřazení objektů, návratové hodnoty funkcí, fieldy)
* * Kontrola deklarace a inicializace proměnných
* * Kontrola volání metod (static, non-static)
* * Kompilace do .tryda classfilu

* Interpreter
* * Paměť pomocí pole objektů
* * Generační garbage collector
* * Nativní volání
* * Statické volání
* * Primitiva (integer, float) na stacku a pointer s 1 na posledním bitu
* * Aritmetické operace pro integer a float
* * Pole (primitiv i referencí)
* * Dynamický lookup metod
* * Overload metody

### Kompilace a spuštění ###

V root složce 

```
#!

mvn clean
mvn install

```

Nastavení práv pro skripty

```
#!
chmod u+x ostrajavac
chmod u+x ostrajava
```

Program SATSolver je ve složce examples/SATSolver/

Kompilace 
```
#!
./ostrajavac examples/SATSolver/ -d compiled/

```

Spuštění
```
#!
./ostrajava -h 1024 -f 256 -s 128 compiled/ resources/sats/01.txt

```