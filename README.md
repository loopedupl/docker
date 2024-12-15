# Podstawowe komendy Dockera

## Cel lekcji

W tej lekcji nauczysz się, jak korzystać z podstawowych komend Docker, które umożliwiają zarządzanie kontenerami i obrazami. Omówimy komendy do uruchamiania, zatrzymywania, usuwania kontenerów oraz zarządzania obrazami.

---

## Agenda

1. **Podstawowe komendy Docker**

   - `docker --version` - sprawdzenie wersji Dockera
   - `docker run` - uruchamianie kontenerów
   - `docker ps` - wyświetlanie uruchomionych kontenerów
   - `docker stop` - zatrzymywanie kontenerów
   - `docker rm` - usuwanie kontenerów
   - `docker images` - wyświetlanie dostępnych obrazów
   - `docker rmi` - usuwanie obrazów

2. **Zarządzanie kontenerami**

   - Uruchamianie kontenerów w tle
   - Łączenie z kontenerem za pomocą `docker exec`
   - Sprawdzanie logów kontenerów

3. **Zarządzanie obrazami**
   - Pobieranie obrazów z Docker Hub
   - Tworzenie własnych obrazów
   - Tagowanie obrazów

---

## Materiały lekcji

### 1. Podstawowe komendy Docker

#### `docker --version`

Komenda ta pozwala na sprawdzenie wersji zainstalowanego Dockera. Jest to przydatne, aby upewnić się, że masz najnowszą wersję Dockera, szczególnie jeśli instalujesz go po raz pierwszy.

```bash
docker --version
```

#### `docker run`

Komenda `docker run` pozwala na uruchomienie kontenera z obrazu. Można ją wykorzystać do uruchamiania kontenerów w tle lub w trybie interaktywnym.

Przykład uruchomienia kontenera z obrazem `hello-world`:

```bash
docker run hello-world
```

#### `docker ps`

Komenda `docker ps` wyświetla listę aktualnie uruchomionych kontenerów. Możesz również dodać flagę `-a`, aby zobaczyć również kontenery, które zostały zatrzymane.

```bash
docker ps
docker ps -a
```

#### `docker stop`

Komenda `docker stop` pozwala na zatrzymanie uruchomionego kontenera. Aby zatrzymać kontener, wystarczy podać jego ID lub nazwę.

```bash
docker stop <container_id>
```

#### `docker rm`

Komenda `docker rm` pozwala na usunięcie zatrzymanego kontenera. Należy pamiętać, że kontener musi być zatrzymany przed jego usunięciem.

```bash
docker rm <container_id>
```

#### `docker images`

Komenda `docker images` wyświetla listę dostępnych obrazów na lokalnym systemie. Możesz zobaczyć nazwę obrazu, jego tag oraz rozmiar.

```bash
docker images
```

#### `docker rmi`

Komenda `docker rmi` pozwala na usunięcie obrazu Docker z lokalnego systemu.

```bash
docker rmi <image_id>
```

### 2. Zarządzanie kontenerami

#### Uruchamianie kontenerów w tle

Możesz uruchomić kontener w tle, dodając flagę `-d` do komendy `docker run`. To pozwala na uruchomienie kontenera bez blokowania terminala.

```bash
docker run -d <image_name>
```

#### Łączenie z kontenerem za pomocą `docker exec`

Komenda `docker exec` pozwala na uruchamianie komend wewnątrz działającego kontenera. Można jej używać do debugowania lub interakcji z aplikacjami uruchomionymi w kontenerze.

Przykład uruchomienia powłoki bash w kontenerze:

```bash
docker exec -it <container_id> bash
```

#### Sprawdzanie logów kontenerów

Komenda `docker logs` pozwala na wyświetlenie logów z kontenera. To przydatne narzędzie do monitorowania działania aplikacji w kontenerze.

```bash
docker logs <container_id>
```

### 3. Zarządzanie obrazami

#### Pobieranie obrazów z Docker Hub

Możesz pobrać obraz z publicznego repozytorium Docker Hub za pomocą komendy `docker pull`. Na przykład, aby pobrać obraz `nginx`, używamy:

```bash
docker pull nginx
```

#### Tworzenie własnych obrazów

Kiedy masz aplikację, którą chcesz uruchomić w Dockerze, musisz stworzyć własny obraz. W tym celu tworzysz plik `Dockerfile`, który zawiera instrukcje budowania obrazu. Więcej na ten temat w kolejnych lekcjach.

#### Tagowanie obrazów

Tagowanie obrazów pozwala na nadanie im łatwego do rozpoznania identyfikatora. Można to zrobić za pomocą komendy `docker tag`.
