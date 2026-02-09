---
layout: new-section
routeAlias: 'expressions-regulieres'
---

<a name="expressions-regulieres" id="expressions-regulieres"></a>

# 🎯 Module 6
## Expressions régulières

### Maîtriser les regex pour le traitement de texte

---

# Qu'est-ce qu'une regex ? 🎯

**Expression régulière** = motif (pattern) de recherche dans du texte.

**Métacaractères de base :**

| Caractère | Signification |
|-----------|--------------|
| `.` | N'importe quel caractère |
| `*` | 0 ou plusieurs fois |
| `+` | 1 ou plusieurs fois (ERE) |
| `?` | 0 ou 1 fois (ERE) |
| `^` | Début de ligne |
| `$` | Fin de ligne |
| `[]` | Classe de caractères |
| `\` | Échappement |

---

# Classes de caractères 📋

```bash
[abc]      # a, b ou c
[a-z]      # Lettre minuscule
[A-Z]      # Lettre majuscule
[0-9]      # Chiffre
[a-zA-Z]   # Lettre (min ou maj)
[^0-9]     # PAS un chiffre

# Classes POSIX
[[:alpha:]]  # Lettre
[[:digit:]]  # Chiffre
[[:alnum:]]  # Lettre ou chiffre
[[:space:]]  # Espace, tab, newline
[[:upper:]]  # Majuscule
[[:lower:]]  # Minuscule
```

---

# grep avec regex 🔍

```bash
# Recherche simple
grep "error" log.txt
grep -i "error" log.txt      # Insensible à la casse
grep -n "error" log.txt      # Avec numéro de ligne
grep -c "error" log.txt      # Compter les occurrences
grep -v "debug" log.txt      # Inverser (exclure)
grep -r "TODO" ./src/        # Récursif

# Regex étendues (ERE)
grep -E "error|warning" log.txt
grep -E "^[0-9]{4}-[0-9]{2}" log.txt  # Date YYYY-MM

# Regex PCRE (Perl)
grep -P "\d{3}\.\d{3}\.\d{3}\.\d{3}" log.txt
```

---

# Quantificateurs et groupes 📊

```bash
# Quantificateurs (ERE)
a*       # 0+ fois "a"
a+       # 1+ fois "a"
a?       # 0 ou 1 fois "a"
a{3}     # Exactement 3 "a"
a{2,5}   # Entre 2 et 5 "a"
a{3,}    # 3 ou plus "a"

# Groupes
(abc)+           # "abc" 1+ fois
(cat|dog)        # "cat" ou "dog"
(http|https)://  # URL http ou https

# Références arrière
\1, \2    # Référence au groupe capturé
```

---

# Exemples pratiques 💡

```bash
# Valider une adresse email
grep -E '^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'

# Trouver des adresses IP
grep -E '\b([0-9]{1,3}\.){3}[0-9]{1,3}\b'

# Trouver des numéros de téléphone français
grep -E '0[1-9](\s?[0-9]{2}){4}'

# Trouver des dates format JJ/MM/AAAA
grep -E '[0-3][0-9]/[01][0-9]/[0-9]{4}'

# Trouver des lignes vides
grep -E '^$'
grep -E '^\s*$'   # Vides ou espaces uniquement
```

---

# Regex dans bash [[ =~ ]] 🔧

```bash
#!/usr/bin/env bash

email="user@example.com"
regex='^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'

if [[ "$email" =~ $regex ]]; then
  echo "Email valide"
  echo "User: ${BASH_REMATCH[0]}"
else
  echo "Email invalide"
fi

# Validation d'IP
ip="192.168.1.1"
if [[ "$ip" =~ ^[0-9]+\.[0-9]+\.[0-9]+\.[0-9]+$ ]]; then
  echo "Format IP valide"
fi
```

---

# En résumé 📝

- `.` = n'importe quel caractère
- `*`, `+`, `?` = quantificateurs
- `^`, `$` = ancres (début/fin de ligne)
- `[...]` = classes de caractères
- `grep -E` pour les regex étendues (ERE)
- `[[ =~ ]]` pour tester en bash
- `${BASH_REMATCH}` pour capturer les groupes
