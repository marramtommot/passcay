# Passcay Fork Notes

Base upstream: `uzyn/passcay` tag `v2.0.0`

Differenza funzionale del fork:
- `src/util.zig`: `parseClientDataJson` esegue un parse permissivo e ignora campi extra del browser come `crossOrigin`.

Scopo:
- compatibilita' con payload WebAuthn reali che includono campi aggiuntivi in `clientDataJSON`

Nota pacchetto:
- il fingerprint in `build.zig.zon` va rigenerato per evitare di riusare l'identita' upstream.
