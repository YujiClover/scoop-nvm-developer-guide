# 🚀 Kompletní průvodce Scoop a NVM pro vývojáře

> **Moderní správa balíčků a verzí Node.js na Windows**

## 📋 Obsah

- [🔧 Co jsou Scoop a NVM](#-co-jsou-scoop-a-nvm)
- [⚡ Rychlé začátky](#-rychlé-začátky)
- [📦 Instalace Scoop](#-instalace-scoop)
- [🔄 Instalace NVM](#-instalace-nvm)
- [🎯 Základní použití](#-základní-použití)
- [🛠️ Pokročilé scénáře](#️-pokročilé-scénáře)
- [💡 Best Practices](#-best-practices)
- [🔍 Troubleshooting](#-troubleshooting)
- [🆚 Alternativy](#-alternativy)

---

## 🔧 Co jsou Scoop a NVM

### **Scoop** 
**Package manager pro Windows** podobný Homebrew (macOS) nebo APT (Linux)
- ✅ Instaluje software z příkazové řádky
- ✅ Automatické aktualizace
- ✅ Žádné admin práva potřeba
- ✅ Čisté odinstalace bez zbytků v registrech

### **NVM (Node Version Manager)**
**Správce verzí Node.js** pro práci s více verzemi současně
- ✅ Rychlé přepínání mezi verzemi Node.js
- ✅ Izolace projektů podle verzí
- ✅ Podpora .nvmrc souborů
- ✅ Testování na různých verzích

---

## ⚡ Rychlé začátky

### Kompletní setup za 5 minut:

```powershell
# 1. Instalace Scoop
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
iwr -useb get.scoop.sh | iex

# 2. Instalace NVM přes Scoop
scoop install nvm

# 3. Instalace Node.js verzí
nvm install 18.17.0
nvm install 20.11.0
nvm use 18.17.0

# 4. Ověření
node --version
npm --version
```

---

## 📦 Instalace Scoop

### Předpoklady
- **Windows 10/11**
- **PowerShell 5.0+** (obvykle již nainstalován)

### Krok za krokem

#### 1. Otevřete PowerShell
```powershell
# Klikněte Win + X, vyberte "Windows PowerShell"
# NEBO stiskněte Win + R, napište "powershell"
```

#### 2. Nastavte execution policy
```powershell
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
```
> ⚠️ **Důležité**: Toto umožní spouštění skriptů, je to bezpečné pro CurrentUser

#### 3. Instalace Scoop
```powershell
# Standardní instalace
iwr -useb get.scoop.sh | iex

# Alternativní způsob
Invoke-RestMethod get.scoop.sh | Invoke-Expression
```

#### 4. Ověření instalace
```powershell
scoop --version
scoop help
```

### Přidání užitečných buckets
```powershell
# Hlavní buckets
scoop bucket add extras        # GUI aplikace, fonty
scoop bucket add versions      # Starší verze aplikací
scoop bucket add java          # Java JDK/JRE
scoop bucket add games         # Hry
scoop bucket add nerd-fonts    # Programátorské fonty
```

---

## 🔄 Instalace NVM

### Metoda 1: Přes Scoop (doporučeno)
```powershell
# Instalace NVM
scoop install nvm

# Ověření
nvm --version
```

### Metoda 2: Přímá instalace (Windows)
1. Stáhněte `nvm-setup.exe` z [GitHub releases](https://github.com/coreybutler/nvm-windows/releases)
2. Spusťte installer
3. Restartujte PowerShell

### Metoda 3: Linux/macOS
```bash
# cURL
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash

# Wget
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash

# Reload bashrc
source ~/.bashrc
```

---

## 🎯 Základní použití

### Scoop - Správa aplikací

#### Hledání a instalace
```powershell
# Hledání aplikace
scoop search nodejs
scoop search git

# Instalace aplikace
scoop install git
scoop install nodejs
scoop install python
scoop install vscode

# Instalace více aplikací najednou
scoop install git nodejs python vscode
```

#### Aktualizace
```powershell
# Aktualizace Scoop samého
scoop update

# Kontrola dostupných aktualizací
scoop status

# Aktualizace konkrétní aplikace
scoop update nodejs

# Aktualizace všech aplikací
scoop update *
```

#### Správa aplikací
```powershell
# Seznam nainstalovaných aplikací
scoop list

# Informace o aplikaci
scoop info nodejs

# Odinstalace aplikace
scoop uninstall nodejs

# Vyčištění starých verzí
scoop cleanup *
```

### NVM - Správa verzí Node.js

#### Dostupné verze
```powershell
# Windows
nvm list available

# Linux/macOS  
nvm ls-remote
nvm ls-remote --lts
```

#### Instalace verzí
```powershell
# Konkrétní verze
nvm install 18.17.0
nvm install 20.11.0

# LTS verze
nvm install --lts              # Linux/macOS
nvm install lts               # Windows

# Nejnovější verze
nvm install node              # Linux/macOS
nvm install latest            # Windows
```

#### Přepínání verzí
```powershell
# Použití konkrétní verze
nvm use 18.17.0

# Použití LTS
nvm use --lts                 # Linux/macOS
nvm use lts                   # Windows

# Aktuální verze
nvm current

# Seznam nainstalovaných verzí
nvm list                      # Windows
nvm ls                        # Linux/macOS
```

#### Výchozí verze
```powershell
# Linux/macOS
nvm alias default 18.17.0
nvm use default

# Windows
nvm use 18.17.0  # automaticky se stane výchozí
```

---

## 🛠️ Pokročilé scénáře

### 1. Správa více verzí Node.js současně

#### Pomocí Scoop buckets
```powershell
# Přidání versions bucket
scoop bucket add versions

# Instalace různých verzií
scoop install nodejs-lts       # LTS verze
scoop install versions/nodejs16
scoop install versions/nodejs18
scoop install nodejs          # nejnovější

# Přepínání verzí
scoop reset nodejs16
node --version  # v16.x.x

scoop reset nodejs18
node --version  # v18.x.x
```

#### Pomocí NVM + konkrétní verze
```powershell
# Instalace více verzií
nvm install 16.20.0
nvm install 18.17.0
nvm install 20.11.0

# Rychlé přepínání
nvm use 16.20.0
npm install -g typescript

nvm use 18.17.0
npm install -g @angular/cli

nvm use 20.11.0
npm install -g create-react-app
```

### 2. Projektová konfigurace (.nvmrc)

#### Vytvoření .nvmrc souboru
```bash
# V kořenovém adresáři projektu
echo "18.17.0" > .nvmrc

# Nebo specify LTS
echo "lts/hydrogen" > .nvmrc
```

#### Použití .nvmrc
```powershell
# V adresáři s .nvmrc
nvm use                       # automaticky načte verzi

# Instalace verze z .nvmrc (pokud není nainstalována)
nvm install                   # Linux/macOS
```

#### Automatické načítání .nvmrc (Linux/macOS)
Přidejte do `~/.bashrc` nebo `~/.zshrc`:
```bash
# Auto-switch node versions
autoload -U add-zsh-hook
load-nvmrc() {
  local node_version="$(nvm version)"
  local nvmrc_path="$(nvm_find_nvmrc)"

  if [ -n "$nvmrc_path" ]; then
    local nvmrc_node_version=$(nvm version "$(cat "${nvmrc_path}")")

    if [ "$nvmrc_node_version" = "N/A" ]; then
      nvm install
    elif [ "$nvmrc_node_version" != "$node_version" ]; then
      nvm use
    fi
  elif [ "$node_version" != "$(nvm version default)" ]; then
    echo "Reverting to nvm default version"
    nvm use default
  fi
}
add-zsh-hook chpwd load-nvmrc
load-nvmrc
```

### 3. Globální balíčky pro různé verze

#### Migrace globálních balíčků
```powershell
# Linux/macOS - kopírování globálních balíčků
nvm install 20.11.0 --reinstall-packages-from=18.17.0

# Ruční instalace nejpoužívanějších
nvm use 20.11.0
npm install -g yarn typescript eslint prettier nodemon
```

#### Seznam globálních balíčků
```powershell
# Zobrazení globálních balíčků
npm list -g --depth=0

# Export globálních balíčků
npm list -g --depth=0 --json > global-packages.json
```

### 4. Development workflow s různými projekty

#### React projekt (Node.js 18+)
```powershell
mkdir my-react-app
cd my-react-app

# Nastavení Node.js verze
echo "18.17.0" > .nvmrc
nvm use

# Vytvoření projektu
npx create-react-app .
npm start
```

#### Node.js API (Node.js 20+)
```powershell
mkdir my-api
cd my-api

# Nastavení nejnovější LTS
echo "20.11.0" > .nvmrc
nvm use

# Inicializace projektu
npm init -y
npm install express
```

#### Legacy projekt (Node.js 16)
```powershell
cd legacy-project

# Starší verze pro kompatibilitu
echo "16.20.0" > .nvmrc
nvm install 16.20.0
nvm use

npm install
npm run build
```

### 5. CI/CD konfigurace

#### GitHub Actions
```yaml
name: Test Multiple Node Versions
on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        node-version: [16.x, 18.x, 20.x]
    
    steps:
    - uses: actions/checkout@v3
    - name: Use Node.js ${{ matrix.node-version }}
      uses: actions/setup-node@v3
      with:
        node-version: ${{ matrix.node-version }}
        cache: 'npm'
    - run: npm ci
    - run: npm test
```

#### Docker s NVM
```dockerfile
FROM ubuntu:latest
ARG NODE_VERSION=18.17.0

# Install curl
RUN apt update && apt install curl -y

# Install NVM
RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash

# Set environment
ENV NVM_DIR=/root/.nvm

# Install Node
RUN bash -c "source $NVM_DIR/nvm.sh && nvm install $NODE_VERSION"

# Set entrypoint
ENTRYPOINT ["bash", "-c", "source $NVM_DIR/nvm.sh && exec \"$@\"", "--"]
CMD ["/bin/bash"]
```

---

## 💡 Best Practices

### Scoop Best Practices

#### 1. Organizace aplikací
```powershell
# Obvyklé vývojářské nástroje
scoop install git nodejs python go rust

# GUI nástroje (z extras bucket)
scoop bucket add extras
scoop install vscode postman figma

# Databases a services
scoop install postgresql redis mongodb
```

#### 2. Pravidelná údržba
```powershell
# Týdenní rutina
scoop update *
scoop cleanup *
scoop cache rm *

# Ověření zdraví systému
scoop checkup
```

#### 3. Backup konfigurace
```powershell
# Export nainstalovaných aplikací
scoop export > scoop-backup.json

# Restore na novém systému
scoop import scoop-backup.json
```

### NVM Best Practices

#### 1. Projektové standardy
```powershell
# Vždy vytvořte .nvmrc pro nové projekty
echo "18.17.0" > .nvmrc

# Dokumentujte požadavky v README.md
echo "## Development Setup" >> README.md
echo "Node.js version: \`$(cat .nvmrc)\`" >> README.md
```

#### 2. Týmová spolupráce
```json
// package.json
{
  "engines": {
    "node": ">=18.17.0",
    "npm": ">=9.0.0"
  },
  "scripts": {
    "preinstall": "node --version"
  }
}
```

#### 3. Testování kompatibility
```powershell
# Skript pro testování na více verzích
$versions = @("16.20.0", "18.17.0", "20.11.0")

foreach ($version in $versions) {
    Write-Host "Testing on Node.js $version" -ForegroundColor Green
    nvm use $version
    npm test
    if ($LASTEXITCODE -ne 0) {
        Write-Host "Tests failed on $version" -ForegroundColor Red
        break
    }
}
```

#### 4. Performance optimalizace
```powershell
# Nastavení rychlejšího registru (pro Evropu)
npm config set registry https://registry.npmjs.org/

# Povolit paralelní downloads
npm config set maxsockets 20

# Cache optimalizace
npm config set cache-max 3600000
```

---

## 🔍 Troubleshooting

### Časté problémy se Scoop

#### Problém: Scoop se nenainstaluje
```powershell
# Řešení: Zkontrolujte execution policy
Get-ExecutionPolicy -Scope CurrentUser

# Nastavte správnou policy
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser -Force

# Alternativní instalace
iwr -useb 'https://raw.githubusercontent.com/scoopinstaller/install/master/install.ps1' | iex
```

#### Problém: Aplikace se nenainstaluje
```powershell
# Zkontrolujte dostupnost bucket
scoop bucket list

# Aktualizujte manifesty
scoop update

# Verbose log pro debugging
scoop install nodejs --verbose
```

#### Problém: PATH konflikty
```powershell
# Zobrazení PATH
$env:PATH -split ';'

# Reset Scoop aplikace
scoop reset nodejs

# Kontrola shimů
ls ~\scoop\shims\
```

### Časté problémy s NVM

#### Problém: NVM příkazy nefungují
```powershell
# Windows: Restartujte PowerShell po instalaci
# Linux/macOS: Znovu načtěte profile
source ~/.bashrc
# nebo
source ~/.zshrc
```

#### Problém: Verze se nepřepíná
```powershell
# Kontrola PATH priority
where node

# Windows: Ověřte admin práva
# Možná je potřeba spustit jako admin

# Reset NVM
nvm unload  # Linux/macOS
nvm use system  # pak znovu nvm use <version>
```

#### Problém: .nvmrc se nenačítá
```bash
# Kontrola současného adresáře
pwd
ls -la .nvmrc

# Ruční načtení
nvm use $(cat .nvmrc)

# Debug autoload (Linux/macOS)
echo $NVM_DIR
ls $NVM_DIR
```

### Performance problémy

#### Pomalé spouštění terminálu
```bash
# Linux/macOS: Lazy loading NVM
export NVM_DIR="$HOME/.nvm"
alias nvm="unalias nvm; [ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"; nvm"
```

#### Síťové problémy
```powershell
# Proxy nastavení pro Scoop
scoop config proxy http://proxy.company.com:8080

# NPM proxy
npm config set proxy http://proxy.company.com:8080
npm config set https-proxy http://proxy.company.com:8080
```

---

## 🆚 Alternativy

### Alternativy k Scoop

| Nástroj | Výhody | Nevýhody |
|---------|--------|----------|
| **Chocolatey** | Největší databáze balíčků | Vyžaduje admin práva |
| **Winget** | Oficiální Microsoft | Menší výběr aplikací |
| **Ninite** | GUI interface | Jen základní aplikace |

#### Chocolatey
```powershell
# Instalace
Set-ExecutionPolicy Bypass -Scope Process -Force
iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))

# Použití
choco install nodejs
choco upgrade all
```

#### Winget
```powershell
# Vestavěno ve Windows 11
winget search nodejs
winget install OpenJS.NodeJS
winget upgrade --all
```

### Alternativy k NVM

| Nástroj | Platformy | Výhody | Nevýhody |
|---------|-----------|--------|----------|
| **Volta** | Cross-platform | Rychlé, moderní | Novější, menší komunita |
| **n** | Linux/macOS | Jednoduché | Jen Unix systémy |
| **fnm** | Cross-platform | Velmi rychlé | Rust dependency |
| **asdf** | Cross-platform | Multi-tool manager | Komplexnější setup |

#### Volta (doporučená alternativa)
```powershell
# Instalace
scoop install volta

# Použití
volta install node@18.17.0
volta pin node@18.17.0  # pro projekt
```

#### fnm (nejrychlejší)
```powershell
# Instalace
scoop install fnm

# Použití
fnm install 18.17.0
fnm use 18.17.0
fnm default 18.17.0
```

---

## 📚 Užitečné odkazy

### Dokumentace
- [Scoop Official Documentation](https://scoop.sh/)
- [NVM Windows GitHub](https://github.com/coreybutler/nvm-windows)
- [NVM Unix GitHub](https://github.com/nvm-sh/nvm)

### Komunita
- [Scoop GitHub Issues](https://github.com/ScoopInstaller/Scoop/issues)
- [NVM Discussions](https://github.com/nvm-sh/nvm/discussions)

### Bucket repozitáře
- [Scoop Main Bucket](https://github.com/ScoopInstaller/Main)
- [Scoop Extras Bucket](https://github.com/ScoopInstaller/Extras)
- [Community Buckets](https://github.com/rasa/scoop-directory)

---

## 🎉 Závěr

Kombinace **Scoop + NVM** poskytuje výkonný a flexibilní způsob správy vývojového prostředí na Windows. Tento setup vám umožní:

- 🚀 **Rychlou instalaci** vývojářských nástrojů
- 🔄 **Snadné přepínání** mezi verzemi Node.js
- 🛡️ **Čisté prostředí** bez problémů s registry
- 👥 **Týmovou spolupráci** s konzistentními verzemi
- 🧪 **Testování** na různých verzích Node.js

**Doporučený workflow:**
1. Nainstalujte Scoop pro obecné nástroje
2. Přes Scoop nainstalujte NVM
3. Používejte NVM pro správu Node.js verzí
4. Vytvářejte .nvmrc soubory pro projekty
5. Pravidelně aktualizujte nástroje

---

*💡 Tip: Označte tento repozitář hvězdičkou, pokud vám pomohl! Přispějte s improvements přes Pull Requests.*
