# Docker-hub eKultura
Pro potřeby projektů v rámci neziskové organizace eKultura používáme system kontejnerů.

## Docker Commands Cheat Sheet

Tento dokument obsahuje základní příkazy pro práci s Dockerem a Docker Compose.

## Vytváření Docker image (Dockerfile -> Image)

### Build Docker image
```sh
docker-compose build
```

### Build bez cache (vytvoří zcela nový image)
```sh
docker-compose build --no-cache
```

---

## Spouštění a správa kontejnerů

### Spuštění kontejnerů pomocí Docker Compose
```sh
docker-compose up -d
```

### Zastavení a odstranění kontejnerů (musí se spouštět ve stejné složce jako `docker-compose.yml`)
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
> Poznámka: Pokud má kontejner nastaveno `restart=always`, po restartu serveru se automaticky spustí znovu.

### Spuštění konkrétního kontejneru
```sh
docker start <container_name>
```

---

## Seznam kontejnerů

### Seznam běžících kontejnerů
```sh
docker ps
```

### Seznam všech kontejnerů (včetně zastavených)
```sh
docker ps -a
```

### Filtrování podle názvu (např. všechny běžící kontejnery obsahující `magic` v názvu)
```sh
docker ps --filter "name=magic"
```

---

## Zobrazení logů z kontejneru

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

## Spouštění příkazů uvnitř kontejnerů

### Otevření terminálu v běžícím kontejneru (vstup do kontejneru)
```sh
docker exec -it <container_name> bash
```

**Příklad:**
```sh
docker exec -it magic_django bash
```

### Otevření MariaDB shellu uvnitř kontejneru
```sh
docker exec -it magic_db mariadb -u root -p
```

### Přečtení obsahu souboru uvnitř kontejneru
```sh
docker exec -it <container_name> cat /cesta/k/souboru
```

**Příklad:**
```sh
docker exec -it magic_django cat /div_app/nohup.out
```

---

## Správa Docker sítí

### Seznam sítí
```sh
docker network ls
```

### Inspekce konkrétní sítě
```sh
docker network inspect <nazev_site>
```

### Volání mezi kontejnery ve stejné síti
V Docker síti se kontejnery mohou oslovovat pomocí jejich názvu z `docker-compose.yml` nebo `.env` .
Například pokud máš kontejner `magic_django` a chceš se připojit k databázi `magic_db`, použiješ `magic_db` místo IP adresy.
Toto platí jak v terminálu, tak např. v `settings.py` v Django projektu

**Příklad v aplikaci:**
```sh
mysql -h magic_db -u root -p
```

---

## Monitorování využití zdrojů

### Zobrazení statistik všech běžících kontejnerů
```sh
docker stats
```

### Zobrazení statistik konkrétního kontejneru
```sh
docker stats <container_name>
```

---

Tento dokument slouží jako základní referenční příručka pro práci s Dockerem a Docker Compose.

  _Vytvořeno pro interní potřeby projektů **[eKultura](https://ekultura.eu)** z. s._  
  *#vytvořil Petr Malina pro potřeby [eKultura](https://ekultura.eu)*
`#eKultura #Docker # #Ubuntu #Server #Linux`
