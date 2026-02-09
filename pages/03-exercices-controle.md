---

# Exercices Module 3 : Structures de contrôle 🎯

---

# Exercice : Script de gestion de services (20 min)

**Consigne :** Créez un script interactif qui propose un menu pour gérer un service :
1. Démarrer le service
2. Arrêter le service
3. Voir le statut
4. Voir les logs (dernières 20 lignes)
5. Quitter

Utilisez `select` + `case`.

---

# Exercice : Solution (menu + démarrage) ✅

```bash
#!/usr/bin/env bash

SERVICE="nginx"

echo "=== Gestion de $SERVICE ==="
select action in "Démarrer" "Arrêter" "Statut" \
                 "Logs" "Quitter"; do
  case $action in
    "Démarrer")
      echo "Démarrage de $SERVICE..."
      sudo systemctl start "$SERVICE" 2>/dev/null \
        && echo "OK" || echo "Erreur"
      ;;
    "Arrêter")
      echo "Arrêt de $SERVICE..."
      sudo systemctl stop "$SERVICE" 2>/dev/null \
        && echo "OK" || echo "Erreur"
      ;;
```

---

# Exercice : Solution (suite) ✅

```bash
    # suite du case
    "Statut")
      systemctl status "$SERVICE" 2>/dev/null \
        || echo "Service non trouvé"
      ;;
    "Logs")
      journalctl -u "$SERVICE" -n 20 --no-pager \
        2>/dev/null || echo "Pas de logs"
      ;;
    "Quitter")
      echo "Au revoir !"
      break
      ;;
    *)
      echo "Choix invalide"
      ;;
  esac
  echo
done
```
