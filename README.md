# Instalacja Dockera i podstawowe komendy

## Cel lekcji

W tej lekcji nauczysz się, jak zainstalować Docker na różnych systemach operacyjnych, oraz jak uruchomić pierwsze kontenery. Przeprowadzimy Cię przez proces instalacji na systemach Windows, macOS i Linux, a także omówimy podstawowe komendy, które pozwolą Ci zacząć korzystać z Dockera.

---

## Agenda

1. **Instalacja Dockera na różnych systemach operacyjnych**

   - Instalacja na Windows
   - Instalacja na macOS
   - Instalacja na Linux (Ubuntu)

2. **Podstawowe komendy Dockera**

   - Sprawdzanie wersji Dockera
   - Uruchamianie kontenerów
   - Wyświetlanie uruchomionych kontenerów
   - Zatrzymywanie i uruchamianie kontenerów
   - Usuwanie kontenerów

3. **Pierwszy kontener w Dockerze**
   - Uruchamianie kontenera z oficjalnego obrazu (np. `hello-world`)
   - Zrozumienie działania polecenia uruchamiania kontenerów
   - Jak sprawdzić, czy kontener działa poprawnie

---

## Materiały lekcji

### Instalacja Dockera

Docker jest dostępny na systemy Windows, macOS i Linux. Poniżej znajdują się instrukcje instalacji dla każdego z systemów:

#### Windows

1. Pobierz Docker Desktop z oficjalnej strony: [Docker Desktop dla Windows](https://www.docker.com/products/docker-desktop)
2. Zainstaluj Docker Desktop, postępując zgodnie z instrukcjami instalatora.
3. Po zakończeniu instalacji uruchom Docker Desktop.
4. Sprawdź, czy Docker działa poprawnie, sprawdzając wersję w terminalu.

#### macOS

1. Pobierz Docker Desktop z oficjalnej strony: [Docker Desktop dla macOS](https://www.docker.com/products/docker-desktop)
2. Zainstaluj aplikację, przeciągając ikonę do folderu "Aplikacje".
3. Po zakończeniu instalacji uruchom Docker Desktop.
4. Sprawdź wersję Dockera, aby upewnić się, że jest zainstalowany poprawnie.

#### Linux (Ubuntu)

1. Zainstaluj Docker za pomocą następujących poleceń:

   - Zaktualizuj listę pakietów i zainstaluj wymagane zależności.
   - Dodaj klucz GPG dla oficjalnego repozytorium Dockera.
   - Zainstaluj Docker.

2. Sprawdź, czy instalacja powiodła się, sprawdzając wersję Dockera.

### Podstawowe komendy Dockera

W tej części omówimy najważniejsze komendy, które pozwolą Ci rozpocząć pracę z Dockerem:

- **Sprawdzanie wersji Dockera**  
  Aby upewnić się, że Docker został zainstalowany poprawnie, możesz sprawdzić jego wersję. Dzięki temu dowiesz się, czy masz najnowszą wersję Dockera.

- **Uruchamianie kontenerów**  
  Docker umożliwia uruchamianie aplikacji w kontenerach. Możesz używać gotowych obrazów z Docker Hub lub tworzyć własne obrazy. Uruchomienie kontenera pozwala na uruchomienie aplikacji w odizolowanym środowisku.

- **Wyświetlanie uruchomionych kontenerów**  
  Po uruchomieniu kontenera możesz sprawdzić, które kontenery są aktualnie aktywne. Dzięki tej komendzie będziesz mógł monitorować działające kontenery.

- **Zatrzymywanie i uruchamianie kontenerów**  
  Docker pozwala na zatrzymywanie i uruchamianie kontenerów w razie potrzeby. Możesz zatrzymać kontener, jeśli nie jest już potrzebny, lub uruchomić go ponownie w razie potrzeby.

- **Usuwanie kontenerów**  
  Jeśli kontener nie jest już potrzebny, możesz go usunąć, aby zwolnić zasoby systemowe.

### Pierwszy kontener w Dockerze

Aby zobaczyć Docker w akcji, uruchomimy pierwszy kontener z oficjalnego obrazu `hello-world`. Jest to bardzo prosty obraz, który wyświetla powitalny komunikat, jeśli Docker jest poprawnie zainstalowany. Jest to pierwszy krok do uruchamiania bardziej zaawansowanych aplikacji w kontenerach.
