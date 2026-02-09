---

# Exercices Module 9 : Débogage 🎯

---

# Exercice : Corriger un script bugué (15 min)

**Consigne :** Ce script a 6 bugs. Trouvez-les et corrigez-les.

```bash
#!/bin/bash
echo "Backup de $backup_dir"
for file in $(ls $backup_dir)
do
  cp $file /tmp/backup/
  echo Copié: $file
done
count=`ls /tmp/backup | wc -l`
echo "Total: $count fichiers sauvegardés"
```

---

# Exercice : Solution ✅

**Bugs trouvés :**
1. Pas de `set -euo pipefail`
2. `$backup_dir` non définie (pas de `set -u`)
3. `$(ls ...)` au lieu de glob
4. Variables non quotées
5. Backticks au lieu de `$()`
6. Pas de vérification que /tmp/backup existe

```bash
#!/usr/bin/env bash
set -euo pipefail

backup_dir="${1:?Usage: $0 <répertoire>}"
dest="/tmp/backup"

mkdir -p "$dest"
echo "Backup de $backup_dir"

for file in "$backup_dir"/*; do
  [[ -f "$file" ]] || continue
  cp "$file" "$dest/"
  echo "Copié: $file"
done

count=$(find "$dest" -type f | wc -l)
echo "Total: $count fichiers sauvegardés"
```
