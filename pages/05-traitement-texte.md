---
layout: new-section
routeAlias: 'traitement-texte'
---

<a name="traitement-texte" id="traitement-texte"></a>

# 📝 Module 5
## Traitement de texte (sed, awk)

### Les outils puissants de manipulation de texte

---

# sed : Stream Editor 🔄

**sed** = éditeur de flux, modifie le texte à la volée.

```bash
# Substitution (remplacer)
sed 's/ancien/nouveau/' fichier.txt       # 1ère occurrence
sed 's/ancien/nouveau/g' fichier.txt      # Toutes les occurrences
sed -i 's/ancien/nouveau/g' fichier.txt   # Modifier en place

# Supprimer des lignes
sed '5d' fichier.txt          # Supprimer la ligne 5
sed '/pattern/d' fichier.txt  # Supprimer les lignes avec pattern
sed '/^$/d' fichier.txt       # Supprimer les lignes vides

# Afficher des lignes spécifiques
sed -n '5,10p' fichier.txt    # Lignes 5 à 10
sed -n '/START/,/END/p' file  # Entre START et END
```

---

# sed : Exemples avancés

```bash
# Insérer avant/après une ligne
sed '3i\Nouvelle ligne avant 3' fichier.txt
sed '3a\Nouvelle ligne après 3' fichier.txt

# Remplacer une ligne entière
sed '5c\Contenu remplacé' fichier.txt

# Plusieurs commandes
sed -e 's/foo/bar/g' -e 's/baz/qux/g' fichier.txt

# Utiliser un autre délimiteur
sed 's|/usr/local|/opt|g' fichier.txt

# Capturer des groupes
sed 's/\(.*\)@\(.*\)/User: \1, Domain: \2/' emails.txt
```

---

# awk : traitement de données structurées 📊

**awk** = langage de traitement de texte orienté colonnes.

```bash
# Structure : awk 'condition { action }' fichier

# Afficher la 1ère colonne
awk '{print $1}' fichier.txt

# Afficher colonnes 1 et 3
awk '{print $1, $3}' fichier.txt

# Séparateur personnalisé
awk -F':' '{print $1, $3}' /etc/passwd

# Avec condition
awk '$3 > 1000 {print $1, $3}' /etc/passwd
```

---

# awk : Variables intégrées

```bash
# NR = numéro de ligne
awk '{print NR, $0}' fichier.txt

# NF = nombre de champs
awk '{print NF, $NF}' fichier.txt   # Dernier champ

# FS = séparateur de champ
awk 'BEGIN{FS=":"} {print $1}' /etc/passwd

# Blocs BEGIN et END
awk 'BEGIN{print "=== Début ==="} 
     {print $0} 
     END{print "=== Fin ==="}' fichier.txt

# Calculs
awk '{sum += $1} END{print "Total:", sum}' nombres.txt
awk '{sum += $1; n++} END{print "Moyenne:", sum/n}' data.txt
```

---

# Outils complémentaires 🛠️

```bash
# cut : extraire des colonnes
cut -d':' -f1,3 /etc/passwd
cut -c1-10 fichier.txt      # Caractères 1 à 10

# sort : trier
sort fichier.txt              # Alphabétique
sort -n fichier.txt           # Numérique
sort -k2 -t':' fichier.txt   # Par 2ème colonne
sort -r fichier.txt           # Inversé
sort -u fichier.txt           # Unique

# uniq : dédupliquer (après sort !)
sort fichier.txt | uniq
sort fichier.txt | uniq -c    # Compter
sort fichier.txt | uniq -d    # Doublons uniquement

# tr : transformer des caractères
echo "Hello" | tr 'a-z' 'A-Z'     # HELLO
echo "Hello  World" | tr -s ' '    # Hello World
echo "abc123" | tr -d '0-9'        # abc

# paste : fusionner des fichiers côte à côte
paste fichier1.txt fichier2.txt
```

---

# Combiner avec des pipes 🔗

```bash
# Top 5 des processus par mémoire
ps aux | sort -k4 -rn | head -5 | \
  awk '{printf "%-10s %s%%\n", $11, $4}'

# Compter les extensions de fichiers
find . -type f | sed 's/.*\.//' | \
  sort | uniq -c | sort -rn | head -10

# Extraire les IPs des logs Apache
awk '{print $1}' access.log | \
  sort | uniq -c | sort -rn | head -20
```

---

# awk : script complet de rapport 📊

```bash
#!/usr/bin/env bash
# Génère un rapport CSV à partir des logs

awk -F'|' '
BEGIN {
  OFS=","
  print "Date", "Utilisateur", "Action", "Durée(ms)"
}

/^#/ || /^$/ { next }

{
  total_duration += $4
  count++
  users[$2]++
  print $1, $2, $3, $4
}
```

---

# awk : rapport (suite - bloc END)

```bash
END {
  print ""
  print "# Résumé"
  printf "# Total actions: %d\n", count
  printf "# Durée moyenne: %.2f ms\n",
    total_duration/count
  for (u in users)
    printf "# %s: %d actions\n", u, users[u]
}
' logfile.txt
```

Le bloc `BEGIN` initialise, le bloc principal traite chaque ligne, et le bloc `END` produit le résumé.

---

# jq : traitement de JSON en shell 🔧

```bash
# jq est indispensable pour les API REST

# Parser du JSON
curl -s https://api.example.com/users | jq '.'

# Extraire un champ
curl -s https://api.example.com/users | jq '.[].name'

# Filtrer
curl -s https://api.example.com/users | \
  jq '.[] | select(.age > 25)'

# Transformer
curl -s https://api.example.com/users | \
  jq '[.[] | {nom: .name, email: .email}]'

# Créer du JSON
jq -n --arg name "Alice" --arg email "a@b.com" \
  '{name: $name, email: $email}'
```

---

# En résumé 📝

- **sed** : substitution, suppression, insertion de texte
- **awk** : traitement de données en colonnes
- **cut** : extraire des colonnes
- **sort** : trier, **uniq** : dédupliquer
- **tr** : transformer des caractères
- **jq** : traitement de JSON
- La puissance vient de la **combinaison avec des pipes**
