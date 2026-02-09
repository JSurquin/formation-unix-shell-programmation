---
layout: new-section
routeAlias: 'gestion-fichiers'
---

<a name="gestion-fichiers" id="gestion-fichiers"></a>

# 📁 Module 7
## Gestion avancée des fichiers

### find, xargs, descripteurs et verrouillage

---

# find avancé 🔍

```bash
# Trouver par nom
find /var/log -name "*.log" -type f

# Trouver par taille
find . -size +100M          # Plus de 100Mo
find . -size -1k            # Moins de 1Ko

# Trouver par date
find . -mtime -7            # Modifié il y a moins de 7j
find . -mmin -30            # Modifié il y a moins de 30min

# Trouver par permissions
find . -perm 755
find . -perm /u+x           # Exécutable par le propriétaire

# Combiner avec -exec
find . -name "*.tmp" -exec rm {} \;
find . -name "*.sh" -exec chmod +x {} \;

# -exec avec confirmation
find . -name "*.bak" -exec rm -i {} \;
```

---

# xargs : construire des commandes 🔗

```bash
# Supprimer les fichiers trouvés (plus rapide que -exec)
find . -name "*.tmp" | xargs rm

# Avec gestion des espaces dans les noms
find . -name "*.log" -print0 | xargs -0 rm

# Limiter le nombre d'arguments
find . -name "*.jpg" | xargs -n 5 ls -la

# Paralléliser
find . -name "*.png" | xargs -P 4 -I {} \
  convert {} -resize 50% resized_{}

# xargs avec confirmation
echo "fichier1 fichier2" | xargs -p rm
```

---

# Descripteurs de fichiers 📝

```bash
# Ouvrir un fichier en lecture (FD 3)
exec 3< input.txt
while read -u 3 ligne; do
  echo "Lu : $ligne"
done
exec 3<&-  # Fermer le FD

# Ouvrir un fichier en écriture (FD 4)
exec 4> output.txt
echo "Ligne 1" >&4
echo "Ligne 2" >&4
exec 4>&-  # Fermer le FD

# Lire et écrire simultanément
exec 5<> fichier.txt
read -u 5 premiere_ligne
echo "Ajout" >&5
exec 5>&-
```

---

# Fichiers temporaires sécurisés 🔒

```bash
# mktemp : crée un fichier temporaire unique
tmpfile=$(mktemp)
echo "Données temporaires" > "$tmpfile"
echo "Fichier temp : $tmpfile"

# Répertoire temporaire
tmpdir=$(mktemp -d)

# Template personnalisé
tmpfile=$(mktemp /tmp/monscript.XXXXXX)

# Nettoyage automatique avec trap
cleanup() {
  rm -rf "$tmpfile" "$tmpdir"
}
trap cleanup EXIT

# Utilisation
tmpfile=$(mktemp)
trap 'rm -f "$tmpfile"' EXIT
echo "data" > "$tmpfile"
```

---

# Verrouillage de fichiers (flock) 🔐

```bash
# Empêcher l'exécution simultanée d'un script
(
  flock -n 9 || {
    echo "Script déjà en cours"
    exit 1
  }
  # Code protégé ici
  echo "Exécution exclusive..."
  sleep 10
) 9>/var/lock/monscript.lock

# Version simplifiée
LOCKFILE="/tmp/monscript.lock"
if ! mkdir "$LOCKFILE" 2>/dev/null; then
  echo "Déjà en cours d'exécution"
  exit 1
fi
trap 'rmdir "$LOCKFILE"' EXIT
```

---

# En résumé 📝

- **find** : recherche avancée avec `-exec`
- **xargs** : construire des commandes à partir de stdin
- `-print0` / `-0` pour les noms avec espaces
- **Descripteurs de fichiers** : `exec N<>fichier`
- **mktemp** pour les fichiers temporaires sécurisés
- **flock** ou `mkdir` pour le verrouillage
- **trap EXIT** pour le nettoyage automatique
