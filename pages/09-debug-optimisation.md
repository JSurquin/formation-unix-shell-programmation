---
layout: new-section
routeAlias: 'debug-optimisation'
---

<a name="debug-optimisation" id="debug-optimisation"></a>

# 🔍 Module 9
## Débogage et Optimisation

### Écrire des scripts fiables et performants

---

# Bash Strict Mode 🔒

```bash
#!/usr/bin/env bash
set -euo pipefail

# set -e : arrêter sur la première erreur
# set -u : erreur sur variable non définie
# set -o pipefail : erreur si un pipe échoue

# IFS pour éviter les problèmes de mots
IFS=$'\n\t'
```

**C'est la PREMIÈRE chose à mettre dans tout script professionnel !**

---

# Options de débogage 🐛

```bash
# Mode trace : affiche chaque commande
set -x     # Activer
set +x     # Désactiver

# Mode verbose : affiche les lignes avant exécution
set -v

# Déboguer une section spécifique
set -x
# Code à déboguer
problematic_function
set +x

# Exécuter avec débogage
bash -x mon_script.sh

# Variable PS4 pour personnaliser le prefix de trace
export PS4='+(${BASH_SOURCE}:${LINENO}): ${FUNCNAME[0]:+${FUNCNAME[0]}(): }'
```

---

# shellcheck : le linter indispensable ✅

```bash
# Installation
sudo apt install shellcheck   # Debian/Ubuntu
brew install shellcheck        # macOS

# Utilisation
shellcheck mon_script.sh

# Exemple de sortie :
# In mon_script.sh line 3:
# echo $var
#      ^-- SC2086: Double quote to prevent
#          globbing and word splitting.
```

**shellcheck** détecte :
- Variables non quotées
- Usages dangereux
- Problèmes de portabilité
- Erreurs de syntaxe subtiles

---

# Logging professionnel 📋

```bash
#!/usr/bin/env bash

LOGFILE="/var/log/monscript.log"
VERBOSE=${VERBOSE:-false}

log() {
  local level="$1"; shift
  local ts=$(date '+%Y-%m-%d %H:%M:%S')
  local msg="[$ts] [$level] [$$] $*"
  echo "$msg" >> "$LOGFILE"
  $VERBOSE && echo "$msg"
}

log "INFO" "Script démarré"
log "WARN" "Espace disque faible"
log "ERROR" "Fichier introuvable"
```

---

# Gestion d'erreurs avancée 🚨

```bash
#!/usr/bin/env bash
set -euo pipefail

# Trap sur les erreurs
trap 'error_handler $? $LINENO' ERR

error_handler() {
  local exit_code=$1
  local line_number=$2
  echo "ERREUR : code $exit_code à la ligne $line_number" >&2
  echo "Commande : ${BASH_COMMAND}" >&2
}

# Ou try/catch style
try() {
  "$@"
  return $?
}

catch() {
  local exit_code=$?
  if [[ $exit_code -ne 0 ]]; then
    echo "Erreur capturée : $exit_code" >&2
  fi
  return $exit_code
}
```

---

# Optimisation de performance ⚡

```bash
# 1. Éviter les sous-shells inutiles
# ❌ Lent
result=$(echo "$string" | tr 'a-z' 'A-Z')
# ✅ Rapide
result="${string^^}"

# 2. Éviter les boucles avec des appels externes
# ❌ Lent
while read line; do
  echo "$line" | grep "pattern"
done < fichier
# ✅ Rapide
grep "pattern" fichier

# 3. Utiliser des builtins
# ❌ Lent
count=$(cat fichier | wc -l)
# ✅ Rapide
count=$(wc -l < fichier)
```

---

# Template de script professionnel 📋

```bash
#!/usr/bin/env bash
set -euo pipefail

# === Configuration ===
readonly SCRIPT_DIR="$(cd "$(dirname "$0")" && pwd)"
readonly SCRIPT_NAME="$(basename "$0")"
readonly VERSION="1.0.0"
readonly LOG_FILE="/var/log/${SCRIPT_NAME%.sh}.log"

# === Fonctions utilitaires ===
source "${SCRIPT_DIR}/lib/utils.sh" 2>/dev/null || true

log()  { echo "[$(date '+%F %T')] $*" | tee -a "$LOG_FILE"; }
die()  { log "FATAL: $*" >&2; exit 1; }
usage() {
  cat << EOF
Usage: $SCRIPT_NAME [OPTIONS] <argument>
Options:
  -v, --verbose    Mode verbeux
  -h, --help       Afficher cette aide
  --version        Afficher la version
EOF
  exit 0
}
```

---

# Template (suite et fin)

```bash
# === Parsing des arguments ===
verbose=false
while [[ $# -gt 0 ]]; do
  case "$1" in
    -v|--verbose) verbose=true; shift ;;
    -h|--help)    usage ;;
    --version)    echo "$VERSION"; exit 0 ;;
    --)           shift; break ;;
    -*)           die "Option inconnue: $1" ;;
    *)            break ;;
  esac
done

# === Traps ===
cleanup() { log "Nettoyage..."; rm -f "$tmpfile"; }
trap cleanup EXIT
trap 'die "Interrompu"' INT TERM

# === Main ===
main() {
  local arg="${1:?$(usage)}"
  log "Début du traitement: $arg"
  tmpfile=$(mktemp)
  # ... votre code ici ...
  log "Terminé avec succès"
}

main "$@"
```

---

# En résumé 📝

- **set -euo pipefail** : toujours en première ligne
- **set -x** pour le mode trace (débogage)
- **shellcheck** : linter indispensable
- **Logging** structuré avec timestamp et niveaux
- **trap ERR** pour capturer les erreurs avec contexte
- **Builtins** plutôt que commandes externes
- **Template professionnel** : config, logging, args, traps, main
