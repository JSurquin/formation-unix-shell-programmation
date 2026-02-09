---

# Exercices Module 10 : Scripts d'administration 🎯

---

# Exercice : Script de health check (20 min)

**Consigne :** Créez un script de health check qui :
1. Vérifie que des services sont actifs (nginx, postgresql)
2. Vérifie que des ports sont ouverts (80, 443, 5432)
3. Vérifie l'espace disque (seuil 85%)
4. Envoie un résumé par email (ou affiche)
5. Retourne un code d'erreur si un check échoue

---

# Exercice : Solution ✅

```bash
#!/usr/bin/env bash
set -uo pipefail

SERVICES=("nginx" "postgresql")
PORTS=(80 443 5432)
DISK_THRESHOLD=85
ERRORS=0

log() { echo "[$(date '+%H:%M:%S')] $*"; }

# Check services
for svc in "${SERVICES[@]}"; do
  if systemctl is-active --quiet "$svc" 2>/dev/null; then
    log "✅ Service $svc: actif"
  else
    log "❌ Service $svc: inactif"
    ((ERRORS++))
  fi
done
```

---

# Exercice : Solution (suite)

```bash
# Check ports
for port in "${PORTS[@]}"; do
  if ss -tlnp | grep -q ":$port "; then
    log "✅ Port $port: ouvert"
  else
    log "❌ Port $port: fermé"
    ((ERRORS++))
  fi
done

# Check disque
while read -r usage mount; do
  pct=${usage%\%}
  if [[ $pct -gt $DISK_THRESHOLD ]]; then
    log "❌ Disque $mount: ${usage} (seuil ${DISK_THRESHOLD}%)"
    ((ERRORS++))
  fi
done < <(df -h | awk 'NR>1 {print $5, $6}')

# Résultat
echo "---"
if [[ $ERRORS -eq 0 ]]; then
  log "✅ Tous les checks OK"
else
  log "❌ $ERRORS erreur(s) détectée(s)"
fi
exit $ERRORS
```
