---
layout: new-section
routeAlias: 'qcm-final'
---

<a name="qcm-final" id="qcm-final"></a>

# ✅ QCM Final
## Validation des acquis - Programmation Shell

---

# Question 1

Quel shebang assure la meilleure portabilité ?

A) `#!/bin/bash`

B) `#!/usr/bin/env bash`

C) `#!/bin/sh`

D) `#!bash`

---

# Question 2

Que fait `set -euo pipefail` ?

A) Active le mode debug

B) Arrête sur erreur, variable non définie, et erreur dans les pipes

C) Exporte les variables

D) Active le mode verbeux

---

# Question 3

Comment accéder au dernier élément d'un tableau ?

A) `${array[-1]}`

B) `${array[last]}`

C) `${array[end]}`

D) `$array[-1]`

---

# Question 4

Que fait `sed -i 's/old/new/g' file` ?

A) Affiche le résultat

B) Modifie le fichier en place

C) Crée un nouveau fichier

D) Supprime les lignes

---

# Question 5

Comment déclarer une variable locale dans une fonction ?

A) `var="value"`

B) `local var="value"`

C) `private var="value"`

D) `let var="value"`

---

# Question 6

Quel outil analyse les colonnes dans un fichier ?

A) sed

B) awk

C) grep

D) tr

---

# Question 7

Que matche `^[0-9]+$` ?

A) Une ligne contenant au moins un chiffre

B) Une ligne composée uniquement de chiffres

C) Le début d'un nombre

D) N'importe quel texte

---

# Question 8

Comment créer un fichier temporaire sécurisé ?

A) `touch /tmp/temp$$`

B) `mktemp`

C) `echo > /tmp/temp`

D) `tempfile`

---

# Question 9

Quel signal est envoyé par `kill` sans option ?

A) SIGKILL (9)

B) SIGTERM (15)

C) SIGINT (2)

D) SIGHUP (1)

---

# Question 10

Quel outil lint les scripts bash ?

A) eslint

B) shellcheck

C) pylint

D) bashfmt

---

# Question 11

Que retourne `$?` ?

A) Le PID du processus

B) Le code retour de la dernière commande

C) Le nombre d'arguments

D) Le nom du script

---

# Question 12

Comment itérer sur les fichiers d'un répertoire ?

A) `for f in $(ls dir)`

B) `for f in dir/*`

C) `foreach f in dir`

D) `list dir | for f`

---

# Question 13

Que fait `trap cleanup EXIT` ?

A) Exécute cleanup uniquement sur Ctrl+C

B) Exécute cleanup à chaque sortie du script

C) Empêche la sortie

D) Supprime cleanup

---

# Question 14

Comment lire un fichier ligne par ligne ?

A) `for line in file`

B) `while IFS= read -r line; do ... done < file`

C) `cat file | for line`

D) `readline file`

---

# Question 15

Que fait `${var:-default}` ?

A) Assigne default à var

B) Retourne default si var est non définie, sans modifier var

C) Supprime var

D) Compare var à default

---

# Réponses QCM Final 📝

| Question | Réponse |
|----------|---------|
| 1 | B) `#!/usr/bin/env bash` |
| 2 | B) Arrête sur erreur, var non définie, pipe |
| 3 | A) `${array[-1]}` |
| 4 | B) Modifie en place |
| 5 | B) `local var="value"` |
| 6 | B) awk |
| 7 | B) Ligne uniquement de chiffres |
| 8 | B) mktemp |

---

# Réponses QCM Final (suite) 📝

| Question | Réponse |
|----------|---------|
| 9 | B) SIGTERM (15) |
| 10 | B) shellcheck |
| 11 | B) Code retour dernière commande |
| 12 | B) `for f in dir/*` |
| 13 | B) Exécute à chaque sortie |
| 14 | B) `while IFS= read -r line` |
| 15 | B) Retourne default sans modifier var |

---

# Score Final 📊

Comptez vos bonnes réponses sur 15 :

- **14-15** : Expert Shell ! 🏆
- **11-13** : Très bien ! ⭐⭐⭐
- **8-10** : Bien ! ⭐⭐
- **5-7** : À revoir ⭐
- **< 5** : Revoir les modules

---

# Merci ! 🎉

**Formation Unix/Linux - Programmation Shell**

Ressources pour aller plus loin :
- Bash Manual : https://www.gnu.org/software/bash/manual/
- ShellCheck : https://www.shellcheck.net/
- Advanced Bash Guide : https://tldp.org/LDP/abs/html/
- Explainshell : https://explainshell.com/
