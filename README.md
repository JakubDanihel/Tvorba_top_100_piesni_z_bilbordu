# Tvorba_top_100_piesni_z_bilbordu
Python program na tvorbu Spotify zoznamu zo stranky Billboard TOP 100 pre zadany datum.


## Ako to funguje?

Skript vykoná nasledujúce kroky:
1.  **Načíta dáta z Billboardu**: Vypýta si od používateľa dátum a počet pesničiek (1-100). Následne pomocou web scrapingu stiahne zoznam najpopulárnejších pesničiek z oficiálnej stránky `billboard.com`.
2.  **Prihlási sa do Spotify**: Pomocou knižnice `spotipy` a Spotify API sa bezpečne autentifikuje do vášho Spotify účtu.
3.  **Vyhľadá pesničky**: Pre každú pesničku zo zoznamu Billboardu vyhľadá jej unikátny identifikátor (URI) na Spotify. Ak sa pesnička nenájde, je preskočená.
4.  **Vytvorí playlist**: Vytvorí nový súkromný playlist s názvom obsahujúcim zadaný dátum a počet pesničiek (napr. `2000-08-12 Billboard TOP 50`).
5.  **Pridá pesničky**: Všetky nájdené pesničky pridá do novovytvoreného playlistu.

## Inštalácia a nastavenie

### 1. Knižnice
Pred spustením skriptu je potrebné nainštalovať požadované Python knižnice. Môžete to urobiť pomocou nasledujúceho príkazu v termináli:
```bash
pip install requests beautifulsoup4 spotipy
```

### 2. Nastavenie Spotify Aplikácie
Aby sa skript mohol pripojiť k vášmu účtu, musíte si vytvoriť aplikáciu na Spotify Developer Dashboard.

1.  Prejdite na [Spotify Developer Dashboard](https://developer.spotify.com/dashboard/) a prihláste sa.
2.  Kliknite na **"Create app"**.
3.  Zadajte názov a popis aplikácie (napr. "Billboard Playlist Generator").
4.  Po vytvorení aplikácie uvidíte **Client ID** a po kliknutí na **"Show client secret"** aj **Client Secret**. Tieto hodnoty budete potrebovať.
5.  Kliknite na **"Edit Settings"**.
6.  Do poľa **"Redirect URIs"** pridajte `http://example.com` a kliknite na **"Add"** a potom na **"Save"**.

### 3. Premenné Prostredia
Skript načíta vaše prihlasovacie údaje (Client ID, Client Secret) z premenných prostredia. Je to bezpečnejší spôsob ako ich vkladať priamo do kódu.

**Windows (v príkazovom riadku):**
```cmd
set SPOTIPY_CLIENT_ID=vas_client_id
set SPOTIPY_CLIENT_SECRET=vas_client_secret
set SPOTIPY_REDIRECT_URI=http://example.com
```

**Linux / macOS:**
```bash
export SPOTIPY_CLIENT_ID='vas_client_id'
export SPOTIPY_CLIENT_SECRET='vas_client_secret'
export SPOTIPY_REDIRECT_URI='http://example.com'
```
> **Poznámka:** Tieto premenné musíte nastaviť v tom istom termináli, z ktorého budete spúšťať skript. Po zatvorení terminálu sa stratia.

## Ako spustiť skript

1.  Uistite sa, že máte správne nastavené premenné prostredia (viď vyššie).
2.  Spustite skript `main.py` z vášho terminálu:
    ```bash
    python main.py
    ```
3.  Skript vás vyzve na zadanie dátumu vo formáte `YYYY-MM-DD`.
4.  Následne zadajte, koľko TOP pesničiek si želáte pridať (číslo od 1 do 100).
5.  Pri prvom spustení sa vám v prehliadači otvorí prihlasovacia stránka Spotify. Prihláste sa a odsúhlaste oprávnenia pre aplikáciu.
6.  Po úspešnom prihlásení skript dokončí svoju prácu. Vytvorí sa súbor `token.txt`, ktorý slúži na uloženie prihlásenia pre budúce spustenia.
7.  Po dokončení nájdete nový playlist vo vašej knižnici na Spotify.
