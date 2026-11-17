# Strona LearnCode na GitHub Pages

Zawartość katalogu `site/` trafia do repozytorium `dominik676767/LearnCode` (gałąź i folder publikowane przez GitHub Pages),
czyli pod adres https://dominik676767.github.io/LearnCode/.

| Plik | Adres | Rola |
|---|---|---|
| `index.html` | `/LearnCode/` | dotychczasowa strona „potwierdzono adres e-mail” (bez zmian) |
| `auth/callback/index.html` | `/LearnCode/auth/callback/` | powrót z logowania Google / GitHub / Discord: otwiera aplikację deep linkiem `learncode://auth/callback?code=…&flow=…` (na Androidzie przez `intent://`), obsługuje błąd i anulowanie, a gdy aplikacja się nie otworzy — pokazuje jednorazowy kod do wklejenia w aplikacji („Mam kod z przeglądarki”) |
| `.nojekyll` | — | wyłącza przetwarzanie Jekyll (publikowane są wszystkie pliki bez zmian) |

Strona nie wysyła kodu nigdzie poza aplikację (brak zewnętrznych skryptów, `Content-Security-Policy`, `no-referrer`).
Sam kod jest bezużyteczny bez `code_verifier`, który nie opuszcza telefonu (PKCE).

## Pliki dla domeny głównej (`root-domain/`)

GitHub Pages projektu (`/LearnCode/`) **nie może** serwować plików z katalogu głównego domeny. Te dwa pliki muszą trafić do
repozytorium **`dominik676767/dominik676767.github.io`** (strona użytkownika), w ten sam układ katalogów:

- `.well-known/assetlinks.json` → https://dominik676767.github.io/.well-known/assetlinks.json — weryfikacja Android App Links
  (adres strony powrotu otwiera aplikację bezpośrednio). Uzupełnij `package_name` (z `buildozer.spec`: `package.domain` +
  `package.name`) i odcisk SHA-256 certyfikatu podpisu (`keytool -list -v -keystore twoj.keystore` albo Play Console →
  Integralność aplikacji → Podpisywanie aplikacji). W repozytorium użytkownika dodaj też pusty plik `.nojekyll`, bo Jekyll
  pomija katalogi zaczynające się od kropki.
- `app-ads.txt` → https://dominik676767.github.io/app-ads.txt — wymagany przez AdMob dla reklam produkcyjnych; ta sama domena
  musi być wpisana jako strona dewelopera w Google Play.

Bez `assetlinks.json` logowanie nadal działa: strona powrotu otwiera aplikację deep linkiem.
