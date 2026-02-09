---

# QCM Module 7 : Gestion de fichiers ✅

---

# Question 1

Comment créer un fichier temporaire sécurisé ?

A) `touch /tmp/temp`

B) `mktemp`

C) `echo > /tmp/$$`

D) `tempfile`

---

# Question 2

Que fait `find . -name "*.log" -print0 | xargs -0 rm` ?

A) Affiche les fichiers .log

B) Supprime les fichiers .log en gérant les espaces dans les noms

C) Compresse les fichiers .log

D) Déplace les fichiers .log

---

# Question 3

Comment empêcher l'exécution simultanée d'un script ?

A) `chmod 000`

B) `flock` ou verrouillage par fichier

C) `nice -20`

D) `nohup`

---

# Question 4

Que fait `trap cleanup EXIT` ?

A) Exécute cleanup quand on tape Ctrl+C

B) Exécute cleanup à la sortie du script (quelle que soit la raison)

C) Capture les erreurs

D) Désactive le trap

---

# Question 5

Quel est l'avantage de xargs sur -exec ?

A) Plus sécurisé

B) Plus rapide (batch les appels)

C) Plus lisible

D) Aucun avantage

---

# Réponses du Module 7 📝

**Réponse 1 :** B) `mktemp`
**Réponse 2 :** B) Supprime en gérant les espaces
**Réponse 3 :** B) `flock` ou verrouillage par fichier
**Réponse 4 :** B) Exécute à la sortie du script
**Réponse 5 :** B) Plus rapide (batch)

---

# Score du Module 7 📊

- **5** : Parfait ! ⭐⭐⭐
- **3-4** : Bien ! ⭐⭐
- **1-2** : À revoir ⭐
