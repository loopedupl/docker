# Zarządzanie woluminami w Dockerze

## Cel lekcji

W tej lekcji dowiesz się, czym są woluminy w Dockerze, jak je tworzyć, zarządzać nimi oraz wykorzystywać je do przechowywania danych w kontenerach. Nauczysz się, jak używać woluminów, aby dane były przechowywane niezależnie od życia kontenera, co jest kluczowe w przypadku aplikacji produkcyjnych.

---

## Agenda

1. **Co to są woluminy w Dockerze?**

   - Definicja woluminów
   - Różnica między woluminami a bind mounts
   - Kiedy używać woluminów

2. **Tworzenie woluminów**

   - Komenda `docker volume create`
   - Sprawdzanie dostępnych woluminów
   - Przykład tworzenia woluminu

3. **Używanie woluminów w kontenerach**

   - Montowanie woluminów w kontenerach
   - Przykład uruchamiania kontenera z woluminem

4. **Zarządzanie woluminami**

   - Usuwanie woluminów
   - Przykład usuwania woluminu
   - Sprawdzanie informacji o woluminach

5. **Przechowywanie danych w woluminach**
   - Przechowywanie danych aplikacji
   - Jak zapewnić trwałość danych w kontenerach

---

## Materiały lekcji

### 1. Co to są woluminy w Dockerze?

Woluminy w Dockerze to specjalne obiekty służące do przechowywania danych, które są niezależne od cyklu życia kontenera. Woluminy mogą być używane do przechowywania danych, które muszą być trwałe, takich jak bazy danych, pliki konfiguracyjne, logi, itp.

#### Różnica między woluminami a bind mounts

- **Woluminy**: Przechowywane są przez Docker w zarządzanym obszarze na hoście. Są niezależne od kontenera i mogą być łatwo przenoszone między kontenerami.
- **Bind mounts**: Używają lokalnych ścieżek na hoście, co oznacza, że dane są bezpośrednio związane z systemem plików hosta.

### 2. Tworzenie woluminów

Aby stworzyć wolumin, używamy komendy `docker volume create`. Na przykład:

```bash
docker volume create my_volume
```

Ta komenda utworzy wolumin o nazwie `my_volume`, który będzie przechowywał dane.

Aby sprawdzić dostępne woluminy, używamy komendy:

```bash
docker volume ls
```

### 3. Używanie woluminów w kontenerach

Aby użyć woluminu w kontenerze, montujemy go do kontenera za pomocą opcji `-v` w komendzie `docker run`. Przykład:

```bash
docker run -d -v my_volume:/data my_image
```

W tym przypadku wolumin `my_volume` jest montowany do katalogu `/data` w kontenerze.

### 4. Zarządzanie woluminami

#### Usuwanie woluminów

Aby usunąć wolumin, używamy komendy:

```bash
docker volume rm my_volume
```

Jeśli wolumin jest wciąż używany przez kontener, Docker nie pozwoli na jego usunięcie. Możemy sprawdzić, które kontenery używają woluminów, używając:

```bash
docker ps -a --filter volume=my_volume
```

#### Sprawdzanie informacji o woluminach

Aby uzyskać szczegóły na temat woluminu, możemy użyć komendy:

```bash
docker volume inspect my_volume
```

### 5. Przechowywanie danych w woluminach

Woluminy są idealnym rozwiązaniem do przechowywania danych, które muszą przetrwać restart kontenera. Przykładem może być baza danych, której dane nie powinny zostać utracone po usunięciu kontenera.

Aby zapewnić trwałość danych w kontenerze, warto zawsze używać woluminów do przechowywania plików aplikacji, logów czy konfiguracji. Dzięki temu dane nie zostaną utracone w przypadku, gdy kontener zostanie usunięty lub zrestartowany.
