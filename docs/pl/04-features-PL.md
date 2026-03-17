🇬🇧 English version → [See English version](../en/04-features.md)

---

# Propozycje funkcjonalności – Floowe

Dokument przedstawia trzy nowe funkcjonalności dla platformy Floowe na podstawie wcześniejszej analizy produktu, przepływów użytkownika (user flows) oraz analizy Event Storming.

Etap generowania pomysłów został wsparty przez Claude AI, a następnie dopracowany w celu dopasowania do obecnej architektury produktu.

---

# Funkcja 1 – Panel analizy wyników treści

Domena: Dystrybucja  
Typ: Analityka

## User Story

Jako marketing manager korzystający z Floowe  
Chcę widzieć statystyki dotyczące opublikowanych artykułów i postów w mediach społecznościowych  
Aby móc zrozumieć, które treści generują największy ruch i zaangażowanie.

## Kryteria akceptacji

- Panel pokazuje metryki artykułów, takie jak liczba odsłon, średni czas spędzony na stronie oraz wyświetlenia w wyszukiwarce.
- Metryki z mediów społecznościowych (polubienia, udostępnienia, kliknięcia, zasięg) są agregowane dla Facebooka, LinkedIn i X.
- System wyświetla ranking najlepiej performujących artykułów według wskaźnika zaangażowania.
- Dane odświeżają się automatycznie co 24 godziny.
- Każda metryka zawiera link do oryginalnego źródła analityki.

## Uzasadnienie biznesowe

Obecnie Floowe koncentruje się na generowaniu i publikowaniu treści, ale nie dostarcza informacji o ich skuteczności.  
Panel analityczny zamyka pętlę informacji zwrotnej i pozwala użytkownikom optymalizować strategię content marketingową.

## Przegląd techniczny

Komponenty:
- interfejs panelu analitycznego
- backendowy serwis agregujący metryki
- warstwa przechowywania danych analitycznych

Integracje:
- Google Search Console API
- Facebook Graph API
- LinkedIn Marketing API
- X API

Proponowany stos technologiczny:
- React (panel analityczny)
- Node.js (serwis agregujący dane)
- PostgreSQL (przechowywanie metryk)
- Redis (warstwa cache)

## Ryzyka i wyzwania

- ograniczenia API poszczególnych platform analitycznych
- niedokładna atrybucja ruchu bez parametrów UTM
- konieczność utrzymania wielu integracji zewnętrznych

---

# Funkcja 2 – Kalendarz publikacji i harmonogramowanie treści

Domena: Publikacja  
Typ: Główny workflow

## User Story

Jako właściciel małej firmy korzystający z Floowe  
Chcę planować publikację artykułów i postów z wyprzedzeniem  
Aby utrzymać regularny harmonogram publikacji bez ręcznego logowania się do systemu.

## Kryteria akceptacji

- Użytkownik może wybrać datę i godzinę publikacji artykułu.
- Kalendarz pokazuje artykuły w statusach: szkic, zaplanowany i opublikowany.
- Zaplanowane publikacje można edytować lub anulować.
- System wysyła powiadomienie przed planowaną publikacją.
- W przypadku błędu publikacji system automatycznie podejmuje ponowną próbę.

## Uzasadnienie biznesowe

Regularność publikacji jest kluczowa dla skuteczności strategii SEO i content marketingu.  
Funkcja harmonogramowania zmienia Floowe z narzędzia do generowania treści w platformę do zarządzania całym procesem publikacji.

## Przegląd techniczny

Komponenty:
- moduł harmonogramowania publikacji
- interfejs kalendarza
- system kolejek zadań w tle

Integracje:
- API platform społecznościowych
- API systemu CMS
- system wysyłki powiadomień email

Proponowany stos technologiczny:
- React + FullCalendar (interfejs kalendarza)
- Node.js (serwis harmonogramowania)
- Redis + BullMQ (kolejka zadań)
- PostgreSQL (zaplanowane publikacje)

## Ryzyka i wyzwania

- wygaśnięcie tokenów OAuth dla zaplanowanych publikacji
- obsługa różnych stref czasowych
- niezawodność systemu kolejek zadań

---

# Funkcja 3 – Profile stylu i tonu marki

Domena: Generowanie treści  
Typ: Personalizacja AI

## User Story

Jako agencja marketingowa obsługująca wielu klientów  
Chcę definiować profile stylu i tonu marki dla każdego klienta  
Aby generowane treści automatycznie odpowiadały stylowi komunikacji danej marki.

## Kryteria akceptacji

- Użytkownik może tworzyć wiele profili stylu marki.
- Profil zawiera ton komunikacji, styl pisania, opis grupy docelowej oraz listę preferowanych i zakazanych fraz.
- Profil można wybrać podczas generowania artykułu.
- System AI uwzględnia styl i ton podczas generowania treści.
- Użytkownik może ustawić domyślny profil stylu.

## Uzasadnienie biznesowe

Jednym z głównych problemów narzędzi AI do generowania treści jest brak spójności stylu komunikacji.  
Profile stylu marki pozwalają generować treści dopasowane do charakteru marki i zmniejszają konieczność ręcznej edycji.

## Przegląd techniczny

Komponenty:
- interfejs zarządzania profilami stylu
- warstwa konfiguracji promptów AI
- baza danych profili stylu

Integracje:
- API modeli językowych wykorzystywanych do generowania treści

Proponowany stos technologiczny:
- React (panel ustawień)
- Node.js (generator promptów)
- PostgreSQL (przechowywanie profili)

## Ryzyka i wyzwania

- modele językowe mogą nie zawsze respektować ograniczenia stylu
- większa złożoność interfejsu dla małych użytkowników
- zmiany modeli AI mogą wpływać na spójność stylu

---

# Podsumowanie

| Funkcja | Domena | Typ | Wpływ |
|-------|-------|-------|-------|
| Panel analizy wyników treści | Dystrybucja | Analityka | umożliwia optymalizację strategii contentowej |
| Kalendarz publikacji i harmonogramowanie | Publikacja | Workflow | poprawia regularność publikacji |
| Profile stylu i tonu marki | Generowanie treści | Personalizacja AI | poprawia jakość i spójność treści |
