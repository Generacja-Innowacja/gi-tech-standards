# Git - how to
Git to system kontroli system, czyli program czuwający nad prowadzonymi równolegle zmianami w kodzie. Tego typu rozwiązania są nieodłącznym elementem pracy programisty - im większy projekt, im więcej developerów, tym bardziej pogmatwana może okazać się niezależna praca developerów. Nietrudno wyobrazić sobie sytuację, w której dwie osoby wprowadzają zmiany w obrębie tego samego pliku. Tutaj na straży stoi git, który czuwa nad tym, żeby zmiany się nie gryzły.
Git ma oczywiście swoje alternatywy, np. CVS, natomiast w fundacji używamy tylko i wyłącznie gita.
Github to jeden z serwisów, który oferuje gita. Zaznaczę: nie jest to to samo. Git to system niezależny, natomiast github jest portalem, który pozwala nam hostować pliki i obsługiwać je za pomocą gita. Oprócz Githuba funkcjonuje m.in. Gitlab, który również jest serwisem gitowym.

### Jak zacząć?
Pierwszym krokiem jest instalacja gita i sklonowanie (pobranie) *repozytorium*. Gita można pobrać stąd: https://git-scm.com/downloads/ w wersji na swój ulubiony system operacyjny. Można też skorzystać z aplikacji Github Desktop, która oferuje graficzny interfejs. W tym dokumencie skupimy się na konsolowej obsłudze gita.
Po instalacji przechodzimy do katalogu, w którym chcemy zawrzeć projekt. Porównajmy dwa polecenia:
```
git clone [repo]
git clone [repo] .
```
W miejsce linku należy wprowadzić link do repozytorium. Różnica między powyższymi poleceniami to kropka na końcu. Jeżeli kropki nie będzie: git utworzy nowy folder o nazwie zgodnej z nazwą repozytorium i umieści tam wszystkie pliki. Jeżeli kropka się pojawi: git ściągnie repozytorium do aktualnego katalogu.


### Jak zapisać zmianę?
Porozmawiajmy o tym, jak wygląda praca z gitem. Podstawową jednostką czasowo-roboczą jest `commit`, czyli pojedyncza zmiana w kodzie, mogąca jednak obejmować więcej niż jeden plik. Np. gdy zmieniamy nazwę klasy, to prawdopodobnie chcemy zachować spójność między różnymi plikami, więc w obrębie jednego commita wprowadzamy zmiany w kilku plikach. No dobrze, ale jak commitować?
Możemy wyróżnić cztery etapy, w których może znajdować się kod:
 * katalog roboczy (working directory) - czyli zmiany wprowadzone w obrębie lokalnej kopii repozytorium,
 * staging area - zmiany przygotowane do commita, zmiany które chcemy zawrzeć w commicie,
 * local repository - zmiany lokalnie scommitowane, jednak niezsynchronizowane z chmurą,
 * cloud repository - zmiany zsynchronizowane z repozytorium w chmurze.
Wszelkie modyfikacje plików dzieją się w working directory. Takie zmiany widzimy oznaczone kolorem czerwonym po wpisaniu komendy `git status`. Komenda ta sama nam podpowiada: aby dodać rzeczy do staging area, używamy komendy `git add [względna ścieżka do pliku]`. Możemy też dodać cały katalog: `git add [względna ścieżka do katalogu]` oraz wszystkie zmiany w obecnym katalogu i podkatalogach: `git add .`. Jeżeli stwierdzimy, że danego pliku commitować nie chcemy, możemy użyć polecenia `git restore --staged [plik]` (działa także dla folderów). Polecenia `git restore [file]` użyjemy natomiast, by cofnąć wszystkie zmiany w obrębie working directory (tj. przypadkowo usunęliśmy cały plik - `git restore [plik]` nam go przywróci do wersji z ostatniego commita).
Gdy mamy już nasze zmiany na etapie staging area i chcemy je "zapisać" w repozytorium, to jest to właśnie moment commitowania. Nic prostszego: `git commit -m [notka: co zostało zrobione? / tytuł commita]`. Jeżeli przypadkiem wpiszesz bez opcji `-m`, szukaj ratunku w gogle pod hasłem vim.
Gdy popełniliśmy już commita, powinniśmy go zsynchronizować z chmurą. Użyjemy do tego polecenia `git push origin HEAD`.


### Jak i po co branchować?
Zanim zaczniesz pracę, musisz utworzyć lokalną gałąź. Wszelkie zmiany wprowadzamy na wydzielonych gałęziach kodu. Tak jak liście na drzewie, tak zmiany na różnych branchach repozytorium są całkowicie niezależne. Dzięki temu unikamy konfliktów.
Aby stworzyć nowy branch użyj `git branch --track [nazwa Twojego brancha] origin/main`. Aby przełączać się między branchami, użyj `git checkout [nazwa brancha docelowego]`. Idealny schemat wygląda tak: jesteś na `main`, tworzysz nowego brancha, wykonujesz zadanie, commitujesz, pushujesz. Wówczas w zakładce Pull requests na stronie repozytorium pojawi się możliwość utworzenia pull requestu. Posługujemy się pull requestami, żeby mieć możliwość weryfikacji tego, co wchodzi do finalnego produktu. Pull request jest "żądaniem", aby zmiany z Twojego brancha trafiły do głównego brancha. Na tym etapie nasi developerzy sprawdzą kod, ewentualnie wskażą co należy poprawić i dopiero po ich zatwierdzeniu możliwe jest wprowadzenie Twojego kodu. Ten ostatni krok, czyli połączenie kodu z różnych branchów, nazywamy *merge*.
*Co po udanym mergu? Jak zaktualizować lokalne repozytorium?*
Gdy uda się wprowadzić zmianę na branchu `main`, git nie pobierze automatycznie zmian u każdego użytkownika. Jest to przemyślane rozwiązanie - gdy coś testujemy na ustalonej wersji oprogramowania, takie nikczemne działania pod stołem ze strony gita mogłyby nam nieco namieszać.
Aby zaktualizować lokalne repozytorium, tj. lokalną gałąź main, musisz się na niej znajdować (`git checkout master`), a następnie uruchomić dwa polecenia
```
git fetch
git pull
```
Pierwsze z nich zaciąga informacje o zmianach, które nastąpiły w chmurze (metadane). Drugie natomiast zaciąga najnowszą wersję wszystkich branchy w chmurze. Wyobraźmy sobie sytuację: pracuję nad zadaniem, ale kolega musi stworzyć nowy komponent dla mnie. Kolega stworzył komponent, udało się go zmergować do maina. Jak mam sprawić, żeby ten kod pojawił się także w branchu związanym z moim zadaniem? Tego typu sytuacja, gdzie nasz podstawowy branch ulega aktualizacji, a my tę aktualizację chcemy uwzględniać, określamy mianem rebase. Wygląda to tak:
```
git checkout main
git fetch
git pull
git checkout moje-zadanie-branch
git rebase master
```
W ten sposób upewniamy się, że nasze zmiany oparte są o najnowszą wersję kodu z maina.


### Inne przydatne rzeczy
Komenda `git status`, której poświęciliśmy tylko chwilę, bywa niezastąpiona. Poradnik będzie pewnie rozwijany w miarę pojawiających się problemów - na ten moment to jednak wszystko.


### FAQ
Puste - zadaj pytanie, by rozbudować tę sekcję!