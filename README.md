# Debugowanie kontenerów

## Cel lekcji

W tej lekcji nauczysz się, jak efektywnie diagnozować i rozwiązywać problemy z kontenerami Dockera. Dowiesz się, jak monitorować logi, uzyskiwać dostęp do wnętrza kontenera, analizować jego stan oraz identyfikować potencjalne przyczyny błędów.

---

## Agenda

1. **Dlaczego debugowanie kontenerów jest ważne?**

   - Typowe problemy w środowiskach kontenerowych
   - Wpływ błędów na produkcję i procesy CI/CD

2. **Podstawowe narzędzia do debugowania w Dockerze**

   - Komendy `docker logs`, `docker ps`, `docker inspect`
   - Analiza stanu kontenera

3. **Dostęp do wnętrza kontenera**

   - Użycie komendy `docker exec`
   - Praktyczne przykłady

4. **Debugowanie problemów z siecią w kontenerach**

   - Sprawdzanie konfiguracji sieciowej kontenera
   - Testowanie połączeń z użyciem `curl` i `ping`

5. **Diagnostyka problemów z woluminami**

   - Weryfikacja poprawności montowania danych
   - Sprawdzanie uprawnień i dostępu

6. **Zaawansowane narzędzia do debugowania**

   - Użycie narzędzi takich jak `ctop` i `sysdig`
   - Analiza zasobów kontenera (CPU, RAM)

7. **Praktyczne scenariusze debugowania**
   - Rozwiązywanie problemów z uruchomieniem kontenera
   - Diagnoza błędów aplikacji wewnątrz kontenera

---

## Materiały lekcji

### 1. Dlaczego debugowanie kontenerów jest ważne?

Debugowanie kontenerów pozwala na szybkie i efektywne rozwiązywanie problemów, co jest kluczowe w środowiskach produkcyjnych. Typowe błędy, które mogą wystąpić:

- Kontener nie uruchamia się poprawnie.
- Aplikacja wewnątrz kontenera działa nieprawidłowo.
- Problemy z siecią lub dostępem do danych.

### 2. Podstawowe narzędzia do debugowania w Dockerze

- **`docker logs`**: Wyświetla logi kontenera.  
  Przykład:
  ```bash
  docker logs <container_id>
  ```
- **`docker ps`**: Wyświetla listę działających kontenerów.  
  Przykład:
  ```bash
  docker ps -a
  ```
- **`docker inspect`**: Zwraca szczegółowe informacje o kontenerze.  
  Przykład:
  ```bash
  docker inspect <container_id>
  ```

### 3. Dostęp do wnętrza kontenera

Czasami konieczne jest wejście do kontenera, aby sprawdzić pliki lub uruchomić dodatkowe komendy.  
Przykład:

```bash
docker exec -it <container_id> /bin/bash
```

### 4. Debugowanie problemów z siecią w kontenerach

Jeśli aplikacja w kontenerze ma problemy z komunikacją, warto sprawdzić:

- **Sieć kontenera**:
  ```bash
  docker network inspect <network_name>
  ```
- **Połączenia wewnętrzne**:  
  Użyj `ping` lub `curl` do testowania połączeń.

### 5. Diagnostyka problemów z woluminami

Problemy z woluminami często wynikają z:

- Nieprawidłowego montowania ścieżek.
- Braku odpowiednich uprawnień.

Sprawdź zamontowane woluminy:

```bash
docker inspect <container_id> | grep Mounts
```

### 6. Zaawansowane narzędzia do debugowania

- **`ctop`**: Monitoruje zasoby używane przez kontenery (CPU, RAM).
- **`sysdig`**: Analizuje zachowanie systemu i kontenerów.

### 7. Praktyczne scenariusze debugowania

**Scenariusz 1**: Kontener nie uruchamia się.

- Sprawdź logi:
  ```bash
  docker logs <container_id>
  ```
- Sprawdź konfigurację obrazu:
  ```bash
  docker inspect <image_name>
  ```

**Scenariusz 2**: Aplikacja w kontenerze nie działa.

- Wejdź do kontenera:
  ```bash
  docker exec -it <container_id> /bin/bash
  ```
- Sprawdź logi aplikacji wewnątrz kontenera.
