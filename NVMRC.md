## 📄 **Co je .nvmrc soubor**

**.nvmrc** je konfigurační soubor pro **NVM (Node Version Manager)**, který definuje, jakou verzi Node.js má projekt používat. Je to textový soubor umístěný v kořenovém adresáři projektu.

---

## 🎯 **Jak .nvmrc funguje**

### **Základní princip:**
1. **NVM čte .nvmrc** soubor v aktuálním adresáři
2. **Automaticky přepne** na definovanou verzi Node.js
3. **Zajišťuje konzistenci** napříč týmem a prostředími

---

## 📝 **Syntaxe a formát**

### **Základní formát:**
```bash
# .nvmrc soubor obsahuje pouze verzi Node.js
18.17.0
```

### **Různé způsoby zápisu:**

#### **1. Konkrétní verze:**
```bash
18.17.0
20.11.0
16.20.2
```

#### **2. Major verze:**
```bash
18
20
16
```

#### **3. LTS aliasy:**
```bash
lts/hydrogen    # Node.js 18 LTS
lts/iron        # Node.js 20 LTS
lts/gallium     # Node.js 16 LTS
lts/*           # nejnovější LTS
```

#### **4. Jiné aliasy:**
```bash
node            # nejnovější stable verze
stable          # nejnovější stable verze
```

---

## 🛠️ **Vytvoření a použití .nvmrc**

### **Vytvoření .nvmrc souboru:**

#### **Metoda 1: Ruční vytvoření**
```bash
# V kořenovém adresáři projektu
echo "18.17.0" > .nvmrc
```

#### **Metoda 2: Z aktuální verze**
```bash
# Uloží aktuálně používanou verzi
node --version > .nvmrc

# Nebo pro NVM
nvm current > .nvmrc
```

#### **Metoda 3: Pomocí editoru**
```bash
# VS Code
code .nvmrc

# Nano
nano .nvmrc

# Notepad
notepad .nvmrc
```

### **Použití .nvmrc:**

#### **Linux/macOS:**
```bash
# V adresáři s .nvmrc
nvm use                    # automaticky načte verzi z .nvmrc

# Pokud verze není nainstalována
nvm install               # nainstaluje verzi z .nvmrc a použije ji
```

#### **Windows (nvm-windows):**
```powershell
# V adresáři s .nvmrc
nvm use $(Get-Content .nvmrc)

# Nebo čtení a instalace
$version = Get-Content .nvmrc
nvm install $version
nvm use $version
```

---

## ⚡ **Automatizace .nvmrc**

### **Automatické načítání (Linux/macOS)**

#### **Bash (.bashrc):**
```bash
# Automatické načítání .nvmrc při změně adresáře
cd() {
  builtin cd "$@"
  if [[ -f .nvmrc ]]; then
    nvm use
  fi
}
```

#### **Zsh (.zshrc):**
```bash
# Pokročilá automatizace pro Zsh
autoload -U add-zsh-hook
load-nvmrc() {
  local node_version="$(nvm version)"
  local nvmrc_path="$(nvm_find_nvmrc)"

  if [ -n "$nvmrc_path" ]; then
    local nvmrc_node_version=$(nvm version "$(cat "${nvmrc_path}")")

    if [ "$nvmrc_node_version" = "N/A" ]; then
      echo "Installing Node.js version from .nvmrc..."
      nvm install
    elif [ "$nvmrc_node_version" != "$node_version" ]; then
      echo "Switching to Node.js version from .nvmrc..."
      nvm use
    fi
  elif [ "$node_version" != "$(nvm version default)" ]; then
    echo "Reverting to default Node.js version..."
    nvm use default
  fi
}
add-zsh-hook chpwd load-nvmrc
load-nvmrc
```

#### **Fish Shell:**
```fish
# functions/nvm_auto_use.fish
function nvm_auto_use --on-variable PWD
  if test -f .nvmrc
    nvm use
  end
end
```

### **VS Code integrace:**

#### **settings.json:**
```json
{
  "terminal.integrated.shellIntegration.enabled": true,
  "terminal.integrated.shellIntegration.decorationsEnabled": "never",
  "nodejs.preferences.includePackageJsonAutoImports": "auto"
}
```

#### **tasks.json:**
```json
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "Use .nvmrc Node version",
      "type": "shell",
      "command": "nvm use",
      "group": "build",
      "presentation": {
        "echo": true,
        "reveal": "always",
        "focus": false,
        "panel": "shared"
      }
    }
  ]
}
```

---

## 👥 **Týmová spolupráce**

### **package.json integrace:**
```json
{
  "name": "my-project",
  "version": "1.0.0",
  "engines": {
    "node": ">=18.17.0",
    "npm": ">=9.0.0"
  },
  "scripts": {
    "preinstall": "node --version",
    "check-node": "node -e \"console.log('Node.js version:', process.version)\"",
    "nvm-use": "nvm use"
  }
}
```

### **README.md dokumentace:**
```markdown
## 🚀 Development Setup

### Node.js verze
Tento projekt vyžaduje Node.js verzi definovanou v `.nvmrc` souboru.

```bash
# Instalace správné verze Node.js
nvm install

# Použití správné verze
nvm use

# Ověření verze
node --version
```

### Rychlý start
```bash
git clone <repository>
cd <project>
nvm use
npm install
npm start
```
```

---

## 🔄 **CI/CD integrace**

### **GitHub Actions:**
```yaml
name: CI/CD Pipeline

on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main ]

jobs:
  test:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v3
    
    - name: Read Node.js version from .nvmrc
      run: echo "NODE_VERSION=$(cat .nvmrc)" >> $GITHUB_ENV
    
    - name: Setup Node.js
      uses: actions/setup-node@v3
      with:
        node-version: ${{ env.NODE_VERSION }}
        cache: 'npm'
    
    - name: Install dependencies
      run: npm ci
    
    - name: Run tests
      run: npm test
```

### **GitLab CI:**
```yaml
# .gitlab-ci.yml
image: node:$(cat .nvmrc)

before_script:
  - node --version
  - npm --version
  - npm ci

test:
  script:
    - npm test

build:
  script:
    - npm run build
  artifacts:
    paths:
      - dist/
```

### **Docker integrace:**
```dockerfile
# Dockerfile
# Čtení Node.js verze z .nvmrc
FROM node:$(shell cat .nvmrc)-alpine

WORKDIR /app

# Ověření verze
RUN node --version

COPY package*.json ./
RUN npm ci --only=production

COPY . .

EXPOSE 3000
CMD ["npm", "start"]
```

---

## 🏗️ **Pokročilé scénáře**

### **Monorepo s více .nvmrc:**
```bash
# Struktura projektu
project/
├── .nvmrc                 # 18.17.0 (root)
├── frontend/
│   └── .nvmrc            # 20.11.0 (React app)
├── backend/
│   └── .nvmrc            # 18.17.0 (Node.js API)
└── tools/
    └── .nvmrc            # 16.20.0 (legacy tools)
```

### **Skript pro automatickou detekci:**
```bash
#!/bin/bash
# auto-nvm.sh

find_and_use_nvmrc() {
  local current_dir="$PWD"
  
  while [[ "$current_dir" != "/" ]]; do
    if [[ -f "$current_dir/.nvmrc" ]]; then
      echo "Found .nvmrc in: $current_dir"
      cd "$current_dir"
      nvm use
      cd - > /dev/null
      return 0
    fi
    current_dir="$(dirname "$current_dir")"
  done
  
  echo "No .nvmrc found in current directory tree"
  return 1
}

find_and_use_nvmrc
```

### **Podmíněné .nvmrc:**
```bash
# .nvmrc s komentáři (neoficiální, ale užitečné pro dokumentaci)
# Production: 18.17.0 LTS
# Development: 20.11.0 (latest features)
# CI/CD: 18.17.0 (stability)
18.17.0
```

---

## 🚨 **Troubleshooting**

### **Časté problémy:**

#### **1. .nvmrc se nenačítá automaticky**
```bash
# Kontrola, zda je NVM správně nastaveno
echo $NVM_DIR
ls $NVM_DIR

# Restart terminálu
source ~/.bashrc
# nebo
source ~/.zshrc
```

#### **2. Verze v .nvmrc není dostupná**
```bash
# Kontrola dostupných verzí
nvm ls-remote

# Instalace konkrétní verze
nvm install 18.17.0

# Ověření .nvmrc souboru
cat .nvmrc
file .nvmrc  # kontrola typu souboru
```

#### **3. Windows problémy**
```powershell
# Kontrola kódování .nvmrc
Get-Content .nvmrc -Encoding UTF8

# Ruční čtení a použití
$version = (Get-Content .nvmrc).Trim()
nvm use $version
```

#### **4. Whitespace problémy**
```bash
# Odstranění whitespace z .nvmrc
sed -i 's/[[:space:]]*$//' .nvmrc

# Nebo pomocí tr
tr -d '\r\n' < .nvmrc > .nvmrc.tmp && mv .nvmrc.tmp .nvmrc
```

---

## ✅ **Best Practices**

### **1. Vždy commitujte .nvmrc**
```bash
git add .nvmrc
git commit -m "Add Node.js version specification"
```

### **2. Dokumentujte v README**
```markdown
## Node.js Setup
Projekt používá Node.js verzi definovanou v `.nvmrc`.

Para quick setup:
\```bash
nvm use && npm install
\```
```

### **3. Používejte LTS verze pro produkci**
```bash
# Pro produkční projekty
echo "lts/hydrogen" > .nvmrc

# Pro experimentální projekty
echo "20.11.0" > .nvmrc
```

### **4. Kombinace s package.json engines**
```json
{
  "engines": {
    "node": "$(cat .nvmrc)",
    "npm": ">=9.0.0"
  }
}
```

### **5. Git hooks integrace**
```bash
#!/bin/sh
# .git/hooks/post-checkout
if [ -f .nvmrc ]; then
  echo "Node.js version required: $(cat .nvmrc)"
  echo "Current version: $(node --version)"
  if command -v nvm > /dev/null 2>&1; then
    nvm use
  fi
fi
```

---

## 🎯 **Výhody .nvmrc**

- ✅ **Konzistence** napříč týmem
- ✅ **Automatizace** development setupu  
- ✅ **CI/CD integrace** s garantovanou verzí
- ✅ **Dokumentace** požadavků projektu
- ✅ **Prevence** problémů s kompatibilitou
- ✅ **Jednoduchost** onboardingu nových členů
- ✅ **Reproductibilita** builds

**.nvmrc** je jednoduché, ale velmi mocné řešení pro správu Node.js verzí v projektech a je klíčové pro profesionální development workflow!
