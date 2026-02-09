---
layout: new-section
routeAlias: 'scripts-administration'
---

<a name="scripts-administration" id="scripts-administration"></a>

# 🖥️ Module 10
## Scripts d'administration

### Automatiser les tâches d'administration système

---

# Script de backup automatisé 💾

```bash
#!/usr/bin/env bash
set -euo pipefail

BACKUP_DIR="/backup"
SOURCE="/var/www"
DATE=$(date +%Y%m%d_%H%M%S)
ARCHIVE="$BACKUP_DIR/backup_$DATE.tar.gz"
RETENTION=7  # Jours

# Créer le backup
tar czf "$ARCHIVE" -C "$(dirname "$SOURCE")" \
  "$(basename "$SOURCE")"
echo "Backup créé : $ARCHIVE"

# Rotation : supprimer les anciens
find "$BACKUP_DIR" -name "backup_*.tar.gz" \
  -mtime +$RETENTION -delete
echo "Anciens backups supprimés (+${RETENTION}j)"
```

---

# Script de monitoring système 📊

```bash
#!/usr/bin/env bash
set -euo pipefail

SEUIL_CPU=80
SEUIL_MEM=90
SEUIL_DISK=85

check_cpu() {
  local cpu=$(top -bn1 | grep "Cpu(s)" | \
    awk '{print int($2)}')
  [[ $cpu -gt $SEUIL_CPU ]] && \
    echo "⚠️ CPU: ${cpu}% (seuil: ${SEUIL_CPU}%)"
}
```

---

# Monitoring (suite) : RAM, disque

```bash
check_memory() {
  local mem=$(free | \
    awk '/Mem/{printf "%d", $3/$2*100}')
  [[ $mem -gt $SEUIL_MEM ]] && \
    echo "⚠️ RAM: ${mem}% (seuil: ${SEUIL_MEM}%)"
}

check_disk() {
  df -h | awk 'NR>1 && int($5)>'"$SEUIL_DISK"' {
    printf "⚠️ Disque %s: %s\n", $6, $5
  }'
}

echo "=== Monitoring $(date) ==="
check_cpu
check_memory
check_disk
```

---

# Rotation de logs 📋

```bash
#!/usr/bin/env bash
set -euo pipefail

LOGDIR="/var/log/myapp"
MAX_SIZE=10485760  # 10Mo en bytes
KEEP=5             # Nombre de rotations à garder

for logfile in "$LOGDIR"/*.log; do
  [[ -f "$logfile" ]] || continue
  size=$(stat -f%z "$logfile" 2>/dev/null || \
         stat -c%s "$logfile")

  if [[ $size -gt $MAX_SIZE ]]; then
    # Rotation
    for ((i = KEEP; i > 0; i--)); do
      prev=$((i - 1))
      [[ -f "${logfile}.$prev.gz" ]] && \
        mv "${logfile}.$prev.gz" "${logfile}.$i.gz"
    done
    gzip -c "$logfile" > "${logfile}.0.gz"
    : > "$logfile"  # Vider le fichier
    echo "Rotated: $logfile"
  fi
done
```

---

# Cron avancé ⏰

```bash
# Éditer la crontab
crontab -e

# Format : min heure jour mois jour_semaine commande
# Backup quotidien à 2h du matin
0 2 * * * /opt/scripts/backup.sh >> /var/log/backup.log 2>&1

# Monitoring toutes les 5 minutes
*/5 * * * * /opt/scripts/monitoring.sh

# Rotation de logs chaque dimanche à 3h
0 3 * * 0 /opt/scripts/rotate_logs.sh

# Nettoyage mensuel le 1er à minuit
0 0 1 * * /opt/scripts/cleanup.sh

# Avec MAILTO pour recevoir les erreurs
MAILTO=admin@example.com
```

---

# Script de déploiement 🚀

```bash
#!/usr/bin/env bash
set -euo pipefail

APP_DIR="/var/www/myapp"
BRANCH="${1:-main}"

log() { echo "[$(date '+%H:%M:%S')] $*"; }

log "Déploiement branche: $BRANCH"

# Pull du code
cd "$APP_DIR"
git fetch origin
git checkout "$BRANCH"
git pull origin "$BRANCH"
```

---

# Déploiement (suite) : install et restart

```bash
# Installation des dépendances
npm ci --production

# Redémarrage du service
sudo systemctl restart myapp

# Vérification
sleep 3
if systemctl is-active --quiet myapp; then
  log "✅ Déploiement réussi"
else
  log "❌ Échec du déploiement"
  exit 1
fi
```

---

# En résumé 📝

- **Backup** : tar + rotation avec find -delete
- **Monitoring** : vérification CPU, RAM, disque
- **Rotation de logs** : gzip + compteur
- **Cron** : planification des tâches récurrentes
- **Déploiement** : git pull + npm ci + restart service
- Toujours avec `set -euo pipefail` et logging
