# Wprowadzenie do Docker Compose

## Cel lekcji

W tej lekcji zapoznasz się z narzędziem Docker Compose, które pozwala na definiowanie i uruchamianie wielu kontenerów Docker w ramach jednej aplikacji. Nauczysz się, jak tworzyć pliki `docker-compose.yml`, jak uruchamiać aplikacje składające się z wielu kontenerów oraz jak zarządzać tymi kontenerami w sposób zautomatyzowany.

---

## Agenda

1. **Co to jest Docker Compose?**

   - Wprowadzenie do Docker Compose
   - Korzyści z używania Docker Compose w projekcie

2. **Instalacja Docker Compose**

   - Jak zainstalować Docker Compose na różnych systemach operacyjnych

3. **Podstawy pliku `docker-compose.yml`**

   - Struktura pliku `docker-compose.yml`
   - Definicja usług, sieci i woluminów

4. **Uruchamianie aplikacji za pomocą Docker Compose**

   - Komenda `docker-compose up`
   - Uruchamianie aplikacji w tle i w trybie interaktywnym

5. **Zarządzanie aplikacjami za pomocą Docker Compose**

   - Komenda `docker-compose down`
   - Komenda `docker-compose logs`

6. **Przykład aplikacji wielokontenerowej**
   - Tworzenie aplikacji składającej się z kontenera aplikacji i bazy danych

---

## Materiały lekcji

### 1. Co to jest Docker Compose?

Docker Compose to narzędzie umożliwiające definiowanie i uruchamianie aplikacji składających się z wielu kontenerów. Zamiast uruchamiać każdy kontener osobno, Docker Compose pozwala na zdefiniowanie wszystkich usług w jednym pliku konfiguracyjnym `docker-compose.yml`, który następnie uruchamia wszystkie kontenery w odpowiedniej kolejności.

Korzyści z używania Docker Compose:

- **Łatwość zarządzania**: Możliwość zarządzania wszystkimi kontenerami aplikacji za pomocą jednej komendy.
- **Skalowalność**: Proste skalowanie aplikacji poprzez uruchamianie wielu instancji kontenerów.
- **Izolacja**: Możliwość tworzenia izolowanych środowisk dla różnych aplikacji.

### 2. Instalacja Docker Compose

Docker Compose jest dostępny na różnych systemach operacyjnych, w tym Linux, macOS i Windows. Możesz zainstalować Docker Compose za pomocą poniższych komend:

#### Linux:

1. Pobierz najnowszą wersję Docker Compose:

   ```bash
   sudo curl -L "https://github.com/docker/compose/releases/download/$(curl -s https://api.github.com/repos/docker/compose/releases/latest | jq -r .tag_name)/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
   ```

2. Nadaj uprawnienia do wykonywania pliku:

   ```bash
   sudo chmod +x /usr/local/bin/docker-compose
   ```

#### macOS:

Na macOS Docker Compose jest częścią instalacji Docker Desktop, więc wystarczy zainstalować Docker Desktop, aby mieć dostęp do Docker Compose.

#### Windows:

Na Windows Docker Compose jest również częścią Docker Desktop, więc po zainstalowaniu Docker Desktop będziesz mógł korzystać z Docker Compose.

### 3. Podstawy pliku `docker-compose.yml`

Plik `docker-compose.yml` jest podstawowym plikiem konfiguracyjnym w Docker Compose. Definiuje on usługi, sieci i woluminy, które będą używane przez aplikację. Oto przykładowa struktura pliku:

```yaml
version: "3"
services:
  web:
    image: nginx
    ports:
      - "8080:80"
  db:
    image: postgres
    environment:
      POSTGRES_PASSWORD: example
```

W tym przykładzie:

- **version**: Określa wersję składni pliku Compose.
- **services**: Definiuje usługi, które będą uruchamiane w kontenerach. W tym przypadku mamy usługę `web` (z obrazem Nginx) i usługę `db` (z obrazem PostgreSQL).
- **ports**: Określa mapowanie portów między hostem a kontenerem.
- **environment**: Ustawia zmienne środowiskowe dla kontenera (w tym przypadku hasło dla bazy danych PostgreSQL).

### 4. Uruchamianie aplikacji za pomocą Docker Compose

Aby uruchomić aplikację zdefiniowaną w pliku `docker-compose.yml`, używamy komendy:

```bash
docker-compose up
```

Ta komenda uruchomi wszystkie usługi zdefiniowane w pliku Compose. Jeśli chcesz uruchomić aplikację w tle, użyj opcji `-d`:

```bash
docker-compose up -d
```

Aby zatrzymać aplikację, używamy komendy:

```bash
docker-compose down
```

### 5. Zarządzanie aplikacjami za pomocą Docker Compose

Docker Compose oferuje kilka przydatnych komend do zarządzania aplikacjami:

- **Zobacz logi aplikacji**:

  ```bash
  docker-compose logs
  ```

- **Zatrzymaj aplikację**:

  ```bash
  docker-compose down
  ```

- **Skalowanie aplikacji (np. uruchomienie 3 instancji kontenera)**:

  ```bash
  docker-compose up --scale web=3
  ```

### 6. Przykład aplikacji wielokontenerowej

Przykład aplikacji, która korzysta z dwóch kontenerów: aplikacji webowej i bazy danych. W tym przypadku używamy Nginx jako serwera WWW oraz PostgreSQL jako bazy danych:

```yaml
version: "3"
services:
  web:
    image: nginx
    ports:
      - "8080:80"
  db:
    image: postgres
    environment:
      POSTGRES_PASSWORD: example
```

W tym przykładzie uruchamiamy aplikację z dwoma kontenerami: jednym dla Nginx i drugim dla PostgreSQL.
