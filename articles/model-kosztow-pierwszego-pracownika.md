# Model pełnego kosztu pierwszego pracownika we Włoszech: arkusz w pięciu warstwach

> Jak polski dział finansów może zbudować arkusz pełnego kosztu włoskiego pracownika, od danych wejściowych po kontrolę wyniku, z przeliczeniem na złote.

Zarząd pyta: „ile nas będzie kosztował człowiek w Mediolanie?”. Kontroler finansowy otwiera arkusz, wpisuje pensję, dolicza „około dwudziestu procent ZUS” i przelicza na złote. Wynik jest za niski, a różnica wychodzi przy pierwszej grudniowej fakturze. Ten artykuł pokazuje, jak zbudować model kosztu włoskiego pracownika, który się nie rozjedzie.

Model ma pięć warstw. Każda to osobna sekcja arkusza.

## Warstwa 1: dane wejściowe

Osobna zakładka z założeniami. Nic w niej nie liczysz, tylko wpisujesz:

- roczne brutto (RAL),
- układ zbiorowy (CCNL) i poziom,
- liczbę rat wynagrodzenia w roku (13 lub 14),
- miasto zamieszkania pracownika,
- datę rozpoczęcia,
- planowane premie i prowizje,
- benefity: bony żywieniowe, samochód, fundusz zdrowotny,
- kurs EUR/PLN do budżetu.

Każde założenie powinno mieć źródło i datę. Gdy coś się zmieni, zmieniasz jedną komórkę.

Uwaga na kurs. W naszej usłudze fakturujemy w złotych po kursie referencyjnym EUR z dnia faktury, bez spreadu, albo w euro. Do budżetu użyj kursu konserwatywnego i aktualizuj go co kwartał.

## Warstwa 2: podstawa wymiaru składek

Z danych wejściowych wylicz podstawę. Na niej oprzyj dwie główne stawki:

- składka emerytalna pracodawcy (IVS): 23,81% podstawy,
- składka emerytalna pracownika (IVS): 9,19% podstawy.

Druga nie jest Twoim kosztem, ale potrzebujesz jej do oszacowania netto, o które zapyta kandydat. Pamiętaj, że dodatkowe raty, czyli 13. i 14. pensja, też wchodzą do podstawy. Jeśli liczysz od dwunastu równych pensji, zaniżasz koszt.

Do składek emerytalnych dolicz pozostałe składki pracodawcy do INPS (bezrobocie, choroba, macierzyństwo, świadczenia rodzinne, fundusze gwarancyjne) według zestawienia od dostawcy płac.

## Warstwa 3: ubezpieczenie wypadkowe

INAIL ma osobny wiersz. Obowiązują taryfy z 2019 roku, ale sposób ich stosowania zmienił się w 2026 roku. Nie kopiuj więc stawki ze starego artykułu.

Zbuduj wiersz z dwóch komórek: stawki i zasady jej stosowania. Wypełnij obie z aktualnego źródła INAIL dla Twojej klasyfikacji. Dla stanowisk biurowych pozycja będzie mała, dla serwisantów i inżynierów w terenie wyraźnie większa.

## Warstwa 4: pozycje poza listą płac

Tu ląduje wszystko, czego nie ma w składkach, a co kosztuje:

- **TFR**, odprawa narastająca, ok. 6,91% rocznego wynagrodzenia. W naszym modelu wpłacana co miesiąc do funduszu pracownika, więc nie tworzy zobowiązania na koniec.
- **Fundusze z CCNL**, np. dodatkowy fundusz zdrowotny lub emerytalny.
- **Benefity**: bony żywieniowe, samochód, sprzęt, delegacje.
- **BHP**: badania lekarskie i szkolenia.
- **Opłata EOR**: 250 € miesięcznie.
- **Rekrutacja i relokacja**, jeśli dotyczy.

## Warstwa 5: suma i kontrole

Na końcu suma roczna, rozkład miesięczny i przeliczenie na złote. Do tego kilka kontroli:

- **Koszt / RAL.** Jeśli wynik jest bliski polskiemu wskaźnikowi kosztu pracodawcy, coś pominąłeś.
- **Rozkład miesięczny.** Przy wypłacie dodatkowych rat jednorazowo grudzień (i lipiec przy 14. pensji) musi być wyraźnie wyższy. Przy wypłacie proporcjonalnej miesiące są równe.
- **Rezerwy.** Czy 13./14. pensja i TFR mają rezerwę miesięczną?
- **Zgodność z wyceną.** Porównaj wynik z wyceną dostawcy. Różnice wyjaśnij przed akceptacją budżetu.

## Dlaczego warto to zrobić porządnie

Model to nie tylko budżet. To narzędzie do rozmowy z zarządem i z kandydatem. Pozwala szybko odpowiedzieć na pytania: co się stanie, jeśli podniesiemy ofertę? co, jeśli kandydat zamieszka w Turynie zamiast w Mediolanie? co, jeśli kurs złotego się zmieni?

Pozwala też uczciwie porównać koszt włoskiego pracownika z polskim. Porównuj całkowity koszt pracodawcy w obu krajach, w tej samej walucie, a nie brutto z brutto.

## Model w wersji uproszczonej

Jeśli nie chcesz budować arkusza od zera, nasz [kalkulator kosztów](/kalkulator-kosztow.html) robi większość tej pracy: pokazuje RAL, składki INPS, INAIL, TFR i opłatę, a także rozkład faktur w ciągu roku i sumę w złotych. Na jego podstawie przygotujemy dokładną wycenę dla konkretnego stanowiska.

## Pytania polskich firm

**Jak często aktualizować model?** Przynajmniej raz w roku, po ustawie budżetowej i zmianach stawek, oraz przy każdym odnowieniu układu zbiorowego. Kurs walutowy co kwartał.

**Czy model dla jednego pracownika wystarczy dla zespołu?** Jako szablon tak. Każde stanowisko ma jednak własny układ, poziom, miasto i benefity, więc zrób osobną kolumnę dla każdej osoby.

**Co z kosztami po stronie polskiej spółki?** Do modelu dolicz własne koszty: czas managerów, podróże do Włoch, sprzęt wysyłany z Polski. Nie są częścią listy płac, ale są częścią kosztu wejścia na rynek.


**Jak wygląda rozliczenie z nami?** Jedna faktura miesięcznie, w złotych po kursie referencyjnym EUR z dnia faktury, bez spreadu walutowego, albo w euro. Faktura obejmuje rzeczywisty koszt zatrudnienia z danego miesiąca i opłatę 250 € za pracownika, z dołączonym zestawieniem pasków. Na start pobieramy zwrotny depozyt równy szacowanemu kosztowi jednego miesiąca oraz jeden miesiąc z góry.

Różnice między polskim a włoskim kosztem pracodawcy znajdziesz też na stronie [Włochy a Polska](/wlochy-vs-polska.html).

{{< compare-table compact="true" >}}


---
Source: https://zatrudnieniewewloszech.com/articles/model-kosztow-pierwszego-pracownika.html · 2026-10-16
