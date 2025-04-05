
# 🔐 Bezpečnostní standardy – eKultura servery

Minimální zabezpečení nových Ubuntu serverů v rámci projektů eKultura. Základní úprava NGINX a skrytí serverových hlaviček.

---

## 🌐 Zabezpečení NGINX

```nginx
# Vypnutí verzí serveru
server_tokens off;

# Přidání bezpečnostních hlaviček
add_header X-Content-Type-Options "nosniff";
add_header X-Frame-Options "SAMEORIGIN";
add_header X-XSS-Protection "1; mode=block";
add_header Referrer-Policy "no-referrer-when-downgrade";
add_header Permissions-Policy "geolocation=(), microphone=()";
add_header Content-Security-Policy "default-src 'self'; script-src 'self';";
```

> 💡 Pokud `add_header` nefunguje, ujisti se, že není v podmíněném bloku (např. `if`, `location`) nebo že server neposílá 304/204 odpověď.

## ⚙️ Doporučení z výstupů nástroje webhint.io

- Nepoužívat `X-Frame-Options`, místo toho použít `Content-Security-Policy` s `frame-ancestors`
- Odstranit hlavičku `Server` nebo omezit na název (`nginx` místo `nginx/1.24.0`)
- Nepoužívat hlavičku `Expires`, preferovat `Cache-Control`
- Přidat `X-Content-Type-Options: nosniff`

---

*Vytvořeno jako bezpečnostní minimum pro nasazení nových serverů eKultura z. s.*

`#eKultura #Ubuntu #Bezpečnost #Nginx #Security`
