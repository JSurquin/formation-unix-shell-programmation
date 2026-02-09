---

# Exercices Module 2 : Variables 🎯

---

# Exercice 1 : Manipulation de chaînes (10 min)

**Consigne :** Écrivez un script qui :
1. Demande un chemin de fichier à l'utilisateur
2. Affiche le nom du fichier (sans le chemin)
3. Affiche l'extension du fichier
4. Affiche le nom sans extension
5. Affiche le chemin du répertoire parent

---

# Exercice 1 : Solution ✅

```bash
#!/usr/bin/env bash

read -p "Chemin du fichier : " chemin

# Nom du fichier
nom="${chemin##*/}"
echo "Nom : $nom"

# Extension
ext="${nom##*.}"
echo "Extension : $ext"

# Nom sans extension
base="${nom%.*}"
echo "Base : $base"

# Répertoire parent
parent="${chemin%/*}"
echo "Répertoire : $parent"
```

---

# Exercice 2 : Tableau associatif (15 min)

**Consigne :** Créez un script "mini carnet d'adresses" qui :
1. Stocke 3 contacts (nom → email) dans un tableau associatif
2. Demande un nom à l'utilisateur
3. Affiche l'email correspondant ou "Contact inconnu"

---

# Exercice 2 : Solution ✅

```bash
#!/usr/bin/env bash

declare -A contacts
contacts[alice]="alice@example.com"
contacts[bob]="bob@example.com"
contacts[charlie]="charlie@example.com"

read -p "Nom du contact : " nom
nom="${nom,,}"  # Convertir en minuscules

if [[ -v contacts[$nom] ]]; then
  echo "Email : ${contacts[$nom]}"
else
  echo "Contact inconnu : $nom"
  echo "Contacts disponibles :"
  for key in "${!contacts[@]}"; do
    echo "  - $key"
  done
fi
```
