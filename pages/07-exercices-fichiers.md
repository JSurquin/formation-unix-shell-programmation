---

# Exercices Module 7 : Gestion de fichiers 🎯

---

# Exercice : Script de nettoyage sécurisé (20 min)

**Consigne :** Créez un script qui :
1. Utilise un fichier lock pour empêcher l'exécution simultanée
2. Trouve tous les fichiers `.tmp` et `.bak` de plus de 7 jours dans /tmp
3. Les liste dans un fichier temporaire
4. Demande confirmation avant suppression
5. Nettoie tout à la sortie (trap)

---

# Exercice : Solution (setup + lock) ✅

```bash
#!/usr/bin/env bash

LOCKDIR="/tmp/cleanup.lock"
tmpfile=$(mktemp)

cleanup() {
  rm -f "$tmpfile"
  rmdir "$LOCKDIR" 2>/dev/null
}
trap cleanup EXIT

# Verrouillage
mkdir "$LOCKDIR" 2>/dev/null || {
  echo "Déjà en cours"; exit 1
}
```

---

# Exercice : Solution (recherche + suppression) ✅

```bash
# Trouver les fichiers
find /tmp -type f \( -name "*.tmp" -o -name "*.bak" \) \
  -mtime +7 > "$tmpfile" 2>/dev/null

count=$(wc -l < "$tmpfile")
echo "Fichiers trouvés : $count"

if [[ $count -gt 0 ]]; then
  cat "$tmpfile"
  read -p "Supprimer ? [o/N] " rep
  if [[ "$rep" =~ ^[oOyY]$ ]]; then
    xargs -a "$tmpfile" rm -f
    echo "Nettoyage effectué"
  fi
else
  echo "Rien à nettoyer"
fi
```
