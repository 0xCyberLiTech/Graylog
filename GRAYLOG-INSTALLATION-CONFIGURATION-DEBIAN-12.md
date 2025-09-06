<div align="center">

  <br></br>
  
  <a href="https://github.com/0xCyberLiTech">
    <img src="https://readme-typing-svg.herokuapp.com?font=JetBrains+Mono&size=50&duration=6000&pause=1000000000&color=FF0048&center=true&vCenter=true&width=1100&lines=%3EGRAYLOG_" alt="Titre dynamique GRAYLOG" />
  </a>
  
  <br></br>
  
  <h2>Laboratoire numérique pour la cybersécurité, Linux & IT.</h2>

  <p align="center">
    <a href="https://0xcyberlitech.github.io/">
      <img src="https://img.shields.io/badge/Portfolio-0xCyberLiTech-181717?logo=github&style=flat-square" alt="🌐 Portfolio" />
    </a>
    <a href="https://github.com/0xCyberLiTech">
      <img src="https://img.shields.io/badge/Profil-GitHub-181717?logo=github&style=flat-square" alt="🔗 Profil GitHub" />
    </a>
    <a href="https://github.com/0xCyberLiTech/Graylog/releases/latest">
      <img src="https://img.shields.io/github/v/release/0xCyberLiTech/Graylog?label=version&style=flat-square&color=blue" alt="📦 Dernière version" />
    </a>
    <a href="https://github.com/0xCyberLiTech/Graylog/blob/main/CHANGELOG.md">
      <img src="https://img.shields.io/badge/📄%20Changelog-Graylog-blue?style=flat-square" alt="📄 CHANGELOG Graylog" />
    </a>
    <a href="https://github.com/0xCyberLiTech?tab=repositories">
      <img src="https://img.shields.io/badge/Dépôts-publics-blue?style=flat-square" alt="📂 Dépôts publics" />
    </a>
    <a href="https://github.com/0xCyberLiTech/Graylog/graphs/contributors">
      <img src="https://img.shields.io/badge/👥%20Contributeurs-cliquez%20ici-007ec6?style=flat-square" alt="👥 Contributeurs Graylog" />
    </a>
  </p>

</div>

<div align="center">
  <img src="https://img.icons8.com/fluency/96/000000/cyber-security.png" alt="CyberSec" width="80"/>
</div>

<div align="center">
  <p>
    <strong>Cybersécurité</strong> <img src="https://img.icons8.com/color/24/000000/lock--v1.png"/> • <strong>Linux Debian</strong> <img src="https://img.icons8.com/color/24/000000/linux.png"/> • <strong>Sécurité informatique</strong> <img src="https://img.icons8.com/color/24/000000/shield-security.png"/>
  </p>
</div>

---

<div align="center">
  
## À propos & Objectifs.

</div>

Ce projet propose des solutions innovantes et accessibles en cybersécurité, avec une approche centrée sur la simplicité d’utilisation et l’efficacité. Il vise à accompagner les utilisateurs dans la protection de leurs données et systèmes, tout en favorisant l’apprentissage et le partage des connaissances.

Le contenu est structuré, accessible et optimisé SEO pour répondre aux besoins de :
- 🎓 Étudiants : approfondir les connaissances
- 👨‍💻 Professionnels IT : outils et pratiques
- 🖥️ Administrateurs système : sécuriser l’infrastructure
- 🛡️ Experts cybersécurité : ressources techniques
- 🚀 Passionnés du numérique : explorer les bonnes pratiques

---

# Installer Graylog sur Debian 12.

---

## Sommaire :

<div align="center">

| Section | Description | Accès Direct |
|:---:|:---|:---:|
| **1.** | Présentation | [<img src="https://img.shields.io/badge/ACCÉDER-blue?style=for-the-badge&logo=github&logoColor=white">](#i-présentation) |
| **2.** | Prérequis | [<img src="https://img.shields.io/badge/ACCÉDER-blue?style=for-the-badge&logo=github&logoColor=white">](#ii-prérequis) |
| **3.** | Installation pas à pas de Graylog | [<img src="https://img.shields.io/badge/ACCÉDER-blue?style=for-the-badge&logo=github&logoColor=white">](#iii-installation-pas-à-pas-de-graylog) |
| **3.A** | ↳ Installation de MongoDB | [<img src="https://img.shields.io/badge/ACCÉDER-lightgrey?style=flat-square&logo=github">](#a-installation-de-mongodb) |
| **3.B** | ↳ Installation d'OpenSearch | [<img src="https://img.shields.io/badge/ACCÉDER-lightgrey?style=flat-square&logo=github">](#b-installation-dopensearch) |
| **3.C** | ↳ Configuration de Java (JVM) | [<img src="https://img.shields.io/badge/ACCÉDER-lightgrey?style=flat-square&logo=github">](#c-configuration-de-java-jvm) |
| **3.D** | ↳ Installation de Graylog | [<img src="https://img.shields.io/badge/ACCÉDER-lightgrey?style=flat-square&logo=github">](#d-installation-de-graylog) |
| **3.E** | ↳ Création d’un compte administrateur | [<img src="https://img.shields.io/badge/ACCÉDER-lightgrey?style=flat-square&logo=github">](#e-création-dun-compte-administrateur) |
| **4.** | Conclusion | [<img src="https://img.shields.io/badge/ACCÉDER-blue?style=for-the-badge&logo=github&logoColor=white">](#iv-conclusion) |

</div>


---

### I. Présentation.

#### 🔍 Qu'est-ce que Graylog ?

**Graylog** est une plateforme open source de **gestion centralisée des journaux** (logs) permettant la **collecte**, **l’analyse**, **la recherche** et **la visualisation** en temps réel de données issues de différents systèmes, serveurs, applications ou équipements réseau.

Il est particulièrement utilisé en **cybersécurité**, en **monitoring**, et pour la **traçabilité** des événements systèmes.

---

#### ⚙️ Fonctionnalités clés.

- 🧲 **Collecte de logs** multi-sources : syslog, fichiers journaux, flux réseau, etc.
- 🔎 **Moteur de recherche puissant** basé sur **Elasticsearch**.
- 📊 **Dashboards interactifs** : création de graphiques et widgets personnalisés.
- 📁 **Archivage et rotation automatique** des logs.
- 🛡️ **Détection d'incidents** et d'anomalies.
- 📦 Extensible avec des **plugins** et des **pipelines de traitement**.

---

#### 🏗️ Architecture.

Graylog repose sur :
- **MongoDB** (base de données de configuration),
- **Elasticsearch** ou **OpenSearch** (moteur d’indexation et de recherche),
- **Graylog Server** (cœur applicatif),
- **Graylog Web Interface** (interface graphique de consultation).

---

#### 📈 Cas d’usages typiques.

- 🛡️ Surveillance de la sécurité (SIEM léger),
- 🖥️ Supervision des serveurs (logs Apache/Nginx, SSH, etc.),
- 📡 Analyse des événements réseau,
- 📦 Suivi des conteneurs Docker, Kubernetes,
- 🔐 Détection d'intrusion ou analyse forensic.

---

#### ✅ Avantages.

- Interface web moderne et intuitive,
- Filtrage avancé avec requêtes personnalisées,
- Très bonne performance même avec un grand volume de logs,
- Open source avec une **édition communautaire gratuite**,
- Évolutif en version **Entreprise ou Cloud** pour les environnements critiques.

---

#### 🚀 Pourquoi utiliser Graylog ?

Graylog simplifie la gestion des logs dans un environnement distribué, en rendant possible l’**agrégation et l’analyse rapide** de millions d’événements. C’est une solution efficace pour :

- Répondre aux exigences de conformité (RGPD, PCI-DSS…),
- Identifier rapidement les anomalies et incidents,
- Faciliter le diagnostic et le dépannage système.

---

### II. Prérequis.

Avant de procéder à l’installation de Graylog, assurez-vous que les prérequis suivants sont respectés.

#### Composants requis

- **MongoDB 6** (versions supportées : ≥ 5.0.7 et ≤ 7.x)  
- **OpenSearch** (fork open source d’Elasticsearch développé par Amazon — versions supportées : de 1.1.x à 2.15.x)  
- **OpenJDK 17**

#### Configuration système recommandée

- **Système d’exploitation** : Debian 12 (autres distributions GNU/Linux également compatibles, ou installation via Docker)  
- **Mémoire vive (RAM)** : 8 Go minimum  
- **Espace disque** : 256 Go minimum

> **Remarque** : Ces spécifications sont fournies à titre indicatif. Le dimensionnement dépend du volume de logs à traiter. Graylog peut gérer aussi bien quelques mégaoctets que plusieurs téraoctets de données par jour.

#### Préparation de la machine

Avant de commencer l’installation :

- Attribuez une **adresse IP statique** à la machine ;
- Installez les **dernières mises à jour** du système ;
- Vérifiez que le **fuseau horaire** est correctement configuré ;
- Définissez un **serveur NTP** pour la synchronisation de l’heure.

```bash
sudo timedatectl set-timezone Europe/Paris
```

#### Mise à jour du système

```bash
sudo apt update && sudo apt upgrade -y
```

---

### III. Installation pas à pas de Graylog

Mise à jour du cache des paquets et installation de paquets supplémentaires pour la suite :

```bash
sudo apt-get update
```

```bash
sudo apt-get install curl lsb-release ca-certificates gnupg2 pwgen
```

##### A. Installation de MongoDB

Commençez par installer MongoDB, puis récupérez la clé GPG correspondante au dépôt MongoDB.

```bash
curl -fsSL https://www.mongodb.org/static/pgp/server-6.0.asc | sudo gpg -o /usr/share/keyrings/mongodb-server-6.0.gpg --dearmor
```

Ajoutez le dépôt de MongoDB 6 pour Debian 12 :

```bash
echo "deb [ signed-by=/usr/share/keyrings/mongodb-server-6.0.gpg] http://repo.mongodb.org/apt/debian bullseye/mongodb-org/6.0 main" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list
```

Allez mettre à jour le cache des paquets et tenter d'installer MongoDB :

```bash
sudo apt-get update
```

```
Réception de :4 http://repo.mongodb.org/apt/debian bullseye/mongodb-org/6.0 InRelease [2 951 B]
Réception de :5 http://repo.mongodb.org/apt/debian bullseye/mongodb-org/6.0/main amd64 Packages [105 kB]
```

```bash
sudo apt-get install -y mongodb-org
```

L'installation de MongoDB ne peut pas être effectuée, car il manque une dépendance : libssl1.1. Nous allons devoir installer ce paquet manuellement avant de pouvoir poursuivre parce que Debian 12 ne l'a pas dans ses dépôts.

On peut constatez :

```
Les paquets suivants contiennent des dépendances non satisfaites :
 mongodb-org-mongos : Dépend: libssl1.1 (>= 1.1.1) mais il n'est pas installable
 mongodb-org-server : Dépend: libssl1.1 (>= 1.1.1) mais il n'est pas installable
Impossible de corriger les problèmes, des paquets défectueux sont en mode « garder en l'état ».
```

Vous allez télécharger le paquet DEB nommé "libssl1.1_1.1.1f-1ubuntu2.24_amd64.deb" (version la plus récente) avec la commande wget, puis procéder à son installation via la commande dpkg. Ce qui donne les deux commandes suivantes :

```bash
wget http://archive.ubuntu.com/ubuntu/pool/main/o/openssl/libssl1.1_1.1.1f-1ubuntu2.24_amd64.deb
```

```bash
sudo dpkg -i libssl1.1_1.1.1f-1ubuntu2.24_amd64.deb
```
On peut constatez :

```bash
Préparation du dépaquetage de libssl1.1_1.1.1f-1ubuntu2.24_amd64.deb ...
Dépaquetage de libssl1.1:amd64 (1.1.1f-1ubuntu2.24) ...
Paramétrage de libssl1.1:amd64 (1.1.1f-1ubuntu2.24) ...
Traitement des actions différées (« triggers ») pour libc-bin (2.36-9+deb12u10) ...
```

Relançons l'installation de MongoDB :

```bash
sudo apt-get install -y mongodb-org
```

On peut constatez l'installation du paquet mongodb-org :

```bash
54% [2 mongodb-mongosh 48,3 MB/57,0 MB 85%]   
```

Ensuite, vous relancez le service MongoDB et activez son démarrage automatique au lancement du serveur Debian.

```bash
sudo systemctl daemon-reload
```

```bash
sudo systemctl enable mongod.service
```

```bash
sudo systemctl restart mongod.service
```

```bash
sudo systemctl --type=service --state=active | grep mongod
```

MongoDB est installé, vous pouvez passer à l'installation du prochain composant.


##### B. Installation d'OpenSearch.

A présent vous allez passer à l'installation d'OpenSearch. La commande suivante permet d’ajouter la clé de signature pour les paquets OpenSearch :

```bash
curl -o- https://artifacts.opensearch.org/publickeys/opensearch.pgp | sudo gpg --dearmor --batch --yes -o /usr/share/keyrings/opensearch-keyring
```

Puis, ajoutez le dépôt OpenSearch pour que nous puissions télécharger le paquet avec apt par la suite :

```bash
echo "deb [signed-by=/usr/share/keyrings/opensearch-keyring] https://artifacts.opensearch.org/releases/bundle/opensearch/2.x/apt stable main" | sudo tee /etc/apt/sources.list.d/opensearch-2.x.list
```
Mettez à jour votre cache de paquets :

```bash
sudo apt-get update
```
Procédez ensuite à l’installation d’OpenSearch, en veillant à définir un mot de passe sécurisé pour le compte administrateur de l’instance.
Dans cet exemple, le mot de passe utilisé est : MonMotDePasse, mais il est fortement recommandé de choisir votre propre mot de passe robuste.

⚠️ Évitez les mots de passe faibles comme P@ssword, car cela entraînera une erreur à la fin de l’installation. Depuis la version 2.12 d’OpenSearch, l’installation impose un mot de passe répondant aux critères suivants :

Minimum 8 caractères :

Contient au moins :

- Une lettre minuscule
- Une lettre majuscule
- Un chiffre
- Un caractère spécial

```bash
sudo env OPENSEARCH_INITIAL_ADMIN_PASSWORD=CLT-Connect2025# apt-get install opensearch
```

Patientez pendant l'installation...

Quand c'est terminé, prenez le temps d'effectuer la configuration minimale. Ouvrez le fichier de configuration au format YAML :

```bash
sudo nano /etc/opensearch/opensearch.yml
```

Configurez les options suivantes :

```bash
cluster.name: graylog
node.name: ${HOSTNAME}
path.data: /var/lib/opensearch
path.logs: /var/log/opensearch
discovery.type: single-node
network.host: 1O.200.200.101
action.auto_create_index: false
plugins.security.disabled: true
```
Cette configuration OpenSearch est destinée à configurer un nœud unique. 

##### Paramètres de configuration d’OpenSearch pour Graylog

###### 📘 Explication des paramètres

Voici le rôle des principaux paramètres à définir dans le fichier `opensearch.yml` :

- **`cluster.name: graylog`**  
  ➤ Définit le nom du cluster OpenSearch. Ici, il est nommé `graylog`. Ce nom identifie l’ensemble des nœuds du cluster.

- **`node.name: ${HOSTNAME}`**  
  ➤ Attribue automatiquement au nœud le nom de la machine Linux locale (`${HOSTNAME}`). Même en environnement mono-nœud, il est conseillé de nommer le nœud.

- **`path.data: /var/lib/opensearch`**  
  ➤ Spécifie l’emplacement local où OpenSearch stocke ses données.

- **`path.logs: /var/log/opensearch`**  
  ➤ Indique le répertoire de stockage des fichiers journaux d’OpenSearch.

- **`discovery.type: single-node`**  
  ➤ Configure OpenSearch pour un fonctionnement en mode mono-nœud. Idéal pour les environnements de test.

- **`network.host: 127.0.0.1`**  
  ➤ Limite l’écoute d’OpenSearch à l’interface locale (loopback). Suffisant pour un usage local avec Graylog.

- **`action.auto_create_index: false`**  
  ➤ Désactive la création automatique d’index. Cette configuration est nécessaire pour que Graylog gère correctement les index.

- **`plugins.security.disabled: true`**  
  ➤ Désactive les fonctionnalités de sécurité intégrées (authentification, gestion des utilisateurs, chiffrement TLS).  
  ⚠️ Ce paramètre est à utiliser uniquement pour les environnements de test ou de développement. **À éviter en production.**

###### 🔧 Conseils de configuration

- Certaines options peuvent déjà exister dans le fichier `opensearch.yml`, mais être commentées avec un `#`.  
  ➤ Il suffit alors de retirer le `#` et de modifier la valeur si nécessaire.

Pour finir Enregistrons et fermons ce fichier.

##### C. Configuration de Java (JVM)

###### Nous devons configurer Java Virtual Machine utilisé par OpenSearch afin d'ajuster la quantité de mémoire que peut utiliser ce service. Éditons le fichier de configuration suivant :

```bash
sudo nano /etc/opensearch/jvm.options
```

- Avec la configuration déployée ici, OpenSearch démarrera avec une mémoire allouée de 4 Go et pourra atteindre jusqu'à 4 Go, il n'y aura donc pas de variation de mémoire pendant le fonctionnement.

- Ici, la configuration tient compte du fait que la machine virtuelle dispose d'un total de 8 Go de RAM. Les deux paramètres doivent avoir la même valeur. Ceci implique de remplacer ces lignes :

```
-Xms1g
-Xmx1g
```

Par ces lignes :

```
-Xms4g
-Xmx4g
```

Fermons ce fichier après l'avoir enregistré.

###### 🔍 Vérification du paramètre vm.max_map_count :

En complément de la configuration d’OpenSearch, il est important de vérifier la valeur du paramètre vm.max_map_count au niveau du noyau Linux.

Ce paramètre contrôle le nombre maximal de zones mémoire mappées par processus. OpenSearch (comme Elasticsearch) recommande une valeur minimale de 262144, afin d’éviter des erreurs lors de la gestion de la mémoire.

💡 Sur une installation récente de Debian 12, cette valeur est généralement déjà correctement définie. Par précaution, nous allons tout de même la vérifier.

Pour cela, exécutons la commande suivante :

```bash
cat /proc/sys/vm/max_map_count
```

Si nous obtenons une valeur différente de "262144", exécutons la commande suivante, sinon ce n'est pas nécessaire.

```bash
sudo sysctl -w vm.max_map_count=262144
```

Enfin, activez le démarrage automatique d'OpenSearch et lançons le service associé.


```bash
sudo systemctl daemon-reload
```

```bash
sudo systemctl enable opensearch
```

```bash
sudo systemctl restart opensearch
```

Si nous affichons l'état de votre système, nous devons voir un processus Java avec 4 Go de RAM.

```bash
top
```

```bash
top - 10:40:47 up  1:42,  1 user,  load average: 0,42, 0,13, 0,05
Tâches: 219 total,   1 en cours, 218 en veille,   0 arrêté,   0 zombie
%Cpu(s):  0,2 ut,  0,0 sy,  0,0 ni, 99,7 id,  0,1 wa,  0,0 hi,  0,0 si,  0,0 st
MiB Mem :  15883,2 total,   6655,0 libr,   5822,7 util,   3916,1 tamp/cache
MiB Éch :    977,0 total,    977,0 libr,      0,0 util.  10060,5 dispo Mem

    PID UTIL.     PR  NI    VIRT    RES    SHR S  %CPU  %MEM    TEMPS+ COM.
   3963 opensea+  20   0 9982,9m   4,4g  27064 S   1,3  28,7   0:41.54 java
```

Passez à la prochaine étape : l'installation tant attendue, celle de Graylog !

##### D. Installation de Graylog

Pour installer la dernière version de Graylog 6.1, il suffit d’exécuter les quatre commandes suivantes. Celles-ci permettent de télécharger et d’installer le serveur Graylog sur votre machine :

```bash
wget https://packages.graylog2.org/repo/packages/graylog-6.1-repository_latest.deb
```

```bash
sudo dpkg -i graylog-6.1-repository_latest.deb
```

```bash
sudo apt-get update
```

```bash
sudo apt-get install graylog-server
```

###### 🔧 Configuration préalable de Graylog :

Avant de lancer Graylog, il est nécessaire de modifier certaines options de configuration.

Commencez par définir ces deux paramètres essentiels :

password_secret : cette clé unique et aléatoire est utilisée par Graylog pour sécuriser le stockage des mots de passe utilisateurs, un peu comme une clé de salage (salt).

root_password_sha2 : il s'agit du mot de passe administrateur par défaut, stocké sous forme de hachage SHA-256.

Pour débuter, nous allons générer une clé aléatoire de 96 caractères à utiliser comme valeur pour password_secret.

```bash
pwgen -N 1 -s 96
```

```bash
7p0gEqEgNyyusvPj58H4CU7bOyr7MWKd5gOQFhcLWNwOljOX5DJi0VA2LK4q86HMEipmEbAmc8WMfitHLgKQuY2a0S3jzDm0 (96 caractères)
```

Copiez la valeur retournée, puis ouvrez le fichier de configuration de Graylog :

```bash
sudo nano /etc/graylog/server/server.conf
```

Collez la clé au niveau du paramètre password_secret = .

Enregistrez et fermez le fichier.

###### 🔐 Définition du mot de passe administrateur
Vous devez ensuite configurer le mot de passe du compte admin créé par défaut.

Dans le fichier de configuration, il faut stocker le hash du mot de passe, ce qui nécessite de le générer au préalable.

L’exemple ci-dessous montre comment obtenir le hash SHA-256 du mot de passe 'MonMotDePasse'. Pensez à remplacer cette valeur par votre propre mot de passe.

```bash
echo -n "MonMotDePasse" | sha256sum | awk '{print $1}'
```
ex : 

```conf
echo -n "S@B85-2025-SID" | sha256sum | awk '{print $1}'
```

Copiez la valeur obtenue en sortie (sans le tiret en bout de ligne).

Ouvrons de nouveau le fichier de configuration de Graylog :

```bash
sudo nano /etc/graylog/server/server.conf
```

Collons la valeur au niveau de l'option root_password_sha2 = .

###### ⚙️ Configuration de l'adresse d'écoute HTTP :

Modifier l’option « http_biend_address » par :

```bash
http_bind_address = 10.200.200.101:9000
```

Modifier l’option « elasticsearch » par :

```bash
elasticsearch_hosts = http://10.200.200.101:9200
```

Enregistrer et quitter.

Cette commande configure Graylog pour qu’il se lance automatiquement au démarrage du système et démarre immédiatement le service Graylog.

```bash
sudo systemctl enable --now graylog-server
```

Une fois cette étape terminée, ouvrez un navigateur et connectez-vous à Graylog en utilisant l’adresse IP (ou le nom) du serveur, suivi du port 9000.

![Graylog-Login](./images/Graylog_auth.png)

À titre d’information :

Un message apparait dans la console Web de Graylog

```
There is a node without any running inputs
(triggered a few seconds ago)
There is a node without any running inputs. This means that you are not receiving any messages from this node at this point in time. This is most probably an indication of an error or misconfiguration. You can click here to solve this.
```

```
Il y a un nœud sans aucune entrée en cours d'exécution (déclenché il y a quelques secondes)
Cela signifie que vous ne recevez aucun message de ce nœud à ce stade.
```

Ce message d’alerte de l’interface Graylog est tout à fait normal juste après l’installation :

✅ Pourquoi ce message s'affiche ?
Graylog fonctionne comme un collecteur de logs centralisé, mais il a besoin qu’au moins une "input" soit créée pour commencer à recevoir des messages (logs syslog, GELF, journaux Windows, etc.).

✅ Comment résoudre le message : "you are not receiving any messages from this node"

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

### IV. Conclusion.

Félicitations, vous avez installé Graylog sur une machine Debian 12 ! Vous pouvez maintenant centraliser, indexer et analyser vos logs depuis une interface unique et puissante.

---

<div align="center">
  <a href="https://github.com/0xCyberLiTech" target="_blank" rel="noopener">
    <img src="https://skillicons.dev/icons?i=linux,debian,bash,docker,nginx,git,vim,python,markdown" alt="Skills" width="440">
  </a>
</div>

<div align="center">
  <b>🔒 Un guide proposé par <a href="https://github.com/0xCyberLiTech">0xCyberLiTech</a> • Pour des tutoriels accessibles à tous. 🔒</b>
</div>

