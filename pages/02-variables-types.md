---
layout: new-section
routeAlias: 'variables-types'
---

<a name="variables-types" id="variables-types"></a>

# 📊 Module 2
## Variables et types de données

### Manipuler les données en Shell

---

# Déclaration de variables 📝

```bash
# PAS d'espace autour du =
nom="Alice"
age=25
chemin="/home/alice"

# Lecture seule
readonly PI=3.14159
declare -r CONSTANTE="immuable"

# Supprimer une variable
unset nom
```

---

# Guillemets : simple vs double 🔤

```bash
nom="monde"

# Double quotes : expansion des variables
echo "Bonjour $nom"    # Bonjour monde

# Simple quotes : pas d'expansion (littéral)
echo 'Bonjour $nom'    # Bonjour $nom

# Backticks/$ : substitution de commande
echo "Date: $(date)"

# Accolades pour délimiter
echo "${nom}_test"      # monde_test
echo "$nom_test"        # Erreur ! cherche $nom_test
```

---

# Manipulation de chaînes ✂️

```bash
str="Hello World Unix Linux"

# Longueur
echo ${#str}           # 22

# Sous-chaîne (offset:longueur)
echo ${str:0:5}        # Hello
echo ${str:6}          # World Unix Linux

# Remplacement
echo ${str/Unix/BSD}   # Hello World BSD Linux
echo ${str//l/L}       # HeLLo WorLd Unix Linux

# Suppression de préfixe/suffixe
fichier="archive.tar.gz"
echo ${fichier%.gz}    # archive.tar
echo ${fichier%%.*}    # archive
echo ${fichier#*.}     # tar.gz
echo ${fichier##*.}    # gz
```

---

# Valeurs par défaut et tests 🔒

```bash
# Valeur par défaut si non définie
echo ${VAR:-"défaut"}

# Assigner la valeur par défaut
echo ${VAR:="défaut"}

# Erreur si non définie
echo ${VAR:?"Variable non définie !"}

# Valeur alternative si définie
echo ${VAR:+"définie"}
```

---

# Tableaux indexés 📋

```bash
# Déclaration
fruits=("pomme" "banane" "cerise" "datte")

# Accès par index (0-based)
echo ${fruits[0]}     # pomme
echo ${fruits[2]}     # cerise

# Tous les éléments
echo ${fruits[@]}     # pomme banane cerise datte

# Nombre d'éléments
echo ${#fruits[@]}    # 4

# Ajouter un élément
fruits+=("figue")

# Supprimer un élément
unset fruits[1]

# Itérer
for fruit in "${fruits[@]}"; do
  echo "- $fruit"
done
```

---

# Tableaux associatifs (dictionnaires) 🗂️

```bash
# Déclaration (bash 4+)
declare -A config

config[host]="localhost"
config[port]="5432"
config[user]="admin"
config[db]="mydb"

# Accès
echo ${config[host]}    # localhost

# Toutes les clés
echo ${!config[@]}      # host port user db

# Toutes les valeurs
echo ${config[@]}

# Itérer
for key in "${!config[@]}"; do
  echo "$key = ${config[$key]}"
done
```

---

# Arithmétique en Shell 🔢

```bash
# Double parenthèses (recommandé)
result=$((5 + 3))
echo $result           # 8

((a = 10))
((a++))
((a += 5))
echo $a                # 16

# let
let "b = 10 * 3"
echo $b                # 30

# expr (ancienne méthode)
c=$(expr 10 + 5)

# Calculs flottants avec bc
echo "scale=2; 10 / 3" | bc    # 3.33
pi=$(echo "scale=10; 4*a(1)" | bc -l)
```

---

# Lecture d'entrée utilisateur 📥

```bash
# Lire une ligne
read -p "Votre nom : " nom
echo "Bonjour $nom"

# Lire avec timeout
read -t 5 -p "Répondez (5s) : " reponse

# Lire un mot de passe (masqué)
read -s -p "Mot de passe : " mdp
echo

# Lire dans un tableau
read -a mots <<< "un deux trois"
echo ${mots[1]}  # deux

# Lire un fichier ligne par ligne
while IFS= read -r ligne; do
  echo ">> $ligne"
done < fichier.txt
```

---

# En résumé 📝

- Pas d'espace autour du `=`
- **Double quotes** pour l'expansion, **simple quotes** pour le littéral
- **${var}** pour la manipulation de chaînes
- **Tableaux indexés** : `array=(...)`, accès `${array[0]}`
- **Tableaux associatifs** : `declare -A`, accès `${array[key]}`
- **$((...))** pour l'arithmétique
- **read** pour la saisie utilisateur
