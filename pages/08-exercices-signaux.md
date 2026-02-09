---

# Exercices Module 8 : Signaux 🎯

---

# Exercice : Daemon simple (15 min)

**Consigne :** Créez un script "daemon" qui :
1. Écrit un PID file au démarrage
2. Capture SIGINT et SIGTERM
3. Effectue un nettoyage propre à la sortie
4. Tourne en boucle en loggant toutes les 5 secondes

---

# Exercice : Solution ✅

```bash
#!/usr/bin/env bash
PIDFILE="/tmp/mydaemon.pid"
LOGFILE="/tmp/mydaemon.log"
RUNNING=true

cleanup() {
  RUNNING=false
  echo "$(date): Arrêt du daemon" >> "$LOGFILE"
  rm -f "$PIDFILE"
  echo "Daemon arrêté"
}

trap cleanup EXIT
trap 'exit 0' INT TERM

# Vérifier s'il tourne déjà
[[ -f "$PIDFILE" ]] && {
  echo "Daemon déjà actif (PID $(cat "$PIDFILE"))"
  exit 1
}

# Écrire le PID
echo $$ > "$PIDFILE"
echo "Daemon démarré (PID $$)"
echo "$(date): Démarrage" >> "$LOGFILE"

while $RUNNING; do
  echo "$(date): heartbeat" >> "$LOGFILE"
  sleep 5
done
```
