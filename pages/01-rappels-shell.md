---
layout: new-section
routeAlias: 'rappels-shell'
---

<a name="rappels-shell" id="rappels-shell"></a>

# 🔄 Module 1
## Rappels Shell et environnement

### Les fondamentaux du shell Unix/Linux

---

# Les différents shells 🐚

| Shell | Chemin | Particularité |
|-------|--------|---------------|
| **sh** | /bin/sh | Shell POSIX minimal |
| **bash** | /bin/bash | Le plus courant (GNU) |
| **zsh** | /bin/zsh | Défaut macOS, très extensible |
| **dash** | /bin/dash | Rapide, scripts système Debian |
| **fish** | /usr/bin/fish | Moderne, interactif |

```bash
# Quel shell j'utilise ?
echo $SHELL
echo $0

# Lister les shells disponibles
cat /etc/shells
```

---

# Le shebang (#!) 📜

**Première ligne d'un script = indique l'interpréteur.**

```bash
#!/bin/bash
# Script interprété par bash

#!/usr/bin/env bash
# Meilleure portabilité (cherche bash dans le PATH)

#!/bin/sh
# Shell POSIX (plus portable, moins de features)
```

```bash
# Rendre un script exécutable
chmod +x mon_script.sh
./mon_script.sh
```

---

# Variables d'environnement 🌍

```bash
# Voir toutes les variables
env
printenv

# Variables courantes
echo $HOME      # Répertoire personnel
echo $USER      # Nom d'utilisateur
echo $PATH      # Chemins des exécutables
echo $PWD       # Répertoire courant
echo $SHELL     # Shell par défaut
echo $LANG      # Langue
echo $$         # PID du shell courant
echo $?         # Code retour dernière commande
echo $!         # PID du dernier processus en arrière-plan
```

---

# Exporter des variables

```bash
# Variable locale (uniquement dans le shell courant)
MA_VAR="bonjour"

# Variable exportée (accessible aux sous-processus)
export MA_VAR="bonjour"

# Définir et exporter en une ligne
export DB_HOST="localhost"
export DB_PORT=5432

# Supprimer une variable
unset MA_VAR
```

---

# Redirections avancées 📡

```bash
# Stdout (1) vers un fichier
commande > fichier.txt      # Écrase
commande >> fichier.txt     # Ajoute

# Stderr (2) vers un fichier
commande 2> erreurs.log

# Stdout ET Stderr vers le même fichier
commande > output.log 2>&1
commande &> output.log      # Raccourci bash

# Rediriger Stderr vers Stdout
commande 2>&1

# Ignorer une sortie
commande > /dev/null 2>&1
```

---

# Pipes et processus substitution 🔗

```bash
# Pipe classique
ls -la | grep ".txt" | sort | head -5

# Pipe avec tee (affiche ET enregistre)
ls -la | tee listing.txt | grep ".sh"

# Process substitution
diff <(ls dir1) <(ls dir2)

# Pipe nommé (FIFO)
mkfifo mon_pipe
echo "data" > mon_pipe &
cat mon_pipe
```

---

# Sous-shells et groupes de commandes 🔲

```bash
# Sous-shell : entre parenthèses ()
(cd /tmp && ls)
# Le cd n'affecte PAS le shell parent

# Groupe de commandes : entre accolades {}
{ echo "début"; ls; echo "fin"; } > output.txt
# ATTENTION : espace après { et ; avant }

# Command substitution
resultat=$(commande)
fichiers=$(ls -1 | wc -l)
echo "Il y a $fichiers fichiers"

# Ancienne syntaxe (backticks - à éviter)
resultat=`commande`
```

---

# Here documents et here strings 📄

```bash
# Here document (texte multi-lignes)
cat << EOF
Bonjour $USER,
Nous sommes le $(date).
Votre home est $HOME.
EOF

# Here document sans expansion de variables
cat << 'EOF'
Ceci affiche $USER littéralement
Pas d'expansion des variables
EOF

# Here string (une seule ligne)
grep "pattern" <<< "texte à chercher"
```

---

# En résumé 📝

- **bash** est le shell le plus courant
- **#!/usr/bin/env bash** : shebang portable
- Variables d'environnement : `$HOME`, `$PATH`, `$?`
- **export** pour les sous-processus
- Redirections : `>`, `>>`, `2>`, `&>`
- **Pipe** `|` et **tee** pour combiner
- **$()** pour la substitution de commandes
- **Here documents** `<< EOF` pour le multi-lignes
