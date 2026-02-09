---

# Exercices Module 6 : Regex 🎯

---

# Exercice : Validation de données (15 min)

**Consigne :** Écrivez un script qui valide :
1. Un email
2. Un numéro de téléphone français (06/07)
3. Un code postal français (5 chiffres)
4. Une date (JJ/MM/AAAA)

---

# Exercice : Solution ✅

```bash
#!/usr/bin/env bash

valider() {
  local label="$1" valeur="$2" regex="$3"
  if [[ "$valeur" =~ $regex ]]; then
    echo "✅ $label valide : $valeur"
  else
    echo "❌ $label invalide : $valeur"
  fi
}

read -p "Email : " email
valider "Email" "$email" \
  '^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'

read -p "Téléphone : " tel
valider "Téléphone" "$tel" \
  '^0[67]([[:space:]]?[0-9]{2}){4}$'

read -p "Code postal : " cp
valider "Code postal" "$cp" '^[0-9]{5}$'

read -p "Date (JJ/MM/AAAA) : " date
valider "Date" "$date" \
  '^[0-3][0-9]/[01][0-9]/[0-9]{4}$'
```
