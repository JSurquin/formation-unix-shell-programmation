---
layout: new-section
routeAlias: 'projet-final-shell'
---

<a name="projet-final-shell" id="projet-final-shell"></a>

# 🎯 Module 11
## Projet final : Server Manager

### Script complet de gestion de serveur

---

# Le projet 📋

**Créez un outil en ligne de commande `srvmgr.sh`** qui offre :
- Menu interactif de gestion de serveur
- Mode commande (arguments CLI)
- Backup automatisé
- Monitoring système
- Gestion des services
- Logging structuré

**Durée : 1h30**

---

# Contraintes techniques ⚙️

1. **Bash strict mode** : `set -euo pipefail`
2. **Bibliothèque** de fonctions dans `lib/`
3. **Trap** pour le nettoyage
4. **Arguments CLI** avec getopts
5. **Logging** dans un fichier avec rotation
6. **Shellcheck** : 0 warning
7. **Documentation** : `--help` fonctionnel

---

# Architecture suggérée

```
srvmgr/
├── srvmgr.sh           # Script principal
├── lib/
│   ├── utils.sh         # Fonctions utilitaires
│   ├── backup.sh        # Module de backup
│   ├── monitor.sh       # Module de monitoring
│   └── services.sh      # Module de gestion de services
├── config/
│   └── srvmgr.conf      # Configuration
└── logs/
    └── srvmgr.log       # Fichier de log
```

---

# Exemple d'utilisation attendue

```bash
# Mode interactif (menu)
./srvmgr.sh

# Mode commande
./srvmgr.sh --backup /var/www
./srvmgr.sh --monitor
./srvmgr.sh --service nginx status
./srvmgr.sh --help

# Options
./srvmgr.sh -v --backup /var/www  # Verbose
./srvmgr.sh -c /etc/srvmgr.conf  # Config custom
```

---

# Critères d'évaluation 📊

| Critère | Points |
|---------|--------|
| Bash strict mode + shellcheck | /15 |
| Architecture modulaire (lib/) | /15 |
| Gestion des erreurs (trap, codes retour) | /15 |
| Arguments CLI (getopts) | /10 |
| Menu interactif (select) | /10 |
| Fonctionnalités (backup, monitor, services) | /20 |
| Logging structuré | /10 |
| Documentation (--help) | /5 |
| **Total** | **/100** |

---

# Bravo ! 🎉

Vous avez terminé la formation Programmation Shell !

**Vous maîtrisez maintenant :**
- Variables, tableaux, arithmétique
- Structures de contrôle avancées
- Fonctions et bibliothèques
- sed, awk et expressions régulières
- Gestion de fichiers et signaux
- Débogage avec shellcheck et strict mode
- Scripts d'administration professionnels
