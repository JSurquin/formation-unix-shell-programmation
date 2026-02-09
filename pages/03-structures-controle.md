---
layout: new-section
routeAlias: 'structures-controle'
---

<a name="structures-controle" id="structures-controle"></a>

# 🔀 Module 3
## Structures de contrôle

### Conditions, boucles et sélection

---

# if / elif / else 🔀

```bash
#!/usr/bin/env bash

read -p "Entrez un nombre : " n

if [[ $n -gt 100 ]]; then
  echo "Grand nombre"
elif [[ $n -gt 10 ]]; then
  echo "Nombre moyen"
elif [[ $n -gt 0 ]]; then
  echo "Petit nombre"
else
  echo "Nombre négatif ou nul"
fi
```

---

# Opérateurs de test 📊

```bash
# Nombres
[[ $a -eq $b ]]  # Égal
[[ $a -ne $b ]]  # Différent
[[ $a -gt $b ]]  # Plus grand que
[[ $a -lt $b ]]  # Plus petit que
[[ $a -ge $b ]]  # Plus grand ou égal
[[ $a -le $b ]]  # Plus petit ou égal

# Chaînes
[[ "$str" == "hello" ]]   # Égal
[[ "$str" != "hello" ]]   # Différent
[[ -z "$str" ]]           # Vide
[[ -n "$str" ]]           # Non vide

# Logique
[[ $a -gt 0 && $a -lt 100 ]]  # ET
[[ $a -eq 0 || $a -eq 1 ]]    # OU
[[ ! -f "$file" ]]             # NON
```

---

# Tests sur les fichiers 📁

```bash
[[ -f "$file" ]]    # Fichier régulier existe
[[ -d "$dir" ]]     # Répertoire existe
[[ -e "$path" ]]    # Existe (fichier ou répertoire)
[[ -r "$file" ]]    # Lisible
[[ -w "$file" ]]    # Modifiable
[[ -x "$file" ]]    # Exécutable
[[ -s "$file" ]]    # Non vide (taille > 0)
[[ -L "$file" ]]    # Lien symbolique
[[ "$f1" -nt "$f2" ]]  # Plus récent que
[[ "$f1" -ot "$f2" ]]  # Plus ancien que
```

---

# case / esac 🎛️

```bash
#!/usr/bin/env bash

read -p "Action (start|stop|restart) : " action

case "$action" in
  start)
    echo "Démarrage du service..."
    ;;
  stop)
    echo "Arrêt du service..."
    ;;
  restart|reload)
    echo "Redémarrage du service..."
    ;;
  *)
    echo "Usage: $0 {start|stop|restart}"
    exit 1
    ;;
esac
```

---

# Boucle for 🔄

```bash
# Itérer sur une liste
for fruit in pomme banane cerise; do
  echo "Fruit : $fruit"
done

# Itérer sur des fichiers
for file in *.sh; do
  echo "Script : $file"
done

# Boucle C-style
for ((i = 0; i < 10; i++)); do
  echo "Itération $i"
done

# Séquence
for i in {1..10}; do
  echo "Nombre : $i"
done

# Avec pas
for i in {0..100..5}; do
  echo "$i"
done
```

---

# Boucle while et until ⏰

```bash
# while : tant que vrai
count=0
while [[ $count -lt 5 ]]; do
  echo "Count : $count"
  ((count++))
done

# Lire un fichier ligne par ligne
while IFS= read -r ligne; do
  echo ">> $ligne"
done < /etc/passwd

# until : jusqu'à ce que vrai
until [[ $count -ge 10 ]]; do
  echo "Count : $count"
  ((count++))
done

# Boucle infinie
while true; do
  read -p "Commande (quit pour sortir) : " cmd
  [[ "$cmd" == "quit" ]] && break
  echo "Vous avez tapé : $cmd"
done
```

---

# select : menu interactif 📋

```bash
#!/usr/bin/env bash

echo "Choisissez un fruit :"
select fruit in "Pomme" "Banane" "Cerise" "Quitter"; do
  case $fruit in
    "Pomme")   echo "Vous aimez les pommes !" ;;
    "Banane")  echo "Bonne source de potassium !" ;;
    "Cerise")  echo "Excellente en confiture !" ;;
    "Quitter") echo "Au revoir !"; break ;;
    *)         echo "Choix invalide" ;;
  esac
done
```

---

# break et continue ⏭️

```bash
# break : sortir de la boucle
for i in {1..100}; do
  [[ $i -eq 5 ]] && break
  echo $i
done
# Affiche 1 2 3 4

# continue : passer à l'itération suivante
for i in {1..10}; do
  [[ $((i % 2)) -eq 0 ]] && continue
  echo $i
done
# Affiche 1 3 5 7 9
```

---

# En résumé 📝

- **[[ ]]** : tests conditionnels (préférer à `[ ]`)
- **if/elif/else/fi** : conditions
- **case/esac** : sélection multiple
- **for** : itération sur liste ou C-style
- **while/until** : boucles conditionnelles
- **select** : menu interactif
- **break/continue** : contrôle de boucle
