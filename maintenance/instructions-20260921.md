# Lokalna aktualizacja Centrum pomocy, 2026-09-21

## Zakres i dowody

Weryfikacja w QA na demonstracyjnej firmie Pracownia Forma. Zrzuty są rzeczywistymi ekranami aplikacji. Dane firmy i dokumentów są fikcyjne. Publikacja produkcyjna nie została wykonana.

| Obszar | Weryfikacja | Ograniczenie |
| --- | --- | --- |
| Centrum pomocy, Sprzedaż, Koszty | Zachowane istniejące trasy, nowa nawigacja zadaniowa, linki do szczegółowych instrukcji | Nowa nawigacja nie oznacza aktualizacji wszystkich dawnych treści |
| Dodanie kosztu i OCR | Dwa osobne PDF-y, porównanie danych, zatwierdzenie jednorazowe, wynik Wystawiona/Nieopłacona | Fikcyjne NIP-y powodują ostrzeżenia; nie testowano wszystkich błędów OCR |
| Wyszukiwanie i filtry | Numer, Po terminie, dwa kryteria, pusty wynik, reset pojedynczy i pełny; powtórzenie w QA | Nie sprawdzano każdej kombinacji filtrów |
| Pliki | Dodanie dokumentów 1 i 2; powtórzenie według tekstu na dokumencie 3 | Bez testu usuwania i uprawnień do dokumentów |
| Pobieranie plików | Pojedynczy plik zgodny bajtowo ze źródłem; ZIP zawiera dwa właściwe pliki; powtórzenie pobierania dokumentu 3 | Nie testowano eksportu wielostronicowego archiwum |
| Import e-mail | Za zgodą użytkownika jedna wiadomość z syntetycznym PDF-em do dedykowanego adresu QA; dokument DEMO/EMAIL/2026/001, 123 PLN, widoczny w Kosztach i powiadomieniu | Nie wysyłano drugiej wiadomości; historia dostarczenia była pusta mimo skutecznego importu |
| Powiadomienia | Dzwonek, przejście do ustawień, zmiana Aktualności/Aplikacja, odczyt po odświeżeniu, powtórzenie; przywrócono stan początkowy | Nie testowano dostarczenia każdego rodzaju wiadomości ani zgody systemowej push |
| Pulpit | Aktualny ekran, szybkie akcje, przejście do raportów finansowych | Nie oznaczano podatków ani faktur jako opłaconych |
| Logowanie | Aktualne formularze, wylogowanie i ponowne logowanie na istniejące konto QA | Nie utworzono nowego konta, nie akceptowano regulaminu ani nie testowano SSO/resetu hasła |
| Dodanie firmy | Menu wejściowe i pierwszy ekran, anulowanie; dane i rachunki istniejącej firmy | Brak pełnego onboardingu nowej firmy |
| Ustawienia faktur | Aktualne sekcje i podgląd numeracji | Nie zmieniano numeracji ani danych firmy |
| Open Banking | Rachunki, stan Nie podłączone, punkt rozpoczęcia synchronizacji | Brak autoryzacji bankowej, transakcji i pełnego testu rozrachunków |

Dziewięć odświeżonych stron klienta: desktop i 390 px, po jednym H1, wszystkie obrazy załadowane, brak poziomego przepełnienia. Sprawdzono lokalne odnośniki i git diff --check. Szczegółowe dowody wykonania, pliki testowe i prywatne identyfikatory pozostają poza repozytorium.

## Pozostałe testy przed uznaniem całej bazy za odświeżoną

- Nowe konto, weryfikacja e-mail i pełne dodanie firmy: osobny scenariusz z ręcznym przyjęciem warunków.
- Open Banking: kontrolowany rachunek testowy, autoryzacja, pobranie danych, odnowienie i rozłączenie.
- Widoki księgowości, organizacja i role: odłożone na prośbę użytkownika do potwierdzenia ukończenia przebudowy.
- Dawne instrukcje e-Obiegu i eksportu sprzedaży: osobny przegląd; nie są potwierdzone przez test pobierania z Plików.
- Rozbieżność historii importu e-mail: zgłoszenie i sprawdzenie przyczyny oddzielnie od redakcji instrukcji.

## Extension batch: verified client workflows

- New guides: missing document troubleshooting, onboarding task map, project result.
- QA 565: DEMO/OCR/2026/002 category changed from empty to Projektowanie; saved and independently seen on list and finance totals. No project assigned.
- The same demo invoice passed Opisz fakturę, Zaakceptuj koszt, Zaakceptuj do płatności. QR showed exact 1230 PLN and document number. Manual paid-state test is simulated QA data, no money transfer. Final independent UI readback: OPŁACONA. Replay on DEMO/OCR/2026/003 passed category save, describe, cost approval, payment approval and paid marking from the list. First run used QR paid marking. Both demo documents remain paid, category Projektowanie, no project. No bank transfer occurred.
- Onboarding dry-run in private workspace, synthetic NIP chosen by user. New write set awaiting confirmation; no account/company created. Registration password and final submit require user handoff.

- Critical distinction: e-Obieg zakończony appears after payment approval while the cost is still unpaid. Guide explicitly separates workflow completion and settlement.
- New guides and hub: desktop and 390 px render checks passed, one H1, all images loaded, no horizontal overflow. Local links and image paths checked; git diff --check passed.
- Project report: month September 2026, Rebranding Forma revenue 25000, costs 22060, difference 2940; all-project cost total 24060. New costs remain without project. Category edits do not change project totals.
- No new account/company, subscription, Stripe, bank consent, KSeF or production publication in this batch. Full new-account onboarding remains pending write-set approval and user password/registration handoff.
