---
layout: new-section
routeAlias: 'signaux-traps'
---

<a name="signaux-traps" id="signaux-traps"></a>

# 🚨 Module 8
## Signaux et Traps

### Gérer les interruptions et le nettoyage

---

# Les signaux Unix 📡

| Signal | Numéro | Description |
|--------|--------|-------------|
| SIGHUP | 1 | Terminal fermé |
| SIGINT | 2 | Ctrl+C |
| SIGQUIT | 3 | Ctrl+\\ |
| SIGKILL | 9 | Kill immédiat (non capturable) |
| SIGTERM | 15 | Terminaison propre (défaut de kill) |
| SIGUSR1 | 10 | Signal utilisateur 1 |
| SIGUSR2 | 12 | Signal utilisateur 2 |
| SIGCHLD | 17 | Processus fils terminé |

```bash
# Lister les signaux
kill -l

# Envoyer un signal
kill -SIGTERM $PID
kill -15 $PID
```

---

# trap : capturer les signaux 🪤

```bash
#!/usr/bin/env bash

# Capturer Ctrl+C
trap 'echo " Ctrl+C intercepté !"' INT

# Nettoyage à la sortie
trap 'echo "Nettoyage..."; rm -f /tmp/myapp.*' EXIT

# Capturer plusieurs signaux
trap 'echo "Signal reçu, arrêt propre..."' INT TERM HUP

# Ignorer un signal
trap '' INT  # Ignore Ctrl+C

# Réinitialiser un signal
trap - INT   # Comportement par défaut
```

---

# Pattern de script robuste 💪

```bash
#!/usr/bin/env bash

# Variables globales
TMPDIR=""
RUNNING=true

# Fonction de nettoyage
cleanup() {
  RUNNING=false
  echo "Nettoyage en cours..."
  [[ -d "$TMPDIR" ]] && rm -rf "$TMPDIR"
  echo "Terminé proprement"
}

# Installer les traps
trap cleanup EXIT
trap 'echo "Interruption !"; exit 1' INT TERM

# Créer les ressources
TMPDIR=$(mktemp -d)
echo "Travail dans $TMPDIR"

# Boucle principale
while $RUNNING; do
  echo "Travail en cours..."
  sleep 2
done
```

---

# Couleurs et formatage dans le terminal 🎨

```bash
# Codes ANSI
RED='\033[0;31m'
GREEN='\033[0;32m'
YELLOW='\033[1;33m'
BLUE='\033[0;34m'
BOLD='\033[1m'
NC='\033[0m'  # No Color (reset)

# Fonctions colorées
success() { echo -e "${GREEN}✅ $*${NC}"; }
warning() { echo -e "${YELLOW}⚠️  $*${NC}"; }
error()   { echo -e "${RED}❌ $*${NC}" >&2; }
info()    { echo -e "${BLUE}ℹ️  $*${NC}"; }
header()  { echo -e "${BOLD}=== $* ===${NC}"; }

# Utilisation
header "Déploiement en cours"
info "Vérification des dépendances..."
success "Tout est OK"
warning "Version de Node.js ancienne"
error "Fichier de config manquant"
```

---

# Barre de progression 📊

```bash
progress_bar() {
  local current=$1
  local total=$2
  local width=50
  local pct=$((current * 100 / total))
  local filled=$((current * width / total))
  local empty=$((width - filled))

  printf "\r["
  printf "%${filled}s" | tr ' ' '█'
  printf "%${empty}s" | tr ' ' '░'
  printf "] %3d%% (%d/%d)" "$pct" "$current" "$total"
}

# Utilisation
total=100
for ((i = 1; i <= total; i++)); do
  progress_bar $i $total
  sleep 0.05
done
echo  # Nouvelle ligne à la fin
```

---

# En résumé 📝

- **Signaux** : mécanisme de communication entre processus
- **SIGINT** (Ctrl+C), **SIGTERM** (kill par défaut)
- **SIGKILL** (9) : non capturable
- **trap** : capturer les signaux et exécuter du code
- **trap cleanup EXIT** : nettoyage garanti à la sortie
- Pattern robuste : trap + cleanup + fichiers temporaires
- **Codes ANSI** pour colorer les messages
- **Barre de progression** pour le feedback utilisateur
