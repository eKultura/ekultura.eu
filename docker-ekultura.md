# 🐳 Docker-hub eKultura

Pro potřeby projektů v rámci neziskové organizace **[eKultura](https://ekultura.eu)** používáme systém kontejnerů.

---

## 🧰 Docker Commands Cheat Sheet

Tento dokument obsahuje základní příkazy pro práci s Dockerem a Docker Compose.

---

## 🏗️ Vytváření Docker image (Dockerfile → Image)


### Build Docker image
```sh
docker-compose build
```

### Build bez cache (vytvoří zcela nový image)
```sh
docker-compose build --no-cache
```

---

## 🚀 Spouštění a správa kontejnerů

![docker up](https://raw.githubusercontent.com/eKultura/assets/main/images/docker-up.png)

### Spuštění kontejnerů pomocí Docker Compose
```sh
docker-compose up -d
```

### Zastavení a odstranění kontejnerů (ve stejné složce jako `docker-compose.yml`)
```sh
docker-compose down
```

### Restart kontejneru
```sh
docker restart <container_name>
```

### Zastavení konkrétního kontejneru
```sh
docker stop <container_name>
```
> Pokud má kontejner `restart=always`, po restartu serveru se spustí automaticky.

### Spuštění konkrétního kontejneru
```sh
docker start <container_name>
```

---

## 📋 Seznam kontejnerů

![docker ps](https://raw.githubusercontent.com/eKultura/assets/main/images/docker-ps.png)

### Běžící kontejnery
```sh
docker ps
```

### Všechny kontejnery (včetně zastavených)
```sh
docker ps -a
```

### Filtrování podle názvu
```sh
docker ps --filter "name=magic"
```

---

## 📄 Zobrazení logů z kontejneru

### Výpis logů
```sh
docker logs <container_name>
```
**Příklad:**
```sh
docker logs magic_django
```

### Posledních 100 řádků s aktualizací v reálném čase
```sh
docker logs magic_django --tail 100 -f
```

---

## 🔧 Spouštění příkazů uvnitř kontejnerů

### Otevření terminálu v kontejneru
```sh
docker exec -it <container_name> bash
```
**Příklad:**
```sh
docker exec -it magic_django bash
```

### MariaDB shell uvnitř kontejneru
```sh
docker exec -it magic_db mariadb -u root -p
```

### Čtení souboru v kontejneru
```sh
docker exec -it <container_name> cat /cesta/k/souboru
```
**Příklad:**
```sh
docker exec -it magic_django cat /div_app/nohup.out
```

---

## 🌐 Správa Docker sítí

![docker network](https://raw.githubusercontent.com/eKultura/assets/main/images/docker-network.png)

### Seznam sítí
```sh
docker network ls
```

### Detailní inspekce sítě
```sh
docker network inspect <nazev_site>
```

### Volání mezi kontejnery (pomocí názvu)
Např. kontejner `magic_django` přistupuje k `magic_db`:
```sh
mysql -h magic_db -u root -p
```

---

## 📊 Monitorování využití zdrojů

### Statistiky všech běžících kontejnerů
```sh
docker stats
```

### Statistiky konkrétního kontejneru
```sh
docker stats <container_name>
```

---

Tento dokument slouží jako základní referenční příručka pro práci s Dockerem a Docker Compose.

_Vytvořeno pro interní potřeby projektů **[eKultura](https://ekultura.eu)** z. s._  
_*#vytvořil Petr Malina pro potřeby [eKultura](https://ekultura.eu)*_  
`#eKultura #Docker #Ubuntu #Server #Linux`

