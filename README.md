# RWMS - Magazine manager 

## Opis projektu

RWMS (Reliable Warehouse Management System) to system informatyczny przeznaczony do zarządzania procesami magazynowymi.
Głównym założeniem projektu jest obsługa przepływu towarów w magazynie – od momentu przyjęcia dostawy, przez składowanie i kompletację zamówienia, aż po kontrolę oraz wysyłkę towaru do klienta.
System ma na celu uporządkowanie i usprawnienie procesów magazynowych, zapewnienie kontroli nad przepływem produktów oraz ułatwienie pracy poszczególnym działom magazynu.

## Warstwa technologoczina

1. C# – główny język programowania.
2. .NET – platforma do tworzenia aplikacji.
3. Blazor – technologia interfejsu użytkownika.
4. PostgreSQL – relacyjna baza danych.
5. Entity Framework Core – komunikacja z bazą danych.
6. Docker – konteneryzacja i zarządzanie środowiskiem.
7. Git / GitHub – kontrola wersji i współpraca zespołowa.

## Architektura systemu

Projekt będzie rozwijany w oparciu o podział na warstwy odpowiedzialne za poszczególne obszary działania aplikacji.
Frontend – interfejs użytkownika, prezentacja danych i obsługa interakcji.
Backend – logika biznesowa, przetwarzanie danych i realizacja operacji magazynowych.
Baza danych – przechowywanie i zarządzanie informacjami systemowymi.
Warstwa komunikacyjna – wymiana danych pomiędzy frontendem a backendem za pomocą API.

##Główne procesy magazynowe

Dostawa – przyjęcie towaru dostarczonego przez klienta lub dostawcę.
Weryfikacja dostawy – sprawdzenie zgodności i kompletności otrzymanego towaru.
Magazynowanie – przekazanie zweryfikowanego towaru do odpowiedniego miejsca w magazynie.
Kompletacja – przygotowanie produktów na podstawie zamówienia klienta.
Kontrola – sprawdzenie kompletności zamówienia oraz przygotowanie go do wysyłki.
Wysyłka – przekazanie przygotowanego towaru przewoźnikowi w celu dostarczenia pod wskazany adres.

##Dashboard – podgląd najważniejszych informacji i aktywności magazynu.

Produkty – zarządzanie asortymentem.
Dostawy – obsługa przyjęć towarów.
Magazyn – zarządzanie lokalizacjami, paletami i stanami magazynowymi.
Zamówienia – obsługa zamówień klientów.
Kompletacja – przygotowywanie towarów do realizacji zamówień.
Kontrola jakości – weryfikacja przygotowanych zamówień.
Wysyłka – obsługa wydań i transportu towarów.
Historia operacji – rejestrowanie i przegląd wykonanych działań.

##Założenia projektowe

obiektowe podejście do programowania w C#;
prawidłowe odwzorowanie procesów magazynowych w strukturze klas;
odpowiedzialny podział logiki pomiędzy poszczególne warstwy;
integralność i spójność danych;
czytelność oraz łatwość utrzymania kodu;
poprawna komunikacja pomiędzy komponentami aplikacji.

## TODO tech
### Inicjalizacja projektu
- [ ] Inicjalizacja frontendu (Blazor)
- [ ] Inicjalizacja backendu (.NET / C#)
- [ ] Inicjalizacja bazy danych (PostgreSQL)
- [ ] Konfiguracja struktury projektu
- [ ] Konfiguracja zależności między projektami
- [ ] Konfiguracja kontenerów Docker
- [ ] Konfiguracja repozytorium Git

### Baza danych
- [ ] Zaprojektowanie schematu bazy danych
- [ ] Utworzenie schematu bazy danych
- [ ] Zdefiniowanie relacji między tabelami
- [ ] Konfiguracja Entity Framework Core
- [ ] Utworzenie początkowych migracji

### Backend
- [ ] Implementacja modeli i klas domenowych
- [ ] Implementacja logiki biznesowej
- [ ] Implementacja repozytoriów
- [ ] Implementacja serwisów
- [ ] Utworzenie endpointów REST API
- [ ] Implementacja walidacji danych
- [ ] Obsługa błędów i wyjątków

### Frontend
- [ ] Inicjalizacja aplikacji Blazor
- [ ] Utworzenie głównego układu aplikacji
- [ ] Implementacja nawigacji
- [ ] Utworzenie komponentów wielokrotnego użytku
- [ ] Implementacja dashboardu
- [ ] Implementacja widoku magazynu
- [ ] Implementacja widoku dostaw
- [ ] Implementacja widoku zamówień
- [ ] Implementacja widoku kompletacji
- [ ] Implementacja widoku kontroli jakości
- [ ] Implementacja widoku wysyłki
- [ ] Integracja frontendu z backendowym API

### Testowanie
- [ ] Konfiguracja środowiska testowego
- [ ] Implementacja testów jednostkowych
- [ ] Implementacja testów integracyjnych
- [ ] Testowanie endpointów API
- [ ] Testowanie operacji na bazie danych
- [ ] Testowanie procesów magazynowych

### Wdrożenie
- [ ] Konfiguracja środowiska produkcyjnego
- [ ] Konfiguracja kontenerów aplikacji
- [ ] Konfiguracja kontenera bazy danych
- [ ] Przygotowanie wdrożenia aplikacji
- [ ] Weryfikacja wersji produkcyjnej


## Procesy 
- [ ] Dostawa (Rampa 1/2/3/n) (dział dostaw)
- [ ] Rozwzenie po magazynie (Magazyn A, segment 1, p1)
- [ ] Dział kompletacji (Pobieranie z magazynu)
- [ ] Dział kontroli (Weryfikacja kompletnosci zamówienia + zapakowanie na palete)
- [ ] Rampa odbioru (Dostarczenie do rampy, ładunek na tira) 

## Database Schema

# Database Schema – RWMS

## 1. WarehouseLocation

- [ ] Id
- [ ] LocationCode
- [ ] Segment
- [ ] Rack
- [ ] Shelf
- [ ] LocationType (Standard / Oversized)
- [ ] IsOccupied (true / false)
- [ ] IsActive (true / false)
- [ ] CreatedAt

**Frontend:**
- Wyświetlanie lokalizacji, kodów i zajętości.
- Rozróżnianie lokalizacji Standard i Oversized.
- Informowanie o dostępności lokalizacji.

**Backend:**
- LocationCode musi być unikalny (element składowy segment (litera) + rack (liczba) + shelf (litera) = np. A003A.
- Jedna lokalizacja może przechowywać maksymalnie jedną paletę.
- IsOccupied aktualizowane automatycznie przy umieszczaniu i pobieraniu palety.
- Rack i Shelf mogą być puste dla lokalizacji podłogowych.
- IsActive określa, czy lokalizacja może być wykorzystywana.

## 2. Pallet

- [ ] Id
- [ ] PalletNumber (UNIQUE)
- [ ] WeightCategory (Light / Medium / Heavy)
- [ ] IsStandard (true / false)
- [ ] InboundDeliveryId
- [ ] WarehouseLocationId (nullable, UNIQUE)
- [ ] CustomerOrderId (nullable)
- [ ] Status (Received / Stored / Reserved / Picked / Shipped / Inactive)
- [ ] CreatedAt
- [ ] UpdatedAt

**Informacje dodatkowe:**

PalletNumber jest generowany automatycznie przez backend podczas rejestracji palety. Jest to unikalny, wewnętrzny numer magazynowy, którego użytkownik nie może ręcznie zmienić.

Format: RWMS-000001.

**Frontend:**
- Wyświetlanie numeru, kategorii wagowej, rozmiaru, statusu i lokalizacji palety.
- Wyszukiwanie palet po PalletNumber.
- Wybieranie konkretnych palet do zamówienia.

**Backend:**
- Automatyczne generowanie PalletNumber.
- Kontrola unikalności numeru palety.
- Jedna paleta może znajdować się maksymalnie w jednej lokalizacji.
- Jedna paleta może być przypisana maksymalnie do jednego aktywnego zamówienia.
- Kontrola zgodności rozmiaru i wagi palety z typem lokalizacji.
- Po wysłaniu paleta otrzymuje status Shipped, a jej lokalizacja zostaje zwolniona.
- Aktualizacja IsOccupied po zmianie lokalizacji palety.

## 3. InboundDelivery

- [ ] Id
- [ ] DeliveryNumber
- [ ] SupplierName
- [ ] DeliveryDate
- [ ] Status (Planned / InProgress / Completed / Cancelled)
- [ ] CreatedAt
- [ ] UpdatedAt

**Frontend:**
- Wyświetlanie i rejestrowanie dostaw.
- Dodawanie palet podczas przyjmowania dostawy.
- Wyświetlanie palet powiązanych z dostawą.

**Backend:**
- Powiązanie palet z dostawą przez InboundDeliveryId.
- Automatyczna aktualizacja statusu dostawy.
- Kontrola poprawności rejestrowanych palet.
- DeliveryDate wykorzystywane do ustalania kolejności FIFO (first in first out).

## 4. CustomerOrder

- [ ] Id
- [ ] OrderNumber
- [ ] CustomerName
- [ ] OrderDate
- [ ] DeliveryAddress
- [ ] Status (New / Processing / Picking / QualityControl / ReadyForShipment / Shipped / Cancelled)
- [ ] CreatedAt
- [ ] UpdatedAt

**Frontend:**
- Tworzenie i wyświetlanie zamówień.
- Wyszukiwanie dostępnych palet po PalletNumber.
- Ręczne wskazywanie konkretnych palet do zamówienia.
- Wyświetlanie palet przypisanych do zamówienia.

**Backend:**
- OrderNumber powinien być unikalny.
- Powiązanie palet z zamówieniem przez Pallet.CustomerOrderId.
- Blokowanie przypisania palety do więcej niż jednego aktywnego zamówienia.
- Kontrola dostępności i statusu wybranych palet.
- FIFO może podpowiadać najstarsze dostępne palety, ale ostateczny wybór należy do pracownika.
- Status zamówienia aktualizowany zgodnie z etapem realizacji.

## 5. PickingTask

- [ ] Id
- [ ] CustomerOrderId
- [ ] AssignedUserId
- [ ] Status (Pending / InProgress / Completed / Cancelled)
- [ ] CreatedAt
- [ ] StartedAt
- [ ] CompletedAt

**Frontend:**
- Wyświetlanie zadań kompletacji.
- Wyświetlanie przypisanego pracownika i zamówienia.
- Prezentowanie aktualnego statusu zadania.

**Backend:**
- Zadanie powiązane z konkretnym zamówieniem.
- Przypisanie pracownika odpowiedzialnego za realizację.
- Kontrola statusu zadania.
- Zapisywanie dat rozpoczęcia i zakończenia kompletacji.

## 6. PickingTaskPallet

- [ ] Id
- [ ] PickingTaskId
- [ ] PalletId
- [ ] WarehouseLocationId
- [ ] Status (Pending / Picked / Cancelled)
- [ ] PickedAt

**Frontend:**
- Wyświetlanie listy palet do pobrania.
- Wyświetlanie lokalizacji każdej palety.
- Oznaczanie pobranych palet.

**Backend:**
- Powiązanie palet z zadaniem kompletacji.
- Zapisywanie postępu pobierania palet.
- Aktualizacja statusu palety po pobraniu.
- WarehouseLocationId przechowuje lokalizację, z której paleta ma zostać pobrana w ramach zadania.
- W przypadku przeniesienia palety przed pobraniem należy zaktualizować lokalizację w zadaniu.

## 7. QualityControl

- [ ] Id
- [ ] CustomerOrderId
- [ ] CheckedByUserId
- [ ] Status (Pending / InProgress / Passed / Failed)
- [ ] InspectionDate
- [ ] Comments

**Frontend:**
- Wyświetlanie zamówień oczekujących na kontrolę.
- Formularz kontroli jakości.
- Wprowadzanie wyniku i komentarzy.

**Backend:**
- Kontrola jakości dotyczy całego zamówienia.
- Zapisywanie osoby przeprowadzającej kontrolę.
- Wynik Passed pozwala przejść do przygotowania wysyłki.
- Wynik Failed blokuje wysyłkę do czasu rozwiązania problemu.
- Aktualizacja statusu zamówienia.

## 8. Shipment

- [ ] Id
- [ ] ShipmentNumber
- [ ] CustomerOrderId (UNIQUE)
- [ ] CarrierId
- [ ] TrackingNumber
- [ ] ShipmentDate
- [ ] Status (Pending / Prepared / Shipped / Delivered / Cancelled)
- [ ] CreatedAt
- [ ] UpdatedAt

**Frontend:**
- Wyświetlanie i przygotowywanie wysyłek.
- Wybór przewoźnika.
- Wprowadzanie numeru śledzenia.
- Wyświetlanie statusu wysyłki.

**Backend:**
- Jedno zamówienie może mieć maksymalnie jedną wysyłkę.
- CustomerOrderId musi być wymagane i unikalne.
- Wysyłka możliwa po pozytywnej kontroli jakości.
- Palety należące do wysyłki ustalane są na podstawie CustomerOrderId i Pallet.CustomerOrderId.
- Po wysłaniu aktualizowane są statusy palet i zamówienia.

## 9. Carrier

- [ ] Id
- [ ] Name (nazwa przewoźnika)
- [ ] Contact (osoba kontaktowa)
- [ ] Phone (numer telefonu)
- [ ] Email (adres e-mail)
- [ ] IsActive (true / false)

**Frontend:**
- Wyświetlanie listy przewoźników.
- Formularz dodawania i edycji przewoźnika.
- Wybieranie przewoźnika podczas przygotowywania wysyłki.

**Backend:**
- Nieaktywny przewoźnik nie może być wybierany do nowych wysyłek.
- Dezaktywacja przewoźnika nie usuwa historii wcześniejszych wysyłek.

## 10. User

- [ ] Id
- [ ] FirstName
- [ ] LastName
- [ ] Email
- [ ] PasswordHash
- [ ] RoleId
- [ ] IsActive (true / false)
- [ ] CreatedAt

**Frontend:**
- Formularz logowania.
- Wyświetlanie danych użytkownika.
- Panel zarządzania użytkownikami.
- Zarządzanie kontami zgodnie z uprawnieniami.

**Backend:**
- Email musi być unikalny.
- Hasło przechowywane wyłącznie jako bezpieczny hash.
- Kontrola roli i uprawnień użytkownika.
- Nieaktywne konto nie może się zalogować.
- RoleId określa rolę użytkownika.

## 11. Role

- [ ] Id
- [ ] Name (Admin / Manager / Employee)
- [ ] Description

**Frontend:**
- Wyświetlanie roli użytkownika.
- Prezentowanie dostępnych funkcji zgodnie z uprawnieniami.

**Backend:**
- Admin – pełny dostęp administracyjny.
- Manager – dostęp do modułów operacyjnych i zarządzania uprawnieniami pracowników.
- Employee – dostęp zgodny z indywidualnie przydzielonymi uprawnieniami.
- Uprawnienia Admina i Managera obsługiwane bezpośrednio przez logikę backendu.

## 12. Permission

- [ ] Id
- [ ] Name (Dashboard / Delivery / Orders / Picking / QualityControl / Shipping)
- [ ] Description

**Frontend:**
- Wyświetlanie modułów dostępnych dla użytkownika.
- Ukrywanie niedostępnych modułów.

**Backend:**
- Kontrola dostępu do poszczególnych modułów i operacji.
- Weryfikacja uprawnień przy wykonywaniu operacji, nie tylko przy wyświetlaniu interfejsu.

## 13. UserPermission

- [ ] Id
- [ ] UserId
- [ ] PermissionId

**Ograniczenie bazy danych:**
- UserId + PermissionId (UNIQUE – unikalna para).

**Frontend:**
- Panel przydzielania uprawnień pracownikom.
- Wyświetlanie aktualnych uprawnień użytkownika.

**Backend:**
- Jeden użytkownik może mieć wiele uprawnień.
- To samo uprawnienie nie może być przypisane temu samemu użytkownikowi dwa razy.
- Kontrola uprawnień podczas korzystania z aplikacji.

---

## General Rules

- [ ] Wszystkie relacje między klasami realizowane przez klucze obce.
- [ ] Wszystkie identyfikatory Id generowane przez bazę danych.
- [ ] Ograniczenia UNIQUE stosowane dla pól wymagających unikalności.
- [ ] Backend odpowiada za walidację danych i logikę biznesową.
- [ ] Frontend odpowiada za prezentację danych i obsługę interfejsu.
- [ ] Dostęp do funkcji aplikacji kontrolowany po stronie backendu.
- [ ] Zmiany statusów muszą być zgodne z przebiegiem procesów magazynowych.
## Wstępny graf procesu

[Diagram](https://viewer.diagrams.net/?tags=%7B%7D&lightbox=1&highlight=0000ff&edit=_blank&layers=1&nav=1&dark=auto#R%3Cmxfile%3E%3Cdiagram%20name%3D%22Strona-1%22%20id%3D%22xA_3FEeRghN1ySeRGSQN%22%3E5VrbcqM4EP0aqnYfkuJiMH4cnOzs1Ga2UuvU7mTfZJCxbEAeIcfGXz8tJIxlYgfHJplLXoxa0Ejdp%2Ft0ixjOMF1%2FZGgx%2FUwjnBi2Ga0N58awbdvsDeBHSAopsSzbk5KYkUjJasGIbLASmkq6JBHOtRs5pQknC10Y0izDIddkiDG60m%2Bb0ER%2F6wLFuCEYhShpSv8jEZ9KqW%2F3a%2FmfmMTT6s2Wp3acoupmtZN8iiK62hE5t4YzZJRyeZWuhzgR1qvsIp%2F748DsdmEMZ7zNA%2BNilN4lG%2F8D%2Buvr8NPNv0X4z99XTlOLUpzzorIBx2uYC6Y8TUBgweVqSjgeLVAo7liB60GWc0bneEgTykCY0QzmgglJkj0RSkicwTCEN2KQB0%2BYcQIW%2F6AmUhJF4tUBo8sswmL5Jozksp5QslTLumc0BGgIU8doU2R0VcAgQ2I%2FbFPMjaFr%2BDaKNgSD6LO8aWkIM3lfl8LswQiNYWnbIcxt0CxdzmBjMRVGIMawZwwG6iXyLSgjOAXJnKaLBPMsLKalCeFaSBMiTDl0jMBZGfZQ4LBcVs6lrkVWrmdV5IVc4VzIfVfooJGYyedogzKxGRQxscNy42AlvN5xkfLyR0xTzJm4e7oDRE%2BhblWD1qlkVXQ6yvtIxUi8VVXDCC4Ukk5AldWTinHUCK4mzuiShfiIMr%2BBR6F2pIaU8SmNaYaS21q6h5z6njtKFwrCM8x5ofINWnKqAxxWyYov4vlrtxo%2BKnXl4GatjQo1ivAELRN%2Bh8Y4CVA4j8uVVBEgk02QiNl7FEUki8vnIE9uAc4RizE%2FYg%2Fbf977DCeIkyfd4MrVV%2Ba12bOsw%2B5W6u4pyXj9mNV3rs2dv54rNahk3nMHuka5dqVkD0PblZ4BK1fL9WhcAcJsousoLvewVHpL9%2F8JSQrnZKOWIhCwELsv7eEGhnsDEpJNMSP8ocyipfbzUbKTBh8gI7EyeYhwx6yYkDkKZ0TscyHz0CyjItUMgpDI5IghwxQrmWNmOBcuj8TjMBPCBMm5zH%2FpNmm2TEEvgNDa5hwFIftkSA58%2FRE6meS4E7j5bbgR9EApgg9w4g6igP4X%2BFOWQzmjJA1PAlMhSQmlP3KOVq%2FK%2FX4z91u2nvstS%2FeDU9Vbl%2BcC84JcMHgPLjgnWvGa8C8VU8D1Y00pMKpJRAwqDtlyj6UxT01EB7inJX%2B8jj5cz%2BufGqvOYA9kzh5fSH83%2BKKhCDL8MR6yenvg7ZqH7HN5yHwWxz82D3HFQ4pPdJbxElFfj0WtHctK20OpyJDZOBc%2FURds49m%2BhpOr3qkIvqpSaaWh6l67Z59BG%2FbRc9sLDNSsHIjw16ZsqcF3ZVNTdiCyh0GvIp9nGo998nFN3aqO3Rn59C9IPvYv04lsWWvLVI%2FVag6yVkv2sbzTQxnqRt880qsebF40lLkt2ediLOGfyxL9n5AlHnSWUGcoVPUi8vCGRqL0LU9JEmhFCnlaoo5zMjxT7LJ5RaY6DjOn399L96eDztY1WHsquiMM%2B5KFtuX9Krmubd4anACoy%2FOY16Ya6KwXVVEqTxXepiH19rP1xWxZlXCXiZN36Ui%2F4zix3XeNk1ZVc4dxAuamyZsFSd%2FvLEiOxMR3%2F2Hofzxmsp6oelJRLqzKM9BgSBunnrUPl%2Bc60Xnms0uVcLYnmHr30%2B%2F5XTnRbePES%2FSQv1Wd44SwVNgEzJ3Jz12cbaBk%2B73RaJalXleful4KnIHbVcdptzo1Ps%2Fm6pzkrYzV8043FgzrL9uywq3%2FQcC5%2FQY%3D%3C%2Fdiagram%3E%3C%2Fmxfile%3E)
