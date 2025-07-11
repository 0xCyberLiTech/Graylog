<!-- MASTER-HEADER-START -->
<div align="center">

<a href="https://0xcyberlitech.com/">
  <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/headers/header-graylog.svg" alt="ATELIER GRAYLOG // CENTRALISATION SIEM" width="100%" />
</a>

<p align="center">
  <a href="https://0xcyberlitech.com/"><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-portal.svg" alt="Portail 0xCyberLiTech.com" width="24%" /></a>
  <a href="https://0xcyberlitech.com/soc-rd.html"><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-soc-rd.svg" alt="Livre Blanc SOC Cockpit" width="24%" /></a>
  <a href="https://0xcyberlitech.com/jarvis-rd.html"><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-jarvis-rd.svg" alt="Livre Blanc JARVIS IA" width="24%" /></a>
  <a href="https://github.com/0xCyberLiTech?tab=repositories"><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-github.svg" alt="Catalogue des 23 Dépôts" width="24%" /></a>
</p>
<p align="center">
  <a href="README.md"><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-back-readme.svg" alt="Retour au sommaire du dépôt" width="340" /></a>
</p>

<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/divider-hud.svg" alt="" width="100%" />
</div>
<!-- MASTER-HEADER-END -->

<!-- DEBIAN-TRUTH-START -->
> [!IMPORTANT]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-shield.svg" width="18" height="18" align="absmiddle" alt="" /> ** Matrice Officielle Debian — `Debian 12 (Bookworm)` · `Debian 13 (Trixie)` · `Debian 14 (Forky)`**
> - **Sources Officielles Debian.org (`opensearch`) :** `Bookworm (12)` : **`Stable-12`** &nbsp;·&nbsp; `Trixie (13 — Stable)` : **`Stable-13`** &nbsp;·&nbsp; `Forky (14 — Next-Gen)` : **`2.4.1+dfsg-2`**
> - **Références Officielles :** [Paquet Debian Trixie (`default-jre-headless`)](https://packages.debian.org/trixie/default-jre-headless) &nbsp;·&nbsp; [Paquet Debian Forky (`default-jre-headless`)](https://packages.debian.org/forky/default-jre-headless) &nbsp;·&nbsp; [Documentation Officielle Debian](https://www.debian.org/releases/trixie/)
> - **Note d'Ingénierie (Divergence 13 vs 14) :** Sous Debian 13 (Trixie) et Debian 14 (Forky), `/etc/sysctl.conf` monolithique est déprécié au profit de fichiers modulaires dans **`/etc/sysctl.d/99-*.conf`** chargés par `sysctl --system`.

<details>
<summary><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> <b>Afficher les Encarts Ligne de Commande : Debian 13 (Trixie — Stable) vs Debian 14 (Forky — Next-Gen)</b></summary>

#### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-ok.svg" width="42" height="16" align="absmiddle" alt="[OK]" /> Profil Production Stable — Commandes pour `Debian 13 (Trixie)`
```bash
# Debian 13 (Trixie) — Depot GPG en /etc/apt/keyrings/ & suivi systemd :
sudo install -m 0755 -d /etc/apt/keyrings
sudo systemctl status graylog-server && sudo journalctl -u graylog-server -n 50
```

#### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-rd.svg" width="46" height="16" align="absmiddle" alt="[R&D]" /> Profil Anticipation Next-Gen — Commandes pour `Debian 14 (Forky)`
```bash
# Debian 14 (Forky) — Format DEB822 (/etc/apt/sources.list.d/graylog.sources) & vm.max_map_count :
echo 'vm.max_map_count=262144' | sudo tee /etc/sysctl.d/99-opensearch.conf && sudo sysctl --system
```

</details>
<!-- DEBIAN-TRUTH-END -->

<!-- CIEL-PEDAGOGY-START -->
<details>
<summary><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-puzzle.svg" width="18" height="18" align="absmiddle" alt="" /> <b>Synthèse d'Architecture, Standards Officiels &amp; Diagnostic (Niveau 1 : Fondamentaux · Niveau 2 : Repères · Niveau 3 : Diagnostic)</b></summary>

- **Niveau 1 — Fondamentaux &amp; Principe d'Architecture :** **Graylog** est une plateforme centralisée de gestion et d'analyse de journaux (**SIEM / Log Management**) articulée autour de trois composants : **MongoDB** (configuration et métadonnées), **OpenSearch** (indexation et recherche temps réel) et **Graylog Server** (ingestion Syslog/GELF, normalisation et alertes).
- **Niveau 2 — Repères Officiels (Ports IANA, Fichiers Debian &amp; Commandes de Validation) :** **Ports standards :** `TCP 9000` (Web UI & API REST Graylog) · `UDP/TCP 5140` ou `1514` (Inputs Syslog/GELF) · `TCP 9200` (OpenSearch local) · `TCP 27017` (MongoDB local) &nbsp;|&nbsp; **Fichier clé :** `/etc/graylog/server/server.conf`.
- **Niveau 3 — Diagnostic d'Incidents &amp; Ingénierie Avancée :** **Diagnostic & Architecture :** Le démarrage de `graylog-server` requiert que `mongod.service` et `opensearch.service` soient actifs et que les paramètres `password_secret` et `root_password_sha2` soient définis. La déportation temps réel des journaux vers un puits isolé est une exigence fondamentale (ANSSI) pour préserver les preuves d'audit en cas de compromission d'un serveur.
- **Sources de Vérité Officielles Éditeurs &amp; Standards :** [Documentation Officielle Graylog](https://go2docs.graylog.org/) &nbsp;·&nbsp; [Documentation Officielle OpenSearch](https://opensearch.org/docs/latest/) &nbsp;·&nbsp; [Recommandations ANSSI Journalisation](https://cyber.gouv.fr/)

</details>
<!-- CIEL-PEDAGOGY-END -->


<div align="center">

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 01 // Installer Graylog 6.1 sur Debian 12 (Bookworm), Debian 13 (Trixie) & Debian 14 (Forky)
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

</div>

<div align="center" style="margin-bottom: 10px;">

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> **Sommaire**

<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-ok.svg" width="42" height="16" align="absmiddle" alt="[OK]" /> **Actif** – Dépôt totalement accessible 
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-rd.svg" width="46" height="16" align="absmiddle" alt="[R&D]" /> **Partiel** – Dépôt partiellement accessible 
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-ko.svg" width="42" height="16" align="absmiddle" alt="[NON]" /> **Inactif** – Dépôt inaccessible ou indisponible

</div>

---

<div align="center">

| Section | Description | Accès Direct |
|:---:|:---|:---:|
| **1.** | Présentation | [<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-explore.svg" alt="Accéder" />](#i-présentation) |
| **2.** | Prérequis | [<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-explore.svg" alt="Accéder" />](#ii-prérequis) |
| **3.** | Installation pas à pas de Graylog | [<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-explore.svg" alt="Accéder" />](#iii-installation-pas-à-pas-de-graylog) |
| **3.A** | ↳ Installation de MongoDB | [<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-explore.svg" alt="Accéder" />](#a-installation-de-mongodb) |
| **3.B** | ↳ Installation d'OpenSearch | [<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-explore.svg" alt="Accéder" />](#b-installation-dopensearch) |
| **3.C** | ↳ Configuration de Java (JVM) | [<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-explore.svg" alt="Accéder" />](#c-configuration-de-java-jvm) |
| **3.D** | ↳ Installation de Graylog | [<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-explore.svg" alt="Accéder" />](#d-installation-de-graylog) |
| **3.E** | ↳ Création d’un compte administrateur | [<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-explore.svg" alt="Accéder" />](#e-création-dun-compte-administrateur) |
| **4.** | Conclusion | [<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-explore.svg" alt="Accéder" />](#iv-conclusion) |

</div>


---

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> I. Présentation.

#### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> Qu'est-ce que Graylog ?

**Graylog** est une plateforme open source de **gestion centralisée des journaux** (logs) permettant la **collecte**, **l’analyse**, **la recherche** et **la visualisation** en temps réel de données issues de différents systèmes, serveurs, applications ou équipements réseau.

Il est particulièrement utilisé en **cybersécurité**, en **monitoring**, et pour la **traçabilité** des événements systèmes.

---

#### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-puzzle.svg" width="18" height="18" align="absmiddle" alt="" /> Fonctionnalités clés.

- <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> **Collecte de logs** multi-sources : syslog, fichiers journaux, flux réseau, etc.
- <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> **Moteur de recherche puissant** basé sur **Elasticsearch**.
- <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> **Dashboards interactifs** : création de graphiques et widgets personnalisés.
- <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> **Archivage et rotation automatique** des logs.
- <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-shield.svg" width="18" height="18" align="absmiddle" alt="" /> **Détection d'incidents** et d'anomalies.
- <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-puzzle.svg" width="18" height="18" align="absmiddle" alt="" /> Extensible avec des **plugins** et des **pipelines de traitement**.

---

#### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> Architecture.

Graylog repose sur :
- **MongoDB** (base de données de configuration),
- **Elasticsearch** ou **OpenSearch** (moteur d’indexation et de recherche),
- **Graylog Server** (cœur applicatif),
- **Graylog Web Interface** (interface graphique de consultation).

---

#### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> Cas d’usages typiques.

- <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-shield.svg" width="18" height="18" align="absmiddle" alt="" /> Surveillance de la sécurité (SIEM léger),
- <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> Supervision des serveurs (logs Apache/Nginx, SSH, etc.),
- <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-network.svg" width="18" height="18" align="absmiddle" alt="" /> Analyse des événements réseau,
- <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-puzzle.svg" width="18" height="18" align="absmiddle" alt="" /> Suivi des conteneurs Docker, Kubernetes,
- <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-crypto.svg" width="18" height="18" align="absmiddle" alt="" /> Détection d'intrusion ou analyse forensic.

---

#### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-ok.svg" width="42" height="16" align="absmiddle" alt="[OK]" /> Avantages.

- Interface web moderne et intuitive,
- Filtrage avancé avec requêtes personnalisées,
- Très bonne performance même avec un grand volume de logs,
- Open source avec une **édition communautaire gratuite**,
- Évolutif en version **Entreprise ou Cloud** pour les environnements critiques.

---

#### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> Pourquoi utiliser Graylog ?

Graylog simplifie la gestion des logs dans un environnement distribué, en rendant possible l’**agrégation et l’analyse rapide** de millions d’événements. C’est une solution efficace pour :

- Répondre aux exigences de conformité (RGPD, PCI-DSS…),
- Identifier rapidement les anomalies et incidents,
- Faciliter le diagnostic et le dépannage système.

---

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> II. Prérequis.

Avant de procéder à l’installation de Graylog, assurez-vous que les prérequis suivants sont respectés.

#### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-puzzle.svg" width="18" height="18" align="absmiddle" alt="" /> Composants requis

- **MongoDB 7.0 / 8.0** (support natif OpenSSL 3.x sous Debian 12, 13 & 14 — zéro dépendance obsolète `libssl1.1`)  
- **OpenSearch 2.x** (fork open source d’Elasticsearch — versions supportées : **2.12 à 2.18+**)  
- **OpenJDK 17 / 21** (fourni directement en bundlé avec `graylog-server` et `opensearch`)

#### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-puzzle.svg" width="18" height="18" align="absmiddle" alt="" /> Configuration système recommandée

- **Système d’exploitation** : **Debian 12 (Bookworm)**, **Debian 13 (Trixie — Stable)** ou **Debian 14 (Forky — Next-Gen)**  
- **Mémoire vive (RAM)** : 8 Go minimum (16 Go recommandés en production)  
- **Espace disque** : 256 Go NVMe minimum

> **Remarque** : Ces spécifications sont fournies à titre indicatif. Le dimensionnement dépend du volume de logs à traiter. Graylog peut gérer aussi bien quelques mégaoctets que plusieurs téraoctets de données par jour.

#### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-puzzle.svg" width="18" height="18" align="absmiddle" alt="" /> Préparation de la machine

Avant de commencer l’installation :

- Attribuez une **adresse IP statique** à la machine ;
- Installez les **dernières mises à jour** du système ;
- Vérifiez que le **fuseau horaire** est correctement configuré ;
- Définissez un **serveur NTP** pour la synchronisation de l’heure.

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo timedatectl set-timezone Europe/Paris
> ```
<!-- CODE-WINDOW-END -->

#### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-puzzle.svg" width="18" height="18" align="absmiddle" alt="" /> Mise à jour du système

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo apt update && sudo apt upgrade -y
> ```
<!-- CODE-WINDOW-END -->

---

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> III. Installation pas à pas de Graylog

Mise à jour du cache des paquets et installation de paquets supplémentaires pour la suite :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo apt-get update
> ```
<!-- CODE-WINDOW-END -->

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo apt-get install curl lsb-release ca-certificates gnupg2 pwgen
> ```
<!-- CODE-WINDOW-END -->

<a id="a-installation-de-mongodb"></a>
##### A. Installation de MongoDB 7.0 (Support natif OpenSSL 3 sous Debian 12, 13 & 14)

Importez la clé GPG officielle de MongoDB 7.0 dans `/usr/share/keyrings/` :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> curl -fsSL https://www.mongodb.org/static/pgp/server-7.0.asc | sudo gpg -o /usr/share/keyrings/mongodb-server-7.0.gpg --dearmor
> ```
<!-- CODE-WINDOW-END -->

Ajoutez le dépôt officiel MongoDB 7.0 (`bookworm` est pleinement compatible avec OpenSSL 3.x sous Debian 12 Bookworm, Debian 13 Trixie et Debian 14 Forky sans nécessiter l'ancienne bibliothèque `libssl1.1`) :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> echo "deb [ signed-by=/usr/share/keyrings/mongodb-server-7.0.gpg ] http://repo.mongodb.org/apt/debian bookworm/mongodb-org/7.0 main" | sudo tee /etc/apt/sources.list.d/mongodb-org-7.0.list
> ```
<!-- CODE-WINDOW-END -->

Mettez à jour le cache des paquets et installez `mongodb-org` :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo apt-get update && sudo apt-get install -y mongodb-org
> ```
<!-- CODE-WINDOW-END -->

Ensuite, rechargez systemd, activez et démarrez le service `mongod.service` :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo systemctl daemon-reload
> ```
<!-- CODE-WINDOW-END -->

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo systemctl enable mongod.service
> ```
<!-- CODE-WINDOW-END -->

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo systemctl restart mongod.service
> ```
<!-- CODE-WINDOW-END -->

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo systemctl --type=service --state=active | grep mongod
> ```
<!-- CODE-WINDOW-END -->

MongoDB est installé, vous pouvez passer à l'installation du prochain composant.


##### B. Installation d'OpenSearch.

A présent vous allez passer à l'installation d'OpenSearch. La commande suivante permet d’ajouter la clé de signature pour les paquets OpenSearch :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> curl -o- https://artifacts.opensearch.org/publickeys/opensearch.pgp | sudo gpg --dearmor --batch --yes -o /usr/share/keyrings/opensearch-keyring
> ```
<!-- CODE-WINDOW-END -->

Puis, ajoutez le dépôt OpenSearch pour que nous puissions télécharger le paquet avec apt par la suite :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> echo "deb [signed-by=/usr/share/keyrings/opensearch-keyring] https://artifacts.opensearch.org/releases/bundle/opensearch/2.x/apt stable main" | sudo tee /etc/apt/sources.list.d/opensearch-2.x.list
> ```
<!-- CODE-WINDOW-END -->

Mettez à jour votre cache de paquets :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo apt-get update
> ```
<!-- CODE-WINDOW-END -->

Procédez ensuite à l’installation d’OpenSearch, en veillant à définir un mot de passe sécurisé pour le compte administrateur de l’instance.
Dans cet exemple, le mot de passe utilisé est : MonMotDePasse, mais il est fortement recommandé de choisir votre propre mot de passe robuste.

<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-alert.svg" width="18" height="18" align="absmiddle" alt="" /> Évitez les mots de passe faibles comme P@ssword, car cela entraînera une erreur à la fin de l’installation. Depuis la version 2.12 d’OpenSearch, l’installation impose un mot de passe répondant aux critères suivants :

Minimum 8 caractères :

Contient au moins :

- Une lettre minuscule
- Une lettre majuscule
- Un chiffre
- Un caractère spécial

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo env OPENSEARCH_INITIAL_ADMIN_PASSWORD=CLT-Connect2025# apt-get install opensearch
> ```
<!-- CODE-WINDOW-END -->

Patientez pendant l'installation...

Quand c'est terminé, prenez le temps d'effectuer la configuration minimale. Ouvrez le fichier de configuration au format YAML :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo nano /etc/opensearch/opensearch.yml
> ```
<!-- CODE-WINDOW-END -->

Configurez les options suivantes :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> cluster.name: graylog
> node.name: ${HOSTNAME}
> path.data: /var/lib/opensearch
> path.logs: /var/log/opensearch
> discovery.type: single-node
> network.host: 10.200.200.101
> action.auto_create_index: false
> plugins.security.disabled: true
> ```
<!-- CODE-WINDOW-END -->

Cette configuration OpenSearch est destinée à configurer un nœud unique. 

##### Paramètres de configuration d’OpenSearch pour Graylog

###### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> Explication des paramètres

Voici le rôle des principaux paramètres à définir dans le fichier `opensearch.yml` :

- **`cluster.name: graylog`**  
 <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> Définit le nom du cluster OpenSearch. Ici, il est nommé `graylog`. Ce nom identifie l’ensemble des nœuds du cluster.

- **`node.name: ${HOSTNAME}`**  
 <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> Attribue automatiquement au nœud le nom de la machine Linux locale (`${HOSTNAME}`). Même en environnement mono-nœud, il est conseillé de nommer le nœud.

- **`path.data: /var/lib/opensearch`**  
 <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> Spécifie l’emplacement local où OpenSearch stocke ses données.

- **`path.logs: /var/log/opensearch`**  
 <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> Indique le répertoire de stockage des fichiers journaux d’OpenSearch.

- **`discovery.type: single-node`**  
 <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> Configure OpenSearch pour un fonctionnement en mode mono-nœud. Idéal pour les environnements de test.

- **`network.host: 127.0.0.1`**  
 <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> Limite l’écoute d’OpenSearch à l’interface locale (loopback). Suffisant pour un usage local avec Graylog.

- **`action.auto_create_index: false`**  
 <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> Désactive la création automatique d’index. Cette configuration est nécessaire pour que Graylog gère correctement les index.

- **`plugins.security.disabled: true`**  
 <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> Désactive les fonctionnalités de sécurité intégrées (authentification, gestion des utilisateurs, chiffrement TLS). 
 <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-alert.svg" width="18" height="18" align="absmiddle" alt="" /> Ce paramètre est à utiliser uniquement pour les environnements de test ou de développement. **À éviter en production.**

###### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-puzzle.svg" width="18" height="18" align="absmiddle" alt="" /> Conseils de configuration

- Certaines options peuvent déjà exister dans le fichier `opensearch.yml`, mais être commentées avec un `#`.  
 <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> Il suffit alors de retirer le `#` et de modifier la valeur si nécessaire.

Pour finir Enregistrons et fermons ce fichier.

##### C. Configuration de Java (JVM)

###### Nous devons configurer Java Virtual Machine utilisé par OpenSearch afin d'ajuster la quantité de mémoire que peut utiliser ce service. Éditons le fichier de configuration suivant :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo nano /etc/opensearch/jvm.options
> ```
<!-- CODE-WINDOW-END -->

- Avec la configuration déployée ici, OpenSearch démarrera avec une mémoire allouée de 4 Go et pourra atteindre jusqu'à 4 Go, il n'y aura donc pas de variation de mémoire pendant le fonctionnement.

- Ici, la configuration tient compte du fait que la machine virtuelle dispose d'un total de 8 Go de RAM. Les deux paramètres doivent avoir la même valeur. Ceci implique de remplacer ces lignes :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> -Xms1g
> -Xmx1g
> ```
<!-- CODE-WINDOW-END -->

Par ces lignes :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> -Xms4g
> -Xmx4g
> ```
<!-- CODE-WINDOW-END -->

Fermons ce fichier après l'avoir enregistré.

###### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> Vérification du paramètre vm.max_map_count :

En complément de la configuration d’OpenSearch, il est important de vérifier la valeur du paramètre vm.max_map_count au niveau du noyau Linux.

Ce paramètre contrôle le nombre maximal de zones mémoire mappées par processus. OpenSearch (comme Elasticsearch) recommande une valeur minimale de 262144, afin d’éviter des erreurs lors de la gestion de la mémoire.

<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> Sur une installation récente de Debian 12, cette valeur est généralement déjà correctement définie. Par précaution, nous allons tout de même la vérifier.

Pour cela, exécutons la commande suivante :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> cat /proc/sys/vm/max_map_count
> ```
<!-- CODE-WINDOW-END -->

Si nous obtenons une valeur différente de "262144", exécutons la commande suivante, sinon ce n'est pas nécessaire.

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo sysctl -w vm.max_map_count=262144
> ```
<!-- CODE-WINDOW-END -->

Enfin, activez le démarrage automatique d'OpenSearch et lançons le service associé.


<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo systemctl daemon-reload
> ```
<!-- CODE-WINDOW-END -->

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo systemctl enable opensearch
> ```
<!-- CODE-WINDOW-END -->

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo systemctl restart opensearch
> ```
<!-- CODE-WINDOW-END -->

Si nous affichons l'état de votre système, nous devons voir un processus Java avec 4 Go de RAM.

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> top
> ```
<!-- CODE-WINDOW-END -->

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> top - 10:40:47 up  1:42,  1 user,  load average: 0,42, 0,13, 0,05
> Tâches: 219 total,   1 en cours, 218 en veille,   0 arrêté,   0 zombie
> %Cpu(s):  0,2 ut,  0,0 sy,  0,0 ni, 99,7 id,  0,1 wa,  0,0 hi,  0,0 si,  0,0 st
> MiB Mem :  15883,2 total,   6655,0 libr,   5822,7 util,   3916,1 tamp/cache
> MiB Éch :    977,0 total,    977,0 libr,      0,0 util.  10060,5 dispo Mem
>
>     PID UTIL.     PR  NI    VIRT    RES    SHR S  %CPU  %MEM    TEMPS+ COM.
>    3963 opensea+  20   0 9982,9m   4,4g  27064 S   1,3  28,7   0:41.54 java
> ```
<!-- CODE-WINDOW-END -->

Passez à la prochaine étape : l'installation tant attendue, celle de Graylog !

##### D. Installation de Graylog

Pour installer la dernière version de Graylog 6.1, il suffit d’exécuter les quatre commandes suivantes. Celles-ci permettent de télécharger et d’installer le serveur Graylog sur votre machine :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> wget https://packages.graylog2.org/repo/packages/graylog-6.1-repository_latest.deb
> ```
<!-- CODE-WINDOW-END -->

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo dpkg -i graylog-6.1-repository_latest.deb
> # Note : si packages.graylog2.org renvoie temporairement une erreur 503, verifiez que /etc/apt/sources.list.d/graylog.list pointe bien sur downloads.graylog.org :
> # deb https://downloads.graylog.org/repo/debian/ stable 6.1
> ```
<!-- CODE-WINDOW-END -->

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo apt-get update
> ```
<!-- CODE-WINDOW-END -->

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo apt-get install graylog-server
> ```
<!-- CODE-WINDOW-END -->

###### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-puzzle.svg" width="18" height="18" align="absmiddle" alt="" /> Configuration préalable de Graylog :

Avant de lancer Graylog, il est nécessaire de modifier certaines options de configuration.

Commencez par définir ces deux paramètres essentiels :

password_secret : cette clé unique et aléatoire est utilisée par Graylog pour sécuriser le stockage des mots de passe utilisateurs, un peu comme une clé de salage (salt).

root_password_sha2 : il s'agit du mot de passe administrateur par défaut, stocké sous forme de hachage SHA-256.

Pour débuter, nous allons générer une clé aléatoire de 96 caractères à utiliser comme valeur pour password_secret.

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> pwgen -N 1 -s 96
> ```
<!-- CODE-WINDOW-END -->

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> 7p0gEqEgNyyusvPj58H4CU7bOyr7MWKd5gOQFhcLWNwOljOX5DJi0VA2LK4q86HMEipmEbAmc8WMfitHLgKQuY2a0S3jzDm0 (96 caractères)
> ```
<!-- CODE-WINDOW-END -->

Copiez la valeur retournée, puis ouvrez le fichier de configuration de Graylog :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo nano /etc/graylog/server/server.conf
> ```
<!-- CODE-WINDOW-END -->

Collez la clé au niveau du paramètre password_secret = .

Enregistrez et fermez le fichier.

###### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-crypto.svg" width="18" height="18" align="absmiddle" alt="" /> Définition du mot de passe administrateur
Vous devez ensuite configurer le mot de passe du compte admin créé par défaut.

Dans le fichier de configuration, il faut stocker le hash du mot de passe, ce qui nécessite de le générer au préalable.

L’exemple ci-dessous montre comment obtenir le hash SHA-256 du mot de passe 'MonMotDePasse'. Pensez à remplacer cette valeur par votre propre mot de passe.

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> echo -n "MonMotDePasse" | sha256sum | awk '{print $1}'
> ```
<!-- CODE-WINDOW-END -->

ex : 

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> echo -n "S@B85-2025-SID" | sha256sum | awk '{print $1}'
> ```
<!-- CODE-WINDOW-END -->

Copiez la valeur obtenue en sortie (sans le tiret en bout de ligne).

Ouvrons de nouveau le fichier de configuration de Graylog :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo nano /etc/graylog/server/server.conf
> ```
<!-- CODE-WINDOW-END -->

Collons la valeur au niveau de l'option root_password_sha2 = .

###### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-puzzle.svg" width="18" height="18" align="absmiddle" alt="" /> Configuration de l'adresse d'écoute HTTP :

Modifier l’option « http_bind_address » par :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> http_bind_address = 10.200.200.101:9000
> ```
<!-- CODE-WINDOW-END -->

Modifier l’option « elasticsearch » par :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> elasticsearch_hosts = http://10.200.200.101:9200
> ```
<!-- CODE-WINDOW-END -->

Enregistrer et quitter.

Cette commande configure Graylog pour qu’il se lance automatiquement au démarrage du système et démarre immédiatement le service Graylog.

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo systemctl enable --now graylog-server
> ```
<!-- CODE-WINDOW-END -->

Une fois cette étape terminée, ouvrez un navigateur et connectez-vous à Graylog en utilisant l’adresse IP (ou le nom) du serveur, suivi du port 9000.

![Graylog-Login](./images/Graylog_auth.png)

À titre d’information :

Un message apparait dans la console Web de Graylog

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> There is a node without any running inputs
> (triggered a few seconds ago)
> There is a node without any running inputs. This means that you are not receiving any messages from this node at this point in time. This is most probably an indication of an error or misconfiguration. You can click here to solve this.
> ```
<!-- CODE-WINDOW-END -->

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> Il y a un nœud sans aucune entrée en cours d'exécution (déclenché il y a quelques secondes)
> Cela signifie que vous ne recevez aucun message de ce nœud à ce stade.
> ```
<!-- CODE-WINDOW-END -->

Ce message d’alerte de l’interface Graylog est tout à fait normal juste après l’installation :

<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-ok.svg" width="42" height="16" align="absmiddle" alt="[OK]" /> Pourquoi ce message s'affiche ?
Graylog fonctionne comme un collecteur de logs centralisé, mais il a besoin qu’au moins une "input" soit créée pour commencer à recevoir des messages (logs syslog, GELF, journaux Windows, etc.).

<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-ok.svg" width="42" height="16" align="absmiddle" alt="[OK]" /> Comment résoudre le message : "you are not receiving any messages from this node"

1) - Va dans l'interface web de Graylog (port 9000)
2) - Dans le menu latéral, clique sur :
 - System → Inputs
3) - Dans le menu déroulant « Select input », choisis un type d’entrée à activer, par exemple :
 - Syslog UDP (si tu veux recevoir des logs syslog via UDP)Syslog TCP
 - GELF UDP / TCP (format Graylog Extended Log Format)
 - Beats input (si tu envoies des logs avec Filebeat/Winlogbeat)
4) - Clique sur « Launch new input »
 - Remplis les paramètres (interface d’écoute, port, nom personnalisé, etc.)
 - Clique sur « Save »

###### E. Création d’un compte administrateur

Créer un nouveau compte administrateur

Au lieu d’utiliser le compte admin par défaut fourni avec Graylog, il est recommandé de créer votre propre compte administrateur.

Pour cela, accédez au menu « System », puis sélectionnez « Users and Teams ». Cliquez ensuite sur le bouton « Create user », remplissez le formulaire avec les informations souhaitées, et attribuez à ce compte le rôle administrateur.

---

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> IV. Conclusion.

Félicitations, vous avez installé Graylog sur une machine Debian 12 ! Vous pouvez maintenant centraliser, indexer et analyser vos logs depuis une interface unique et puissante.

<!-- MASTER-FOOTER-START -->
<div align="center">
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/divider-hud.svg" alt="" width="100%" />

<a href="https://0xcyberlitech.com/">
  <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/footer-master.svg" alt="0xCyberLiTech — Architecture Cyberdéfense, Ingénierie Déterministe & IA Souveraine" width="100%" />
</a>

<p align="center"><a href="https://0xcyberlitech.com/"><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/badge-antigravity.svg" alt="Architecturé par Marc & Antigravity (Google DeepMind)" width="520" /></a></p>

<sub><b>Architecturé &amp; Forgé par Marc &amp; Antigravity (Google DeepMind)</b> &nbsp;·&nbsp; <a href="https://0xcyberlitech.com/"><b>0xcyberlitech.com</b></a> &nbsp;·&nbsp; <a href="https://0xcyberlitech.com/soc-rd.html">Architecture SOC Cockpit v5.5</a> &nbsp;·&nbsp; <a href="https://0xcyberlitech.com/jarvis-rd.html">Architecture JARVIS Mark-VII</a> &nbsp;·&nbsp; <a href="https://0xcyberlitech.com/blueprint-jarvis.html">Blueprint Matériel RTX 5080</a></sub>

</div>
<!-- MASTER-FOOTER-END -->
