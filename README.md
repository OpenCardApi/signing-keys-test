# signing-keys-test

Klucze publiczne **Senderów** [OpenCardAPI](https://opencardapi.org) do weryfikacji podpisów żądań (JWS).

> **Środowisko: test.** Klucze produkcyjne są w repozytorium [signing-keys](https://github.com/OpenCardApi/signing-keys). Oba repozytoria mają ten sam układ.

Specyfikacja: [opencardapi.org – 9. Klucze](https://opencardapi.org/#dok-klucze) oraz [10. Podpis żądania (JWS)](https://opencardapi.org/#dok-podpis).

## Układ repozytorium

```
signing-keys-test/
└── <open_card_api_id>/      # identyfikator Sendera (12 znaków)
    └── <kid>.pem            # klucz publiczny w formacie PEM
```

Przykład:

```
signing-keys-test/
└── 000000000000/
    ├── rsa-key.pem          # kid: "rsa-key" (RS256 lub PS256)
    └── ec-key.pem           # kid: "ec-key"  (ES256)
```

## Zasady

- Każdy Sender ma jeden katalog nazwany swoim `open_card_api_id` (12 znaków alfanumerycznych).
- Każdy klucz to osobny plik `<kid>.pem`. Nazwa pliku bez rozszerzenia to `kid`.
- `kid` może zawierać tylko litery, cyfry, `-` i `_`.
- Obsługiwane klucze: RSA (`RS256`, `PS256`) i EC P-256 (`ES256`).
- Repozytorium zawiera **wyłącznie klucze publiczne**. Klucz prywatny nigdy nie opuszcza Sendera.
- Używaj w testach innej pary kluczy niż na produkcji.
- Sender może mieć kilka aktywnych kluczy jednocześnie. Przy wymianie klucza nowy dodaje się pod nowym `kid`, a stary usuwa, gdy przestanie być używany.

## Powiązane repozytoria

| Klucze | Produkcja | Test |
|---|---|---|
| Podpis Senderów (PEM) | [signing-keys](https://github.com/OpenCardApi/signing-keys) | **signing-keys-test** |
| Szyfrowanie Receiverów (JWK) | [encryption-keys](https://github.com/OpenCardApi/encryption-keys) | [encryption-keys-test](https://github.com/OpenCardApi/encryption-keys-test) |

## Kontakt

Rejestracja lub wymiana klucza, pytania do specyfikacji: [support@espago.com](mailto:support@espago.com).
