LOC Calculator. java

       +++++   LOC za Calculator .java  +++++

LOC = Ukupno linija Code-a u Calculator.java (188)
Od toga ukupno 141 linija efektivnog koda.
Praznih linija je 43
A linija komentara je 4

-----Staticka analiza datog koda iz Calculator.java-------
        Alat (SonarQube)

Linija koda br. 1 - Prebaciti import fajl u odgovarajuci imenovani paket.

Linija koda br. 4 - Calculator - Dodatni privatni konstruktor da bi se sakrio javni kontruktor.

Linija koda br. 7 – Globalna staticka promenljiva `finalResult` može izazvati probleme u višenitnom okruženju (thread-safety problem).

Linija koda br. 11 – Klasa `Operations` je ugnjezdena statička klasa sa konstantama – može biti jasnije predstavljena kao `enum`.

Linija koda br. 17 – Metoda `ToString()` ne koristi standardnu Java konvenciju imenovanja (`toString()`), što može biti zbunjujuće.

Linija koda br. 35 – Uslov dodavanja `0` na početak izraza rešen na jednostavan način, ali bi bilo bolje obaviti validaciju izraza pre obrade.

Linija koda br. 42 – Parsiranje operatora ručno, bez validacije izraza – može doći do nepredviđenih ponašanja sa nevalidnim unosima (npr. `++`, `--`, razmaci itd).

Linija koda br. 55 – Nema validacije broja i operatora – npr. ako je korisnik uneo `5++2`, to se ne hvata, može izazvati greške.

Linija koda br. 61 – Vraća `"ERROR"` ako dođe do greške pri parsiranju brojeva, ali to bi moglo biti detaljnije (npr. poruka o tome šta je pošlo po zlu).

Linije koda br. 66-127 – Metoda `Calculate()` je **predugačka**, sadrži dosta dupliranog koda – krši DRY princip.

Linije koda br. 69, 73, 81, 89, 97, 105, 113, 121 – Kod za izvršavanje operacija (`+`, `-`, `*`, `/`) se ponavlja – preporučuje se ekstrakcija u pomoćnu metodu.

Linija koda br. 66 – Korišćenje rekurzije bez ograničenja može izazvati `StackOverflowError` kod veoma dugih izraza – razmotriti iterativni pristup.

Linija koda br. 70 – `result +=` se koristi gde bi jednostavno `result =` bilo jasnije jer se `result` uvek inicijalizuje sa 0.

Calculator.java – opšte – Klasa ne koristi `unit testove`, nema validaciju unosa korisnika, i ne obrađuje izraze sa razmacima ili složenijim slučajevima (npr. zagrade).

Calculator.java – opšte – Nedostatak logičkog prioriteta (operator precedence) rešen je ručnim poređenjem indeksa, ali bi korišćenje parsera/stack pristupa bilo skalabilnije.

Calculator.java – opšte – Kod funkcioniše, ali je teško održiv i sklon greškama. Potrebna refaktorizacija kako bi bio čitljiviji i modularniji.


      +++++ LOC za Start .java +++++++


LOC = Ukupno linija Code-a u Start.java (25)
Od toga ukupno 20 linija efektivnog koda.
Praznih linija je 5
A linija komentara je 0

-----Staticka analiza datog koda iz Start .java-------
        Alat (SonarQube)

Linija koda br. 8 – Varijabla `scanIn` se kreira unutar petlje i svaki put se pravi novi objekat Scanner, što je nepotrebno. Bolje je instancirati je **jednom izvan petlje**.

Linija koda br. 13 – Svaki prolazak kroz petlju kreira novi `Scanner`, ali se prethodni nikad ne zatvori (osim ako je unet `exit`). To može izazvati **Resource leak**.

Linija koda br. 13 – Potencijalni `NoSuchElementException` ako se unosi EOF (kraj ulaza bez unosa).

Linija koda br. 16 – Dobro je što se koristi `"exit"` kao uslov za izlaz, ali možda bi bilo korisno dozvoliti i `"EXIT"` / `"Exit"` – preporuka: `Expression.equalsIgnoreCase("exit")`.

Linija koda br. 20 – `System.out.println(Calculator.Run(Expression));` – ako `Calculator` vrati `"ERROR"`, korisnik ne zna zašto. Bolje bi bilo prikazati poruku poput: `"Invalid expression: ERROR"`.

Linija koda br. 7 – Poruka `"Enter expression here (type 'exit' to quit):"` se ispisuje samo jednom. Razmotriti da se ponavlja u petlji nakon svake evaluacije, kako bi korisnik znao da može odmah unositi novi izraz.

Start.java – opšte – Nema obrade grešaka: ako korisnik unese `null` ili prazan string, može doći do `StringIndexOutOfBoundsException` u `Calculator` (npr. `expression.charAt(0)` u `Calculator`).

Start.java – opšte – Kod je jednostavan i funkcionalan, ali korisnički interfejs može biti poboljšan za bolju interakciju i obradu grešaka.