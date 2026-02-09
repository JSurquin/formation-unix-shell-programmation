---
layout: new-section
routeAlias: 'fonctions-shell'
---

<a name="fonctions-shell" id="fonctions-shell"></a>

# 🔧 Module 4
## Fonctions Shell

### Modulariser et réutiliser le code

---

# Déclarer une fonction 📝

```bash
# Syntaxe 1 (recommandée)
ma_fonction() {
  echo "Bonjour depuis ma fonction !"
}

# Syntaxe 2 (avec le mot-clé function)
function ma_fonction2 {
  echo "Alternative"
}

# Appel
ma_fonction
ma_fonction2
```

---

# Paramètres de fonction 📥

```bash
saluer() {
  local nom="$1"
  local age="$2"
  echo "Bonjour $nom, vous avez $age ans"
}

saluer "Alice" 25
# Bonjour Alice, vous avez 25 ans

# $# = nombre d'arguments
# $@ = tous les arguments
# $1, $2, ... = arguments individuels

afficher_args() {
  echo "Nombre d'arguments : $#"
  for arg in "$@"; do
    echo "  - $arg"
  done
}
afficher_args "un" "deux" "trois"
```

---

# Valeurs de retour 📤

```bash
# Le return code (0-255) - pas une "vraie" valeur
est_pair() {
  if [[ $(($1 % 2)) -eq 0 ]]; then
    return 0  # Succès = vrai
  else
    return 1  # Échec = faux
  fi
}

if est_pair 4; then
  echo "4 est pair"
fi

# Pour retourner une valeur : echo
calculer() {
  local result=$(($1 + $2))
  echo $result
}

somme=$(calculer 10 20)
echo "Somme = $somme"  # 30
```

---

# Variables locales (local) 🔒

```bash
var_globale="je suis globale"

ma_fonction() {
  local var_locale="je suis locale"
  var_globale="modifiée par la fonction"
  echo "Dans la fonction : $var_locale"
}

ma_fonction
echo "Après : $var_globale"  # modifiée
echo "Locale : $var_locale"  # Vide !
```

**Bonne pratique :** Toujours utiliser `local` dans les fonctions.

---

# Fonctions avec gestion d'erreurs 🚨

```bash
log() {
  local level="$1"
  shift
  local message="$*"
  local timestamp=$(date '+%Y-%m-%d %H:%M:%S')
  echo "[$timestamp] [$level] $message"
}

die() {
  log "ERROR" "$*" >&2
  exit 1
}

# Utilisation
log "INFO" "Script démarré"
[[ -f "$config" ]] || die "Config $config non trouvée"
log "INFO" "Config chargée"
```

---

# Fonctions récursives 🔄

```bash
# Factorielle
factorielle() {
  local n=$1
  if [[ $n -le 1 ]]; then
    echo 1
  else
    local sub=$(factorielle $((n - 1)))
    echo $((n * sub))
  fi
}

echo "5! = $(factorielle 5)"  # 120

# Parcours récursif de répertoires
parcourir() {
  local dir="$1"
  local indent="$2"
  for item in "$dir"/*; do
    echo "${indent}$(basename "$item")"
    [[ -d "$item" ]] && parcourir "$item" "  $indent"
  done
}

parcourir "/etc/nginx" ""
```

---

# Bibliothèque de fonctions 📚

```bash
# lib/utils.sh
#!/usr/bin/env bash

log_info()  { echo "[INFO]  $*"; }
log_warn()  { echo "[WARN]  $*" >&2; }
log_error() { echo "[ERROR] $*" >&2; }

require_root() {
  [[ $EUID -eq 0 ]] || {
    log_error "Ce script nécessite les droits root"
    exit 1
  }
}

confirm() {
  read -p "$1 [o/N] " response
  [[ "$response" =~ ^[oOyY]$ ]]
}
```

---

# Utiliser la bibliothèque

```bash
#!/usr/bin/env bash
# mon_script.sh

# Charger la bibliothèque
source "$(dirname "$0")/lib/utils.sh"

# Utiliser les fonctions
log_info "Démarrage du script"

require_root

if confirm "Voulez-vous continuer ?"; then
  log_info "Continuation..."
else
  log_warn "Annulé par l'utilisateur"
  exit 0
fi
```

---

# getopts : parser les arguments CLI 🎛️

```bash
#!/usr/bin/env bash

usage() {
  echo "Usage: $0 [-v] [-o output] [-n count] file"
  exit 1
}

verbose=false
output="/dev/stdout"
count=10

while getopts "vo:n:h" opt; do
  case $opt in
    v) verbose=true ;;
    o) output="$OPTARG" ;;
    n) count="$OPTARG" ;;
    h) usage ;;
    *) usage ;;
  esac
done
shift $((OPTIND - 1))

# $1 contient maintenant le premier argument positionnel
file="${1:?Fichier requis}"
$verbose && echo "Traitement de $file..."
```

---

# Arguments longs (sans getopt) 📋

```bash
#!/usr/bin/env bash

while [[ $# -gt 0 ]]; do
  case "$1" in
    -v|--verbose)
      verbose=true
      shift
      ;;
    -o|--output)
      output="$2"
      shift 2
      ;;
    -n|--count)
      count="$2"
      shift 2
      ;;
```

---

# Arguments longs (suite)

```bash
    # suite du case
    -h|--help)
      usage
      ;;
    --)
      shift
      break
      ;;
    -*)
      echo "Option inconnue : $1" >&2
      exit 1
      ;;
    *)
      break
      ;;
  esac
done
```

---

# Bonnes pratiques de portabilité 🌍

**Pour que vos scripts fonctionnent partout :**

| Bash-ism | Alternative POSIX |
|----------|-------------------|
| `[[ ... ]]` | `[ ... ]` |
| `$(( ))` | `$(( ))` (OK en POSIX) |
| `${var,,}` | `echo "$var" \| tr 'A-Z' 'a-z'` |
| `declare -A` | Non disponible en sh |
| `<<<` (here string) | `echo "..." \| cmd` |
| `source` | `.` (point) |
| `function f {}` | `f() {}` |

**Règle :** Si le script utilise des bashisms, utiliser `#!/usr/bin/env bash`.
Si portabilité POSIX requise, utiliser `#!/bin/sh`.

---

# En résumé 📝

- `nom() { ... }` pour déclarer une fonction
- `$1`, `$2`, `$@`, `$#` pour les paramètres
- **return** pour le code retour (0-255)
- **echo** pour retourner des valeurs
- **local** : toujours l'utiliser dans les fonctions
- **source** pour charger des bibliothèques de fonctions
- **getopts** pour parser les options courtes
- **while/case/shift** pour les options longues
