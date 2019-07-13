Twoim zadaniem jest rozwinięcie obecnego w tym repozytorium projektu. Lista zadań do wykonania znajduje się poniżej.
Projekt jest wykonany we frameworku vue.js.
Wybierz 3 dowolne zadania i je zrealizuj.

### Uruchomienie projektu:
1. npm install
2. npm run web

### Zadania:
1. Dodaj komponent przycisku edycji każdego elementu listy i dodaj jako kolejną kolumnę do listy.
2. Dodaj edycję elementu listy z zapisem do API (edycja tylko danych, które są na liście). Edycja może być wykonywana od razu na wierszu listy lub na nowym widoku z formularzem.
3. Dostosuj widoki pod RWD.
4. Dodaj menu (możesz wymyślić dodatkowe elementy, które nigdzie nie prowadzą), które na telefonach zamienia się w hamburger menu.
5. Skonfiguruj środowisko do testów jednostkowych i napisz testy do widoku listy.

### Uwagi:
1. Pobierz kopię tego repozytorium (nie rób forka), dodaj na swoje konto i ustaw publiczny dostęp.
2. Każdy task wypushuj do mastera swojego repozytorium ze squashem i odpowiednim opisem w języku angielskim.
3. Testowe API: https://github.com/typicode/jsonplaceholder#how-to


My tasks solution:
1. task #1: I created this.edit element which says which row is edited. At first this.edit has value -1, but is changing when edit button is clicked (because of method edit_row). I used v-if and v-else constructions to determine (according to this.edit) what is displayed: data or editing inputs. 

2. task #2: Every editing input received name and @input attributes. I also created new object - this.editedElem, which stores changing input's values. During editing user has two buttons available: save and reject. Save button runs save_row method, which gets as input an index of edited row and updates (fetch) the data in API, after that this.edit and this.editedElem are cleaned. Reject button sets up this.edit on -1 (no row is edited).

3. task #4: I created &lt nav &gt tag (which contains menu list) and &l tspan &gt tag (which contains hamburger menu). I created also a new object this.classObject which is responsible for toggling class in \&lt nav &gt tag. Navbar is visible on bigger screen and when hamburger menu is clicked on smaller one (because of onMenuClick method). Hamburger menu is visible only on smaller screen. To get responsivity I used media queries.

