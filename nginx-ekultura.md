# 🧭 Nginx – Základní konfigurace a použití v eKultura

Praktická příručka pro nastavení **Nginx** jako webového serveru pro různorodé projekty neziskového spolku **eKultura**.

---

## 📌 Běžné umístění konfigurace
Konfigurační soubory se nacházejí zde:

```bash
/etc/nginx/sites-available/
/etc/nginx/sites-enabled/
```

Symlinkem se propojují soubory z `sites-available` do `sites-enabled`:

```bash
sudo ln -s /etc/nginx/sites-available/ekultura.eu /etc/nginx/sites-enabled/
```

---

## 🔧 Základní PHP konfigurace (např. ekultura.eu)

```nginx
server {
    listen 80;
    server_name ekultura.eu www.ekultura.eu;

    root /var/www/ekultura.eu/public_html;
    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php8.3-fpm.sock; # Zkontrolujte aktuální verzi PHP
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }

    location ~ /\.ht {
        deny all;
    }

    access_log /var/log/nginx/ekultura_access.log;
    error_log /var/log/nginx/ekultura_error.log;
}
```

---

## 🔁 Přesměrování HTTP → HTTPS
Certbot obvykle vytvoří automaticky, ale můžeme upravit ručně:
```bash
sudo certbot --nginx -d ekultura.eu -d www.ekultura.eu
```
A poté
```nginx
server {
    listen 80;
    server_name ekultura.eu www.ekultura.eu;

    return 301 https://$host$request_uri;
}
```

---

## 🔒 HTTPS konfigurace (Certbot / Let's Encrypt)

```nginx
server {
    listen 443 ssl;
    listen [::]:443 ssl;
    server_name ekultura.eu www.ekultura.eu;

    root /var/www/ekultura.eu/public_html;
    index index.php index.html;

    ssl_certificate /etc/letsencrypt/live/ekultura.eu/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/ekultura.eu/privkey.pem;
    include /etc/letsencrypt/options-ssl-nginx.conf;
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php8.2-fpm.sock;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }

    access_log /var/log/nginx/ekultura_ssl_access.log;
    error_log /var/log/nginx/ekultura_ssl_error.log;
}
```

---

## 🐘 Statická HTML stránka (např. etickymajak.cz)

```nginx
server {
    listen 80;
    server_name etickymajak.cz www.etickymajak.cz;
    return 301 https://$host$request_uri;
}

server {
    listen 443 ssl;
    server_name etickymajak.cz www.etickymajak.cz;

    root /var/www/etickymajak.cz;
    index index.html;

    ssl_certificate /etc/letsencrypt/live/etickymajak.cz/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/etickymajak.cz/privkey.pem;
    include /etc/letsencrypt/options-ssl-nginx.conf;
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem;

    location / {
        try_files $uri $uri.html $uri/ =404;
    }

    access_log /var/log/nginx/etickymajak_access.log;
    error_log /var/log/nginx/etickymajak_error.log;
}
```

---

## 🐳 Docker + proxy_pass (např. research.digitalni-muzeum.cz)

```nginx
server {
    listen 80;
    server_name research.digitalni-muzeum.cz;
    return 301 https://$host$request_uri;
}

server {
    listen 443 ssl;
    server_name research.digitalni-muzeum.cz;

    ssl_certificate /etc/letsencrypt/live/research.digitalni-muzeum.cz/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/research.digitalni-muzeum.cz/privkey.pem;
    include /etc/letsencrypt/options-ssl-nginx.conf;
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem;

    location / {
        proxy_pass http://127.0.0.1:8012;
        proxy_set_header Host $host;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    location /static/ {
        alias /var/www/research.digitalni-muzeum.cz/data/staticfiles/;
    }

    access_log /var/log/nginx/muzeum_access.log;
    error_log /var/log/nginx/muzeum_error.log;
}
```

---

## 🧠 UWSGI varianta pro Python (např. Flask / FastAPI / Django)

```nginx
server {
    listen 80;
    server_name api.ekultura.eu;
    return 301 https://$host$request_uri;
}

server {
    listen 443 ssl;
    server_name api.ekultura.eu;

    ssl_certificate /etc/letsencrypt/live/api.ekultura.eu/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/api.ekultura.eu/privkey.pem;
    include /etc/letsencrypt/options-ssl-nginx.conf;
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem;

    location / {
        include uwsgi_params;
        uwsgi_pass unix:/var/www/api.ekultura.eu/app.sock;
    }

    access_log /var/log/nginx/api_access.log;
    error_log /var/log/nginx/api_error.log;
}
```

---

## 🧾 Logy

Logy jsou umístěny ve složce `/var/log/nginx/`:

- **Přístupy:** `/var/log/nginx/example_access.log`
- **Chyby:** `/var/log/nginx/example_error.log`

Lze doplnit i do `http` nebo `server` bloku:

```nginx
access_log /var/log/nginx/custom_access.log;
error_log /var/log/nginx/custom_error.log;
```

---

*Vytvořeno pro interní potřeby projektů [eKultura](https://ekultura.eu) z. s.*  
`#eKultura #nginx #server #webhost`

