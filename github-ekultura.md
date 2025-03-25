# 🐙 GitHub – Denní použití a workflow pro eKultura

Praktická příručka pro práci s Git a GitHub repozitáři v rámci interních projektů **eKultura**.

---

## ✅ Denní použití

```bash
# Stažení změn ze vzdáleného repozitáře
git fetch origin

# Přepsání lokálních změn podle vzdálené větve (pozor: ztrácí neuložené změny)
git reset --hard origin/main

# Stažení větve a nasazení (např. digitální muzeum)
git fetch origin deployment
git reset --hard origin/deployment
```

---

## 1️⃣ Inicializace a základní nastavení (pouze jednou)

```bash
# Inicializace nového Git repozitáře
git init

# Nastavení jména a emailu (globálně)
git config --global user.name "Laura"
git config --global user.email "vas.email@example.com"

# Nastavení bezpečného adresáře (pro CI/produkční prostředí)
git config --global --add safe.directory /var/www/test.digitalni-muzeum.cz

# Přidání vzdáleného repozitáře
git remote add origin https://github.com/eKultura/digitalni-muzeum.cz.git
```

---

## 🔄 Další běžné příkazy

```bash
# Stažení celého repozitáře
git clone https://github.com/eKultura/digitalni-muzeum.cz.git

# Stažení konkrétní větve
git clone -b nazev-vetve https://github.com/eKultura/digitalni-muzeum.cz.git

# Stažení změn z hlavní větve
git pull origin main

# Nastavení místní větve tak, aby sledovala vzdálenou
git branch --set-upstream-to=origin/main main
```

---

## 🧰 Běžné operace

```bash
# Přidání všech změněných souborů
git add .

# Přidání konkrétního souboru
git add soubor.txt

# Commit změn s popisem
git commit -m "Popis změn"

# Odeslání na server
git push origin main

# NEPOUŽÍVEJ BEZ ROZMYSLU – přepíše vše na vzdáleném repozitáři
git push origin main --force

# Kontrola stavu
git status

# Zobrazení historie commitů
git log
```

---

## 🌿 Práce s větvemi

```bash
# Vytvoření nové větve
git branch nova-vetev

# Přepnutí na větev
git checkout nova-vetev
# nebo novější syntax
git switch nova-vetev

# Vytvoření a přepnutí zároveň
git checkout -b nova-vetev
# nebo
git switch -c nova-vetev

# Sloučení větve
git merge nazev-vetve

# Smazání větve
git branch -d nazev-vetve
```

---

## 🔁 Práce se vzdálenými změnami

```bash
# Stažení všech změn bez sloučení
git fetch origin

# Stažení konkrétní větve
git fetch origin nazev-vetve

# Stažení všech změn a odstranění neexistujících větví
git fetch --all --prune
```

---

## 🚀 Distribuční větve a verze

```bash
# 1. Vytvoření nové vývojové větve
git checkout -b feature-branch

# 2. Vývoj a commit
git add .
git commit -m "Funkce verze 1"

# 3. Vytvoření tagu pro release
git tag v1.0.0

# 4. Pokračování ve vývoji
git commit -m "Funkce verze 2"

git tag v2.0.0

# 5. Odeslání tagů
git push origin feature-branch --tags
```

---

*Vytvořeno pro interní potřeby projektů [eKultura](https://ekultura.eu) z. s.*  
`#eKultura #Git #GitHub #workflow`

