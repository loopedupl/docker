# Sieci w Dockerze

## Cel lekcji

W tej lekcji nauczysz się, jak Docker zarządza sieciami, jak tworzyć i konfigurować różne typy sieci, oraz jak komunikować się między kontenerami w ramach tych sieci. Dowiesz się, jak Docker umożliwia izolację i kontrolę nad ruchem sieciowym, co jest kluczowe w aplikacjach produkcyjnych.

---

## Agenda

1. **Wprowadzenie do sieci w Dockerze**

   - Co to są sieci w Dockerze?
   - Jak Docker zarządza sieciami?
   - Typy sieci w Dockerze

2. **Domyślna sieć w Dockerze**

   - Sieć bridge
   - Sieć host
   - Sieć none

3. **Tworzenie własnych sieci**

   - Komenda `docker network create`
   - Tworzenie sieci typu bridge
   - Tworzenie sieci typu overlay

4. **Łączenie kontenerów z sieciami**

   - Podłączanie kontenerów do sieci
   - Komunikacja między kontenerami w tej samej sieci

5. **Sieci w trybie multi-host**

   - Sieci overlay w Docker Swarm
   - Konfiguracja komunikacji między kontenerami na różnych hostach

6. **Zarządzanie sieciami**
   - Sprawdzanie dostępnych sieci
   - Usuwanie sieci
   - Przykłady poleceń

---

## Materiały lekcji

### 1. Wprowadzenie do sieci w Dockerze

Docker pozwala na tworzenie i zarządzanie sieciami, które umożliwiają kontenerom komunikację ze sobą i z zewnętrznym światem. Docker domyślnie tworzy kilka typów sieci, a także pozwala na tworzenie własnych sieci, które mogą mieć różne właściwości.

#### Typy sieci w Dockerze:

- **Bridge**: Jest to domyślny typ sieci dla kontenerów. Każdy kontener podłączony do sieci bridge otrzymuje własny adres IP w tej sieci, ale może komunikować się z innymi kontenerami w tej samej sieci.
- **Host**: Kontener podłączony do sieci host będzie używał adresu IP hosta, co umożliwia bezpośrednią komunikację z siecią hosta.
- **None**: Kontener nie ma przypisanej żadnej sieci. Używane w specyficznych przypadkach, gdy kontener nie powinien mieć dostępu do sieci.

### 2. Domyślna sieć w Dockerze

#### Sieć bridge

Jest to domyślna sieć, którą Docker tworzy podczas instalacji. Kontenery podłączone do tej sieci mają własny adres IP, ale mogą komunikować się z innymi kontenerami w tej samej sieci.

#### Sieć host

Kontener podłączony do sieci host będzie używał adresu IP hosta. Jest to przydatne, gdy kontener musi mieć bezpośredni dostęp do portów hosta, na przykład w przypadku aplikacji serwerowych.

#### Sieć none

W tej sieci kontener nie ma przypisanego adresu IP i nie może komunikować się z żadną inną siecią.

### 3. Tworzenie własnych sieci

Aby utworzyć własną sieć, używamy komendy `docker network create`. Przykład tworzenia sieci typu bridge:

```bash
docker network create --driver bridge my_custom_network
```

Dzięki tej komendzie tworzymy sieć typu bridge o nazwie `my_custom_network`.

#### Tworzenie sieci typu overlay

Sieci typu overlay są wykorzystywane w Docker Swarm, aby kontenery na różnych hostach mogły się ze sobą komunikować. Tworzymy je w sposób podobny do sieci bridge:

```bash
docker network create --driver overlay my_overlay_network
```

### 4. Łączenie kontenerów z sieciami

Aby podłączyć kontener do sieci, używamy opcji `--network` podczas uruchamiania kontenera. Przykład:

```bash
docker run -d --name my_container --network my_custom_network my_image
```

Kontener `my_container` zostanie podłączony do sieci `my_custom_network`.

### 5. Sieci w trybie multi-host

W przypadku Docker Swarm możemy tworzyć sieci typu overlay, które umożliwiają kontenerom uruchomionym na różnych hostach komunikację ze sobą. W Swarmie sieci overlay są automatycznie rozciągane na wszystkie węzły klastra.

### 6. Zarządzanie sieciami

Aby sprawdzić dostępne sieci, używamy komendy:

```bash
docker network ls
```

Aby usunąć sieć, używamy komendy:

```bash
docker network rm my_custom_network
```
