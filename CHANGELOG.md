# 📄 CHANGELOG - Graylog

Toutes les modifications notables de ce projet seront consignées ici, selon le format [Keep a Changelog](https://keepachangelog.com/fr/1.0.0/) et le [versionnement sémantique](https://semver.org/lang/fr/).

---

## [v1.0.0] - 2025-07-17

### 🚀 Ajout initial

- Installation complète de **Graylog 6.1** sur **Debian 12**
- Intégration de :
  - ✅ MongoDB 6 (via dépôt officiel)
  - ✅ OpenSearch 2.x (fork libre d’Elasticsearch)
  - ✅ OpenJDK 17 (via `apt`)
- Configuration sécurisée et commentée
- Ajout des scripts :
  - `install.sh` : déploiement automatisé
  - `update.sh` : mise à jour des composants
- Création de la documentation dans le dossier `docs/`
- Accès à l’interface Web sur le port `9000`
- Compatibilité testée sur Debian 12 minimal

---

## 📌 À venir (prochaine version)

