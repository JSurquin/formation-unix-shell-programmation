---

# Exercices Module 4 : Fonctions 🎯

---

# Exercice : Bibliothèque de fonctions utilitaires (20 min)

**Consigne :** Créez un fichier `lib/utils.sh` avec les fonctions :
1. `log_info`, `log_warn`, `log_error` (avec timestamp)
2. `confirm` (demande oui/non)
3. `require_cmd` (vérifie qu'une commande existe)
4. `is_root` (vérifie si root)

Puis créez un script `main.sh` qui utilise ces fonctions.

---

# Exercice : Solution (utils.sh)

```bash
#!/usr/bin/env bash
# lib/utils.sh

_log() {
  local level="$1"; shift
  local ts=$(date '+%Y-%m-%d %H:%M:%S')
  echo "[$ts] [$level] $*"
}

log_info()  { _log "INFO" "$@"; }
log_warn()  { _log "WARN" "$@" >&2; }
log_error() { _log "ERROR" "$@" >&2; }

confirm() {
  local msg="${1:-Continuer ?}"
  read -p "$msg [o/N] " rep
  [[ "$rep" =~ ^[oOyY]$ ]]
}

require_cmd() {
  command -v "$1" &>/dev/null || {
    log_error "Commande '$1' non trouvée"
    return 1
  }
}

is_root() { [[ $EUID -eq 0 ]]; }
```

---

# Exercice : Solution (main.sh)

```bash
#!/usr/bin/env bash
# main.sh

source "$(dirname "$0")/lib/utils.sh"

log_info "=== Démarrage du script ==="

# Vérifier les dépendances
for cmd in git curl jq; do
  require_cmd "$cmd" || exit 1
done
log_info "Toutes les dépendances OK"

# Vérifier les droits
if is_root; then
  log_warn "Exécution en root"
else
  log_info "Exécution en tant que $USER"
fi

# Demander confirmation
if confirm "Lancer le traitement ?"; then
  log_info "Traitement en cours..."
  sleep 2
  log_info "Traitement terminé"
else
  log_warn "Annulé"
fi
```
