# 🖥️ Ubuntu Server – Nejčastější příkazy a správa systému

Praktická příručka pro správu serverů v prostředí eKultura.

---

## 🧑‍💻 Základní informace o systému

```bash
hostname        # název serveru
uname -a        # info o jádru
lsb_release -a  # verze distribuce
uptime          # doba běhu systému
who             # přihlášení uživatelé
```

## 📦 Správa balíčků (APT)

```bash
sudo apt update                 # aktualizace seznamu balíčků
sudo apt upgrade                # aktualizace všech balíčků
sudo apt install <balíček>     # instalace balíčku
sudo apt remove <balíček>      # odstranění balíčku
sudo apt autoremove            # odstranění nepotřebných závislostí
```

## 🔥 Služby (systemd)

```bash
systemctl status <služba>      # stav služby
systemctl start <služba>       # spuštění služby
systemctl stop <služba>        # zastavení služby
systemctl restart <služba>     # restart služby
systemctl enable <služba>      # automatický start při bootu
systemctl disable <služba>     # zrušení automatického startu
```

## 👥 Správa uživatelů

```bash
adduser <jméno>                # vytvoření uživatele
usermod -aG sudo <jméno>       # přidání uživatele do sudo
passwd <jméno>                 # změna hesla
whoami                         # aktuální uživatel
id                             # info o UID/GID
```

## 📂 Práce se soubory a oprávněními

```bash
ls -l                          # výpis se všemi detaily
chmod +x soubor.sh            # přidání spustitelnosti
chown uživatel:skupina soubor # změna vlastníka
chmod 755 soubor              # oprávnění (rwxr-xr-x)
touch soubor.txt              # vytvoření prázdného souboru
```

## 📶 Síť a připojení

```bash
ip a                           # IP adresy
ping google.com                # test připojení
netstat -tuln                 # seznam otevřených portů
ss -tuln                      # alternativní příkaz
ufw allow 22                  # povolit port (např. SSH)
ufw status                    # stav firewallu
```

## 🧰 Další užitečné

```bash
htop                           # interaktivní správce procesů
journalctl -xe                # podrobné logy systému
history                       # historie příkazů
crontab -e                    # naplánované úlohy
```

---

*Vytvořeno pro interní potřeby projektů [eKultura](https://ekultura.eu) z. s.*  

`#eKultura #Ubuntu #Server #Linux`

