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
- Dawne instrukcje e-Obiegu i eksportu sprzedaży: sprawdzone ponownie 25.09.2026 w QA 577; wynik eksportu pliku wciąż wymaga odczytu pobranego pliku.
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


## Onboarding: potwierdzenie zakończenia w QA

Studio Początek QA (577): użytkownik zatwierdził checkout Stripe w piaskownicy. Zweryfikowano powrót na pulpit oraz Ustawienia → Subskrypcje → Aplikacja: aktywny Team, OKRES PRÓBNY, miesięcznie. Zapisano zrzuty pulpitu i statusu bez adresu e-mail. Instrukcja zawiera etapy kreatora i potwierdzenie aktywacji. Użytkownik zaakceptował dotychczasową weryfikację bez niezależnego replayu; rejestrację, potwierdzenie e-maila i końcowe zatwierdzenie checkoutu wykonał użytkownik. Brak publikacji produkcyjnej.

Zdjęcie e-maila dostarczone przez użytkownika dodano po zamaskowaniu odbiorcy i całego linku aktywacyjnego. Redakcję wykonano narzędziem imagegen, wizualnie sprawdzono brak widocznego adresu i kodu. Oryginał nie wchodzi do commita.


## Usunięcie publicznych notatek redakcyjnych

Potwierdzenie e-maila przeniesiono do instrukcji logowania i rejestracji. Usunięto infoboksy o QA i akceptacji z 10 stron FAQ. Zachowano informacje o uprawnieniach, zakresie funkcji i demonstracyjnych danych. Dotychczasowe notatki weryfikacyjne zachowane poniżej jako dokumentacja wewnętrzna:

- faq/intro/partial-payment.mdx: Materiał roboczy do akceptacji. Zrzuty pochodzą z danych demonstracyjnych w QA. Dodanie wpłaty rejestruje kwotę w aplikacji; nie wykonuje przelewu bankowego.

- faq/intro/creating-company.mdx: Test QA z 21.09.2026, Altera 2.36.0+1574. Dane firmy Studio Początek QA są fikcyjne. Rejestrację, potwierdzenie e-maila i pierwsze logowanie wykonał użytkownik. Kreator przeszedł do checkoutu Stripe w piaskownicy. Użytkownik zatwierdził testową subskrypcję; sprawdzono powrót na pulpit i status okresu próbnego Team.

- faq/intro/first-invoice.mdx: Materiały robocze do akceptacji. Proces sprawdzany w środowisku QA. Zrzuty przedstawiają dane demonstracyjne.

- faq/intro/welcome.mdx: Rejestrację, potwierdzenie e-maila i pierwsze logowanie sprawdzono z udziałem użytkownika w QA 21.09.2026. Instrukcja nie obejmuje wszystkich wariantów logowania przez dostawców zewnętrznych.

- faq/intro/onboarding.mdx: Wersja do akceptacji. Poniższa mapa łączy instrukcje sprawdzone w QA 21.09.2026. Użytkownik wykonał rejestrację, weryfikację e-maila i pierwsze logowanie. Kreator nowej firmy sprawdzono do powrotu na pulpit po testowym checkoutcie Stripe zatwierdzonym przez użytkownika. Potwierdzono aktywny okres próbny Team. Dostępność czynności zależy od uprawnień i pakietu firmy.

- faq/howto/missing-document.mdx: Sprawdzono 21.09.2026 w QA, Altera 2.36.0+1574: dokumenty oczekujące na weryfikację, import e-mailem oraz wyszukiwanie i reset filtrów. Dane na zrzutach są demonstracyjne.

- faq/howto/project-result.mdx: Sprawdzono 21.09.2026 w QA, Altera 2.36.0+1574, na projekcie Rebranding Forma. Przykład pokazuje wynik dokumentów ujętych w raporcie. Nie obejmuje budżetu projektu, ewidencji czasu pracy ani pełnego wyniku księgowego.

- faq/howto/cost-to-settlement.mdx: Sprawdzono 21.09.2026 w QA, Altera 2.36.0+1574. Przykład DEMO/OCR/2026/002 to fikcyjna faktura na 1230 zł. Zrzut pól opisu pochodzi z powtórzenia na dokumencie DEMO/OCR/2026/003. Zapis zapłaty jest symulacją na danych demonstracyjnych; nie wykonano przelewu. Nie przelewaj pieniędzy na rachunki ze zrzutów.

- faq/modules/finance.mdx: Materiał roboczy do akceptacji. Zrzuty i przykłady pochodzą z firmy demonstracyjnej w QA.

- faq/modules/payments.mdx: Wersja do akceptacji. Zrzuty pokazują syntetyczne dane QA. Nie wykonuj przelewów na rachunki z przykładów. Sprawdzono akceptację kosztu, przygotowanie pliku i oba wejścia do QR. Import i wykonanie przelewu w banku pozostają poza testem.

## Uzupełnienie 25.09.2026: e-Obieg i eksport sprzedaży

- QA 577, Altera 2.36.0+1602: odczytano ustawienie **Koszty → e-Obieg dokumentów** i trzy dostępne poziomy. Nie zmieniano konfiguracji firmy. Usunięto ze starej instrukcji twierdzenia o automatycznych powiadomieniach i przypisaniach, których nie sprawdzono.
- W tej samej syntetycznej firmie wystawiono fakturę demonstracyjną za usługę 100 PLN, płatną gotówką. Nie wysyłano jej odbiorcy ani do KSeF.
- Sprawdzono dwa wejścia do eksportu sprzedaży: **Eksportuj** według filtrów i **Eksportuj wybrane** po zaznaczeniu faktury. Odczytano aktualną listę formatów. Po uruchomieniu PDF aplikacja potwierdziła rozpoczęcie przygotowania eksportu, lecz nie potwierdzono otwarcia ani pobrania pliku. Instrukcja nie obiecuje retencji pliku ani wyniku importu księgowego.
- Zrzuty przedstawiają pola i akcje, nie tylko wynik. Sprawdzono istnienie obrazów, ich rzeczywisty format JPEG, lokalne odnośniki i `git diff --check`. Mintlify `dev` nie ukończył pobrania lokalnego klienta; `validate` zgłosił brak dostępu do internetu. Pełny render pozostaje otwarty.
- Test faktury cyklicznej utworzył regułę z pierwszą datą 25.10.2026 i bez automatycznej wysyłki. Akcja **Dezaktywuj** zwróciła błąd serwera. Regułę usunięto przez edycję; lista reguł była następnie pusta. Temat nie jest gotowy do instrukcji końcowej.

## Uzupełnienie 25.09.2026: faktura pro forma

- QA 577, Altera 2.36.0+1602: z menu **Nowa faktura → Pro forma** wystawiono dwa syntetyczne dokumenty, PRO 1/9/2026 na 100 PLN i w powtórzeniu według tekstu PRO 2/9/2026 na 120 PLN. Oba są wystawione, nieopłacone, z formą płatności Gotówka. Nie wysyłano e-maila ani do KSeF. Podgląd PDF potwierdził typ, numer, pozycję i sumę.
- Powtórzenie wykazało, że wpisanie kodu pocztowego bez myślnika w maskowanym polu dało niepełną wartość; dokument 2 początkowo zapisał się bez kodu. W edycji wpisano pełne `00-002`, zapisano i niezależnie otwarto dokument z listy. Lista, szczegóły i ponownie otwarty PDF pokazały pełny adres. Instrukcja nakazuje sprawdzenie pełnego adresu po wystawieniu.
- Nowa instrukcja `faq/howto/proforma.mdx` używa zrzutów menu, początku formularza, danych nabywcy, akcji na pozycji, płatności i wyniku. Pozostałe typy dokumentów z C12, w tym korekta, zaliczka i końcowa, wymagają osobnych testów.
