# Wstęp do konteneryzacji i Dockera

## Cel lekcji

W tej lekcji poznasz podstawy konteneryzacji oraz dowiesz się, czym jest Docker. Omówimy również, jakie problemy rozwiązuje konteneryzacja i dlaczego jest to kluczowa technologia w nowoczesnym tworzeniu oprogramowania.

---

## Agenda

1. **Wprowadzenie do konteneryzacji**

   - Co to jest kontener?
   - Różnice między maszynami wirtualnymi a kontenerami.
   - Zalety konteneryzacji: izolacja, przenośność, skalowalność.

2. **Docker jako platforma konteneryzacyjna**

   - Czym jest Docker?
   - Historia i rozwój Dockera.
   - Główne komponenty Dockera: obrazy, kontenery, rejestry.

3. **Przykłady zastosowania Dockera**
   - Tworzenie środowisk deweloperskich.
   - Uruchamianie aplikacji w kontenerach.
   - Skalowanie aplikacji w środowiskach produkcyjnych.

---

## Co to jest kontener?

Kontener to lekkie, przenośne środowisko, które zawiera aplikację oraz wszystkie jej zależności, takie jak biblioteki czy konfiguracje. Dzięki temu aplikacje działają w sposób przewidywalny niezależnie od środowiska, w którym są uruchamiane.

### Różnice między kontenerami a maszynami wirtualnymi

| **Cecha**             | **Kontenery**                 | **Maszyny wirtualne**            |
| --------------------- | ----------------------------- | -------------------------------- |
| Wydajność             | Bardzo wysoka, niskie narzuty | Mniejsze niż natywne środowisko  |
| Rozmiar               | Kilkadziesiąt MB              | Kilka GB                         |
| Szybkość uruchamiania | Kilka sekund                  | Kilka minut                      |
| Zależności od systemu | Niskie                        | Wyższe (pełny system operacyjny) |

---

## Czym jest Docker?

Docker to platforma konteneryzacyjna, która pozwala na tworzenie, uruchamianie i zarządzanie kontenerami. Docker upraszcza proces tworzenia środowisk i uruchamiania aplikacji w sposób powtarzalny.

### Główne komponenty Dockera:

- **Obrazy Dockera**: To szablony zawierające aplikację i jej zależności.
- **Kontenery Dockera**: To działające instancje obrazów Dockera.
- **Rejestry Dockera**: To miejsca, gdzie przechowywane są obrazy (np. Docker Hub).

---

## Przykłady zastosowania Dockera

1. **Tworzenie środowisk deweloperskich**  
   Dzięki Dockerowi możesz szybko stworzyć środowisko, które będzie identyczne jak na produkcji.
2. **Uruchamianie aplikacji w kontenerach**  
   Docker umożliwia uruchamianie aplikacji w izolacji, co eliminuje problemy związane z konfliktem zależności.

3. **Skalowanie aplikacji**  
   Kontenery są lekkie i łatwe do replikowania, co pozwala na skalowanie aplikacji w środowiskach produkcyjnych.
