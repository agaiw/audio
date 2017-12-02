
##AUDIO.communicator

### Cel aplikacji
Aplikacja umożliwia komunikację między dwoma urządzeniami za pomocą fal dźwiękowych. Informacje są przesyłane przy użyciu modulacji częstotliwościowej. Aplikacja zapewnia niezawodne dostarczanie informacji dzięki kodom korekcyjnym oraz zastosowaniu protokołu Stop and Wait ARQ.

### Przypadek użycia 1: Wysyłanie komunikatu

#### Warunki wstępne
Aplikacja została uruchomiona na urządzeniu i znajduje się w stanie gotowości.

#### Scenariusz
1. Użytkownik wybiera opcję Nowy komunikat.
2. System umożliwia użytkownikowi wprowadzenie komunikatu.
3. Użytkownik wpisuje komunikat przy użyciu znaków ASCII i zatwierdza jego wysyłkę.
4. System sprawdza, czy komunikat zawiera tylko znaki ASCII.
  Ex 4.1. W przypadku komunikatu zawierającego niedozwolone znaki system wyświetla informację o błędzie i powraca do kroku 2.
5. System przechodzi w stan transmisji.
6. System wprowadza nadmiarowe bity do komunikatu oraz wstawia do niego sumę kontrolną.
7. System oblicza charakterystykę fali dźwiękowej na podstawie komunikatu.
8. System emituje preambułę oraz wygenerowaną falę dźwiękową.
9. System uruchamia timer 10 sekund i oczekuje na komunikat potwierdzający.
  Ex 9.1. Jeśli w ciągu 10 sekund komunikat potwierdzający nie nadejdzie, system wyświetla informację o błędzie i przechodzi w stan gotowości.
10. System rejestruje komunikat potwierdzający.
  Ex 10.1. Jeśli nie można poprawnie zdekodować komunikatu potwierdzającego, system wyświetla informację o błędzie i przechodzi w stan gotowości.
  Ex 10.2. Jeśli komunikat potwierdzający zawiera informację o niepoprawnym odbiorze komunikatu, system powraca do kroku 8.
11. System wyświetla informację o poprawnej transmisji i przechodzi do stanu gotowości.
12. Koniec przypadku użycia.

### Przypadek użycia 2: Odbiór komunikatu

#### Warunki wstępne
Aplikacja została uruchomiona na urządzeniu i znajduje się w stanie gotowości.

#### Scenariusz
1. System nasłuchuje i wykrywa preambułę w postaci dźwięku o określonej długości i częstotliwości.
2. System przechodzi w stan odbioru i nagrywa komunikat.
3. System dekoduje komunikat.
4. System sprawdza, czy komunikat jest poprawny, obliczając dla niego sumę komtrolną i porównując ze zdekodowaną sumą kontrolną.
  Ex 4.1. Jeśli komunikat jest niepoprawny, system emituje preambułę oraz komunikat NACK, a następnie przechodzi do stanu gotowości. Koniec przypadku użycia.
5. System wyświetla komunikat na ekranie, a następnie przechodzi do stanu gotowości. 
6. Koniec przypadku użycia.


### Wymagania niefunkcjonalne
1. Maksymalna długość przesyłanego komunikatu wynosi 160 znaków.
2. Informacje 0/1 są kodowane odpowiednio na dwóch wybranych częstotliwościach.
3. Aplikacja działa na komputerze typu PC wyposażonym w kartę dźwiękową, głośnik i mikrofon.

### Protokół wymiany danych:

#### Struktura komunikatu

0. Preambuła
1. Typ komunikatu (1. Komunikat, 2. ACK/NACK)
2. Suma kontrolna
3. Dane z nadmiarowymi bitami korekcyjnymi

