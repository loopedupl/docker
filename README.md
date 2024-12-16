# Tworzenie aplikacji wielokontenerowej

## Cel lekcji

W tej lekcji nauczysz się, jak zbudować i uruchomić aplikację składającą się z wielu kontenerów Docker, współpracujących ze sobą. Poznasz, jak używać Docker Compose do definiowania usług, sieci i woluminów, aby tworzyć skalowalne i modularne aplikacje.

---

## Agenda

1. **Dlaczego warto używać aplikacji wielokontenerowych?**

   - Zalety modularności
   - Przykłady zastosowań (np. aplikacje webowe z bazą danych)

2. **Definiowanie aplikacji wielokontenerowej w Docker Compose**

   - Usługi (services)
   - Sieci (networks)
   - Woluminy (volumes)

3. **Praktyczny przykład aplikacji wielokontenerowej**

   - Aplikacja webowa z serwerem Nginx i bazą danych PostgreSQL

4. **Uruchamianie aplikacji wielokontenerowej**

   - Komenda `docker-compose up`
   - Sprawdzanie statusu kontenerów (`docker-compose ps`)

5. **Testowanie komunikacji między kontenerami**

   - Pingowanie kontenerów
   - Łączenie się z bazą danych z aplikacji

6. **Zarządzanie aplikacją wielokontenerową**
   - Restartowanie usług
   - Aktualizowanie konfiguracji w pliku `docker-compose.yml`

---

## Materiały lekcji

### 1. Dlaczego warto używać aplikacji wielokontenerowych?

Aplikacje wielokontenerowe pozwalają na rozdzielenie różnych komponentów aplikacji na osobne kontenery. Przykładowo, aplikacja webowa może działać w jednym kontenerze, a baza danych w innym. Dzięki temu:

- **Modularność**: Każdy komponent może być rozwijany, testowany i skalowany niezależnie.
- **Izolacja**: Problemy w jednym kontenerze nie wpływają na działanie innych.
- **Łatwość wdrażania**: Używając Docker Compose, możemy uruchomić całą aplikację za pomocą jednej komendy.

### 2. Definiowanie aplikacji wielokontenerowej w Docker Compose

W pliku `docker-compose.yml` definiujemy usługi, które będą działały w naszej aplikacji. Przykładowa struktura:

```yaml
version: "3"
services:
  web:
    image: nginx
    ports:
      - "8080:80"
    networks:
      - app_network

  db:
    image: postgres
    environment:
      POSTGRES_PASSWORD: example
    volumes:
      - db_data:/var/lib/postgresql/data
    networks:
      - app_network

networks:
  app_network:

volumes:
  db_data:
```

W tym przykładzie:

- **web**: Usługa Nginx obsługująca ruch HTTP.
- **db**: Usługa PostgreSQL jako baza danych.
- **networks**: Definiujemy sieć, aby kontenery mogły się komunikować.
- **volumes**: Wolumin przechowujący dane bazy danych.

### 3. Praktyczny przykład aplikacji wielokontenerowej

Przykład aplikacji webowej z serwerem Nginx i bazą danych PostgreSQL:

1. **Plik `docker-compose.yml`**:

   ```yaml
   version: "3"
   services:
     web:
       image: nginx
       ports:
         - "8080:80"
       networks:
         - app_network

     db:
       image: postgres
       environment:
         POSTGRES_PASSWORD: example
       networks:
         - app_network

   networks:
     app_network:
   ```

2. **Tworzenie plików aplikacji**:
   - Stwórz plik `index.html` i umieść go w katalogu, który Nginx będzie serwował.
   - Skonfiguruj bazę danych PostgreSQL za pomocą zmiennych środowiskowych.

### 4. Uruchamianie aplikacji wielokontenerowej

Uruchom aplikację za pomocą komendy:

```bash
docker-compose up
```

Sprawdź status kontenerów:

```bash
docker-compose ps
```

Aby zatrzymać aplikację, użyj:

```bash
docker-compose down
```

### 5. Testowanie komunikacji między kontenerami

Możesz przetestować, czy kontenery komunikują się ze sobą, używając polecenia `ping`:

1. Wejdź do kontenera Nginx:

   ```bash
   docker exec -it <container_id> bash
   ```

2. Spróbuj pingować kontener bazy danych:

   ```bash
   ping db
   ```

Jeśli komunikacja działa, zobaczysz odpowiedzi.

### 6. Zarządzanie aplikacją wielokontenerową

- Aby zrestartować konkretną usługę, użyj:

  ```bash
  docker-compose restart web
  ```

- Aby dodać nową konfigurację, zaktualizuj plik `docker-compose.yml`, a następnie uruchom:

  ```bash
  docker-compose up -d
  ```
