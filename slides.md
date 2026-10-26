---
theme: ./
colorSchema: "auto"
layout: intro
highlighter: shiki
title: Formation Unix/Linux - Programmation Shell 2026
#transition: slide-left
download: "https://shell-programmation.andromed.fr/slides.pdf"
themeConfig:
  logoHeader: "/avatar.png"
  eventLogo: "https://img2.storyblok.com/352x414/f/84560/2388x414/23d8eb4b8d/vue-amsterdam-with-name.png"
  eventUrl: "https://vuejs.amsterdam/"
---

# Unix/Linux - Programmation Shell

🐧 Une formation présentée par Andromed.

💚 08 - 10 Juin 2026

<div class="pt-12">
  <span @click="next" class="px-2 p-3 rounded cursor-pointer hover:bg-white hover:bg-opacity-10 neon-border">
    Appuyez sur espace pour la page suivante <carbon:arrow-right class="inline"/>
  </span>
</div>


<div class="absolute flex gap-x-2 bottom-0 left-0 p-4 z-50">
      <SlideCurrentNo
        class="dark:!text-white !text-[8px] p-1 w-5 h-5 items-center justify-center flex rounded-full bg-white/10 backdrop-blur-sm border border-gray-600 opacity-80"
      />
      <span class="text-gray-400">/</span>
  <SlideTotal
        class="dark:!text-white !text-[8px] p-1 w-5 h-5 items-center justify-center flex rounded-full bg-white/10 backdrop-blur-sm border border-gray-600 opacity-80"
      />
</div>


<div class="absolute bottom-0 right-0 z-50 flex flex-col gap-y-2 p-2">
<div class="hover:bg-white hover:bg-opacity-10 neon-border border-2 rounded-xl w-[200px] p-2 flex flex-col gap-y-2">
  <span class="text-gray-400 text-xs">Programme : <b>2-024</b></span>
  <span class="text-gray-400 text-xs">Lot: <b>2</b></span>
</div>
</div>


---
layout: presenter
eventLogo: 'https://img2.storyblok.com/352x0/f/84560/2388x414/23d8eb4b8d/vue-amsterdam-with-name.png'
eventUrl: 'https://vuejs.amsterdam/'
twitter: '@jimmylansrq'

twitterUrl: 'https://twitter.com/jimmylansrq'
presenterImage: 'https://legacy.andromed.fr/images/fondator.jpg'
---

# Jimmylan Surquin

Fondateur <a  href="https://www.andromed.fr/"><logos-storyblok-icon  mr-1/>Andromed</a>

- Lille, France 🇫🇷
- Création de contenu sur <a href="https://www.youtube.com/channel/jimmylansrq"> <logos-youtube-icon mr-1 /> jimmylansrq </a>
- Blog & Portfolio <a href="https://jimmylan.fr"> jimmylan.fr </a>

---
layout: text-image
media: 'https://i.pinimg.com/originals/f5/5e/80/f55e8059ea945abfd6804b887dd4a0af.gif'
caption: 'PROGRAMMATION SHELL 2026'
---

# DISCLAIMER 🐧

### Dans cette formation nous allons apprendre à programmer en Shell Bash de manière avancée.

---
layout: two-cols
routeAlias: 'sommaire'
---

<a name="sommaire" id="sommaire"></a>

# SOMMAIRE 📜

### Jour 1 : Fondamentaux du Shell

<div class="flex flex-col gap-2">
<Link to="rappels-shell">🔄 1. Rappels Shell et environnement</Link>
<Link to="variables-types">📊 2. Variables et types de données</Link>
<Link to="structures-controle">🔀 3. Structures de contrôle</Link>
<Link to="fonctions-shell">🔧 4. Fonctions Shell</Link>
</div>

### Jour 2 : Programmation avancée

<div class="flex flex-col gap-2">
<Link to="traitement-texte">📝 5. Traitement de texte (sed, awk)</Link>
<Link to="expressions-regulieres">🎯 6. Expressions régulières</Link>
<Link to="gestion-fichiers">📁 7. Gestion avancée des fichiers</Link>
</div>

::right::

### Jour 3 : Scripts professionnels

<div class="flex flex-col gap-2">
<Link to="signaux-traps">🚨 8. Signaux et traps</Link>
<Link to="debug-optimisation">🔍 9. Débogage et optimisation</Link>
<Link to="scripts-administration">🖥️ 10. Scripts d'administration</Link>
<Link to="projet-final-shell">🎯 11. Projet final</Link>
<Link to="qcm-final">✅ QCM de validation finale</Link>
</div>

<br>

**Note :** Chaque module contient :
- 📖 Cours théorique
- ✅ QCM de validation
- 🎯 Exercices pratiques

---
layout: two-cols
---

### PROGRAMME JOUR 1 📅

<small>

**Module 1 - Rappels Shell**
- Les différents shells (bash, zsh, sh)
- Variables d'environnement
- Redirections et pipes avancés
- Sous-shells et groupes de commandes

**Module 2 - Variables et types**
- Variables locales et globales
- Tableaux (indexés et associatifs)
- Arithmétique en shell
- Chaînes de caractères (manipulation)

</small>

::right::

<small>

**Module 3 - Structures de contrôle**
- if/elif/else avancé
- case/esac
- Boucles for, while, until
- select pour les menus interactifs

**Module 4 - Fonctions Shell**
- Déclaration et appel
- Paramètres et valeurs de retour
- Variables locales (local)
- Fonctions récursives

</small>

---
layout: two-cols
---

### PROGRAMME JOUR 2 📅

<small>

**Module 5 - Traitement de texte**
- sed : substitution et édition en flux
- awk : traitement de données structurées
- cut, sort, uniq, tr, paste
- Combiner les outils avec pipes

**Module 6 - Expressions régulières**
- Regex de base (BRE)
- Regex étendues (ERE)
- grep, egrep, sed avec regex
- Cas d'usage pratiques

</small>

::right::

<small>

**Module 7 - Gestion avancée des fichiers**
- find avec -exec et xargs
- Descripteurs de fichiers
- Fichiers temporaires sécurisés
- Verrouillage de fichiers (flock)

</small>

---
layout: two-cols
---

### PROGRAMME JOUR 3 📅

<small>

**Module 8 - Signaux et traps**
- Les signaux Unix (SIGINT, SIGTERM, etc.)
- trap pour capturer les signaux
- Nettoyage à la sortie
- Scripts interruptibles proprement

**Module 9 - Débogage et optimisation**
- set -e, set -u, set -o pipefail
- Bash strict mode
- shellcheck (linter)
- Profilage et optimisation

</small>

::right::

<small>

**Module 10 - Scripts d'administration**
- Backup automatisé
- Monitoring système
- Rotation de logs
- Déploiement automatisé
- Cron avancé

**Module 11 - Projet final**
- Script de gestion de serveur complet
- Menu interactif
- Logging, gestion d'erreurs
- Documentation

**QCM Final** ✅

</small>

---
src: './pages/01-rappels-shell.md'
---

---
src: './pages/01-qcm-rappels.md'
---

---
src: './pages/02-variables-types.md'
---

---
src: './pages/02-qcm-variables.md'
---

---
src: './pages/02-exercices-variables.md'
---

---
src: './pages/03-structures-controle.md'
---

---
src: './pages/03-qcm-controle.md'
---

---
src: './pages/03-exercices-controle.md'
---

---
src: './pages/04-fonctions-shell.md'
---

---
src: './pages/04-qcm-fonctions.md'
---

---
src: './pages/04-exercices-fonctions.md'
---

---
src: './pages/05-traitement-texte.md'
---

---
src: './pages/05-qcm-texte.md'
---

---
src: './pages/05-exercices-texte.md'
---

---
src: './pages/06-expressions-regulieres.md'
---

---
src: './pages/06-qcm-regex.md'
---

---
src: './pages/06-exercices-regex.md'
---

---
src: './pages/07-gestion-fichiers.md'
---

---
src: './pages/07-qcm-fichiers.md'
---

---
src: './pages/07-exercices-fichiers.md'
---

---
src: './pages/08-signaux-traps.md'
---

---
src: './pages/08-qcm-signaux.md'
---

---
src: './pages/08-exercices-signaux.md'
---

---
src: './pages/09-debug-optimisation.md'
---

---
src: './pages/09-qcm-debug.md'
---

---
src: './pages/09-exercices-debug.md'
---

---
src: './pages/10-scripts-administration.md'
---

---
src: './pages/10-qcm-admin.md'
---

---
src: './pages/10-exercices-admin.md'
---

---
src: './pages/11-projet-final.md'
---

---
src: './pages/12-qcm-final.md'
---
