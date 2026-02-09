---

# Exercices Module 5 : Traitement de texte 🎯

---

# Exercice : Analyse de logs (20 min)

**Consigne :** Avec un fichier de logs Apache simulé, écrivez des commandes pour :
1. Extraire les 10 IPs les plus fréquentes
2. Compter les requêtes par code HTTP (200, 404, 500)
3. Extraire les URLs qui ont retourné un 404
4. Calculer le total de bytes transférés

---

# Exercice : Solution ✅

```bash
# Fichier log format : IP - - [date] "METHOD URL" CODE SIZE

# 1. Top 10 IPs
awk '{print $1}' access.log | \
  sort | uniq -c | sort -rn | head -10

# 2. Requêtes par code HTTP
awk '{print $9}' access.log | \
  sort | uniq -c | sort -rn

# 3. URLs avec 404
awk '$9 == 404 {print $7}' access.log | \
  sort | uniq -c | sort -rn

# 4. Total bytes transférés
awk '{sum += $10} END{
  printf "Total: %.2f MB\n", sum/1024/1024
}' access.log
```
