# 📘 SQL príkazy z příkazové řádky (MySQL/MariaDB)
  
Praktická příručka pro správu databází v projektech **[eKultura](https://ekultura.eu)**

---

## 🔗 Připojení k databázi
```bash
mysql -u root -p
sudo mysql -u root -p

### S určením hostitele a portu
mysql -u root -p -h 127.0.0.1 -P 3306

### V Dockeru (např. kontejner magic_db)
docker exec -it magic_db mariadb -u root -p
```

## 🏗️ Vytvoření nové databáze
```sql
CREATE DATABASE ekultura_db DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;
```

## 👤 Vytvoření nového uživatele
```sql
CREATE USER 'ekultura_user'@'localhost' IDENTIFIED BY 'bezpecne_heslo';
CREATE USER 'ekultura_user'@'%' IDENTIFIED BY 'bezpecne_heslo';
```

## 🔐 Přiřazení oprávnění
```sql
GRANT ALL PRIVILEGES ON ekultura_db.* TO 'ekultura_user'@'localhost';
GRANT ALL PRIVILEGES ON ekultura_db.* TO 'ekultura_user'@'%';
FLUSH PRIVILEGES;

-- Změna hesla uživatele
ALTER USER 'ekultura_user'@'localhost' IDENTIFIED BY 'nove_bezpecne_heslo';
ALTER USER 'ekultura_user'@'%' IDENTIFIED BY 'nove_bezpecne_heslo';
```

## 📋 Zobrazení informací
```sql
-- Seznam databází
SHOW DATABASES;

-- Použití konkrétní databáze
USE ekultura_db;

-- Seznam tabulek v databázi
SHOW TABLES;

-- Seznam uživatelů
SELECT user, host FROM mysql.user;
```

## 🩹 Odstranění databáze nebo uživatele
```sql
-- Smazání databáze
DROP DATABASE ekultura_db;

-- Smazání uživatele
DROP USER 'ekultura_user'@'%';
```

## 📦 Práce s databází v Dockeru
```bash
# Shell uvnitř kontejneru
docker exec -it magic_db bash

# MariaDB shell uvnitř kontejneru
docker exec -it magic_db mariadb -u root -p
```

---

_Vytvořeno pro interní potřeby projektů **[eKultura](https://ekultura.eu)** z. s._  
`#eKultura #SQL #Docker #MariaDB`
