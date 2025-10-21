# **🎯 Generator Tarcz Strzeleckich i Tabel Balistycznych (Pneumatyka)**

Projekt zawiera skrypt w Pythonie (mil\_target\_generator.py) wykorzystujący bibliotekę reportlab do generowania precyzyjnych, wielostronicowych dokumentów PDF z tarczami strzeleckimi oraz arkuszami konwersji (Dope Sheets) dla strzelectwa pneumatycznego.

Tarcze są skalowane w proporcji 1:1, co oznacza, że fizyczny wymiar jednostki siatki (np. 1 MIL) jest zawsze poprawny dla zadanej odległości.

## **⚙️ Wymagania i Instalacja**

Projekt wymaga zainstalowanego środowiska Python 3 oraz biblioteki reportlab.

\# Wymagana instalacja biblioteki ReportLab  
pip install reportlab

## **✨ Kluczowe Funkcje**

* **Tarcze MIL-DOT (Siatkowe):** Generowanie tarcz z siatką MIL w skali 1:1 dla określonych dystansów. Siatka główna co 1 MIL, subgrid co 0.2 MIL (z automatycznym wyłączaniem, gdy $1 \\text{ MIL} \< 5 \\text{ mm}$).  
* **Tarcze MOA (Siatkowe):** Generowanie tarcz z siatką MOA w skali 1:1. Siatka główna co $1/4 \\text{ MOA}$ (z automatycznym wyłączaniem, gdy $1 \\text{ MOA} \< 5 \\text{ mm}$).  
* **Tarcze Standardowe:** Generowanie tarcz w skali 1:1 zgodnie ze standardami ISSF (Karabin Pneumatyczny $10 \\text{ m}$, Pistolet Pneumatyczny $10 \\text{ m}$). Tarcze te są automatycznie układane w macierzy, aby zmaksymalizować wykorzystanie strony A4.  
* **Tabele Konwersji (Dope Sheets):** Generowanie oddzielnych plików PDF z tabelami przeliczeniowymi dla lunet $0.25 \\text{ MIL}/\\text{klik}$ oraz $1/4 \\text{ MOA}/\\text{klik}$ na dystansach $5 \\text{ m}$ do $100 \\text{ m}$.  
* **Pola Danych:** Każda tarcza zawiera sekcję do wpisania danych strzelania (Strzelec, Broń, Śrut, Warunki, Data).

## **🚀 Użycie**

Uruchomienie głównego skryptu spowoduje automatyczne wygenerowanie wszystkich zdefiniowanych tarcz i tabel konwersji w bieżącym katalogu.

python mil\_target\_generator.py

### **Wygenerowane Pliki**

Skrypt generuje następujące pliki PDF:

| Typ Tarczy | Nazwa Pliku | Odległości | Skala |
| :---- | :---- | :---- | :---- |
| **MIL-DOT** | mil\_target\_10m.pdf, mil\_target\_25m.pdf, mil\_target\_50m.pdf | $10 \\text{ m}$, $25 \\text{ m}$, $50 \\text{ m}$ | 1:1 |
| **MOA** | moa\_target\_10m.pdf, moa\_target\_25m.pdf, moa\_target\_50m.pdf | $10 \\text{ m}$, $25 \\text{ m}$, $50 \\text{ m}$ | 1:1 |
| **Standard (Pistolet)** | standard\_pistol\_target.pdf | $10 \\text{ m}$ (nominalna) | 1:1 (Macierz) |
| **Standard (Karabin)** | standard\_rifle\_target.pdf | $10 \\text{ m}$ (nominalna) | 1:1 (Macierz) |
| **Tabela MIL** | dope\_sheet\_mil.pdf | $5 \\text{ m}$ \- $100 \\text{ m}$ | $0.25 \\text{ MIL}/\\text{klik}$ |
| **Tabela MOA** | dope\_sheet\_moa.pdf | $5 \\text{ m}$ \- $100 \\text{ m}$ | $1/4 \\text{ MOA}/\\text{klik}$ |

## **🛠️ Konfiguracja (mil\_target\_generator.py)**

Kluczowe stałe konfiguracyjne znajdują się na początku skryptu i umożliwiają dostosowanie wygenerowanych tarcz:

| Stała | Opis | Domyślna wartość |
| :---- | :---- | :---- |
| TARGET\_DISTANCES | Lista odległości, dla których generowane są tarcze MIL/MOA. | \[10.0, 25.0, 50.0\] |
| FIXED\_MARGIN\_CM | Margines na stronie A4 w centymetrach. | 2.0 |
| BULLSEYE\_COLOR | Kolor centralnego punktu celu na tarczach siatkowych. | 'black' |
| FIXED\_BULLSEYE\_DIAMETER\_CM | Średnica centralnego celu na tarczach siatkowych. | 2.5 |
| MIN\_GRID\_SIZE\_CM | Minimalny fizyczny rozmiar $1 \\text{ MIL}/1 \\text{ MOA}$ w $\\text{cm}$, przy którym drukowane są podziałki subgrid. | 0.5 |
| PISTOL\_TARGET\_DATA / RIFLE\_TARGET\_DATA | Definicje pierścieni punktowych dla tarcz standardowych. | Zdefiniowane w kodzie |

