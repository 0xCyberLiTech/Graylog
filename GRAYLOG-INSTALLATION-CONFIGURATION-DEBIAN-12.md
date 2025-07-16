<div align="center">
<a href="https://github.com/0xCyberLiTech">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&size=32&pause=1000&color=D14A4A&center=true&vCenter=true&width=1000&lines=SUPERVISION+CENTRALISÉE+AVEC+GRAYLOG;Détection+des+menaces+•+Logs+structurés+•+Alertes;Tutoriel+pédagogique+100%+Debian+12" alt="Typing SVG" />
</a>

<p align="center">
  <em>Tuto, installation & configurations d'un serveur Graylog 6.3 sur Debian 12.</em><br>
  <b>📊 Monitoring – 📈 Performance – ⚙️ Fiabilité</b>
</p>

</div>

---

### 👨‍💻 **À propos de moi.**

> Ce dépôt constitue mon laboratoire numérique où je consigne rigoureusement mes apprentissages et expérimentations.
> Passionné par l'écosystème Linux et la cybersécurité, je documente mon parcours et mes projets sur mon GitHub.
> Vous y trouverez des guides pratiques sur la supervision (Zabbix, Nagios), la conteneurisation (Docker) et la sécurisation de serveurs Debian.
> Mon objectif : partager mes connaissances de manière claire et pédagogique.
> N'hésitez pas à y jeter un œil : https://github.com/0xcyberlitech

<p align="center">
  <a href="https://skillicons.dev">
    <img src="https://skillicons.dev/icons?i=linux,debian,bash,docker,nginx,grafana,prometheus,git,vim" />
  </a>
</p>

---

### 🎯 **Objectif de ce dépôt.**

> Ce dépôt a pour vocation de centraliser un ensemble de notions clés concernant la journalisation des logs avec Graylog. Il s'adresse aux passionnés, étudiants et professionnels souhaitant mieux comprendre les enjeux de cet équipement de
> sécurité fondamental, apprendre à mettre en place ses configurations efficaces, et se familiariser avec les concepts et bonnes pratiques pour maintenir la performance et la stabilité de leurs systèmes
> d'information face aux menaces externes.

---

# Installer Graylog sur Debian 12 afin de centraliser et analyser vos logs de manière plus conviviale.

---

## Sommaire [-]

## I. Présentation
## II. Prérequis
## III. Installation pas à pas de Graylog
### A. Installation de MongoDB
### B. Installation d'OpenSearch
### C. Configurer Java (JVM)
### D. Installation de Graylog
### E. Graylog : créer un nouveau compte administrateur
## IV. Conclusion

---

## I. 🛰️ Présentation de **Graylog**.

### 🔍 Qu'est-ce que Graylog ?

**Graylog** est une plateforme open source de **gestion centralisée des journaux** (logs) permettant la **collecte**, **l’analyse**, **la recherche** et **la visualisation** en temps réel de données issues de différents systèmes, serveurs, applications ou équipements réseau.

Il est particulièrement utilisé en **cybersécurité**, en **monitoring**, et pour la **traçabilité** des événements systèmes.

---

### ⚙️ Fonctionnalités clés.

- 🧲 **Collecte de logs** multi-sources : syslog, fichiers journaux, flux réseau, etc.
- 🔎 **Moteur de recherche puissant** basé sur **Elasticsearch**.
- 📊 **Dashboards interactifs** : création de graphiques et widgets personnalisés.
- 📁 **Archivage et rotation automatique** des logs.
- 🛡️ **Détection d'incidents** et d'anomalies.
- 📦 Extensible avec des **plugins** et des **pipelines de traitement**.

---

### 🏗️ Architecture.

Graylog repose sur :
- **MongoDB** (base de données de configuration),
- **Elasticsearch** ou **OpenSearch** (moteur d’indexation et de recherche),
- **Graylog Server** (cœur applicatif),
- **Graylog Web Interface** (interface graphique de consultation).

---

### 📈 Cas d’usages typiques.

- 🛡️ Surveillance de la sécurité (SIEM léger),
- 🖥️ Supervision des serveurs (logs Apache/Nginx, SSH, etc.),
- 📡 Analyse des événements réseau,
- 📦 Suivi des conteneurs Docker, Kubernetes,
- 🔐 Détection d'intrusion ou analyse forensic.

---

### ✅ Avantages.

- Interface web moderne et intuitive,
- Filtrage avancé avec requêtes personnalisées,
- Très bonne performance même avec un grand volume de logs,
- Open source avec une **édition communautaire gratuite**,
- Évolutif en version **Entreprise ou Cloud** pour les environnements critiques.

---

## 🚀 Pourquoi utiliser Graylog ?

Graylog simplifie la gestion des logs dans un environnement distribué, en rendant possible l’**agrégation et l’analyse rapide** de millions d’événements. C’est une solution efficace pour :

- Répondre aux exigences de conformité (RGPD, PCI-DSS…),
- Identifier rapidement les anomalies et incidents,
- Faciliter le diagnostic et le dépannage système.

---

## II. Prérequis pour l'installation de Graylog

Avant de procéder à l’installation de Graylog, assurez-vous que les prérequis suivants sont respectés.

### Composants requis

- **MongoDB 6** (versions supportées : ≥ 5.0.7 et ≤ 7.x)  
- **OpenSearch** (fork open source d’Elasticsearch développé par Amazon — versions supportées : de 1.1.x à 2.15.x)  
- **OpenJDK 17**

### Configuration système recommandée

- **Système d’exploitation** : Debian 12 (autres distributions GNU/Linux également compatibles, ou installation via Docker)  
- **Mémoire vive (RAM)** : 8 Go minimum  
- **Espace disque** : 256 Go minimum

> **Remarque** : Ces spécifications sont fournies à titre indicatif. Le dimensionnement dépend du volume de logs à traiter. Graylog peut gérer aussi bien quelques mégaoctets que plusieurs téraoctets de données par jour.

### Préparation de la machine

Avant de commencer l’installation :

- Attribuez une **adresse IP statique** à la machine ;
- Installez les **dernières mises à jour** du système ;
- Vérifiez que le **fuseau horaire** est correctement configuré ;
- Définissez un **serveur NTP** pour la synchronisation de l’heure.

```bash
sudo timedatectl set-timezone Europe/Paris
```

### Mise à jour du système

```bash
sudo apt update && sudo apt upgrade -y
```

---

## III. Installation pas à pas de Graylog

Mise à jour du cache des paquets et installation d'outils nécessaires pour la suite.


```bash
sudo apt-get update
```
```bash
sudo apt-get install curl lsb-release ca-certificates gnupg2 pwgen
```

### A. Installation de MongoDB

Commençons par installer MongoDB, récupération de la clé GPG correspondante au dépôt MongoDB.

```bash
curl -fsSL https://www.mongodb.org/static/pgp/server-6.0.asc | sudo gpg -o /usr/share/keyrings/mongodb-server-6.0.gpg --dearmor
```

Ajoutons le dépôt de MongoDB 6 pour Debian 12 :

```bash
echo "deb [ signed-by=/usr/share/keyrings/mongodb-server-6.0.gpg] http://repo.mongodb.org/apt/debian bullseye/mongodb-org/6.0 main" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list
```

Allons mettre à jour le cache des paquets et tenter d'installer MongoDB :

```bash
sudo apt-get update
```

```bash
sudo apt-get install -y mongodb-org
```

L'installation de MongoDB ne peut pas être effectuée, car il manque une dépendance : libssl1.1. Nous allons devoir installer ce paquet manuellement avant de pouvoir poursuivre parce que Debian 12 ne l'a pas dans ses dépôts.

```
Les paquets suivants contiennent des dépendances non satisfaites :
 mongodb-org-mongos : Dépend: libssl1.1 (>= 1.1.1) mais il n'est pas installable
 mongodb-org-server : Dépend: libssl1.1 (>= 1.1.1) mais il n'est pas installable
E: Impossible de corriger les problèmes, des paquets défectueux sont en mode « garder en l'état ».
```

Nous allons télécharger le paquet DEB nommé "libssl1.1_1.1.1f-1ubuntu2.23_amd64.deb" (version la plus récente) avec la commande wget, puis procéder à son installation via la commande dpkg. Ce qui donne les deux commandes suivantes :

```bash
wget http://archive.ubuntu.com/ubuntu/pool/main/o/openssl/libssl1.1_1.1.1f-1ubuntu2.23_amd64.deb
```

```bash
sudo dpkg -i libssl1.1_1.1.1f-1ubuntu2.23_amd64.deb
```

Relançons l'installation de MongoDB :

```bash
sudo apt-get install -y mongodb-org
```

Ensuite, nous relançons le service MongoDB et activons son démarrage automatique au lancement du serveur Debian.

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

MongoDB est installé, nous pouvons passer à l'installation du prochain composant.


### B. Installation d'OpenSearch.

A présent nous allons passer à l'installation d'OpenSearch. La commande suivante permet d’ajouter la clé de signature pour les paquets OpenSearch :

```bash
curl -o- https://artifacts.opensearch.org/publickeys/opensearch.pgp | sudo gpg --dearmor --batch --yes -o /usr/share/keyrings/opensearch-keyring
```

Puis, ajoutez le dépôt OpenSearch pour que nous puissions télécharger le paquet avec apt par la suite :

```bash
echo "deb [signed-by=/usr/share/keyrings/opensearch-keyring] https://artifacts.opensearch.org/releases/bundle/opensearch/2.x/apt stable main" | sudo tee /etc/apt/sources.list.d/opensearch-2.x.list
```
Mettons à jour votre cache de paquets :

```bash
sudo apt-get update
```
Procédons ensuite à l’installation d’OpenSearch, en veillant à définir un mot de passe sécurisé pour le compte administrateur de l’instance.
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

Patientons pendant l'installation...

Quand c'est terminé, prenons le temps d'effectuer la configuration minimale. Ouvrons le fichier de configuration au format YAML :

```bash
sudo nano /etc/opensearch/opensearch.yml
```

Configurons les options suivantes :

```bash
cluster.name: graylog
node.name: ${HOSTNAME}
path.data: /var/lib/opensearch
path.logs: /var/log/opensearch
discovery.type: single-node
network.host: 127.0.0.1
action.auto_create_index: false
plugins.security.disabled: true
```
Cette configuration OpenSearch est destinée à configurer un nœud unique. 

#### Paramètres de configuration d’OpenSearch pour Graylog

##### 📘 Explication des paramètres

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

##### 🔧 Conseils de configuration

- Certaines options peuvent déjà exister dans le fichier `opensearch.yml`, mais être commentées avec un `#`.  
  ➤ Il suffit alors de retirer le `#` et de modifier la valeur si nécessaire.

Pour finir Enregistrons et fermons ce fichier.

### C. Configurer Java (JVM)

#### Nous devons configurer Java Virtual Machine utilisé par OpenSearch afin d'ajuster la quantité de mémoire que peut utiliser ce service. Éditons le fichier de configuration suivant :

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

#### 🔍 Vérification du paramètre vm.max_map_count :

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

Enfin, activons le démarrage automatique d'OpenSearch et lançons le service associé.


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

Passons à la prochaine étape : l'installation tant attendue, celle de Graylog !

### D. Installation de Graylog

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

#### 🔧 Configuration préalable de Graylog :

Avant de lancer Graylog, il est nécessaire de modifier certaines options de configuration.

Commençons par définir ces deux paramètres essentiels :

password_secret : cette clé unique et aléatoire est utilisée par Graylog pour sécuriser le stockage des mots de passe utilisateurs, un peu comme une clé de salage (salt).

root_password_sha2 : il s'agit du mot de passe administrateur par défaut, stocké sous forme de hachage SHA-256.

Pour débuter, nous allons générer une clé aléatoire de 96 caractères à utiliser comme valeur pour password_secret.

```bash
pwgen -N 1 -s 96
```

Si `pwgen` n’est pas installé, installons le avec :

```bash
sudo apt install pwgen -y
```

```bash
7p0gEqEgNyyusvPj58H4CU7bOyr7MWKd5gOQFhcLWNwOljOX5DJi0VA2LK4q86HMEipmEbAmc8WMfitHLgKQuY2a0S3jzDm0 (96 caractères)
```

Copions la valeur retournée, puis ouvrons le fichier de configuration de Graylog :

```bash
sudo nano /etc/graylog/server/server.conf
```

Collez la clé au niveau du paramètre password_secret = .

Enregistrez et fermez le fichier.

🔐 Définition du mot de passe administrateur
Vous devez ensuite configurer le mot de passe du compte admin créé par défaut.

Dans le fichier de configuration, il faut stocker le hash du mot de passe, ce qui nécessite de le générer au préalable.

L’exemple ci-dessous montre comment obtenir le hash SHA-256 du mot de passe 'MonMotDePasse'. Pensez à remplacer cette valeur par votre propre mot de passe.

```bash
echo -n "MonMotDePasse" | sha256sum | awk '{print $1}'
```
ex : 

Ex :

```conf
echo -n "S@B85-2025-SID" | sha256sum | awk '{print $1}'
```

Copions la valeur obtenue en sortie (sans le tiret en bout de ligne).

Ouvrons de nouveau le fichier de configuration de Graylog :

```bash
sudo nano /etc/graylog/server/server.conf
```

Collons la valeur au niveau de l'option root_password_sha2 = .

⚙️ Configuration de l'adresse d'écoute HTTP :

Profitez de votre présence dans le fichier de configuration pour définir le paramètre http_bind_address.

Attribuons-lui la valeur 0.0.0.0:9000 afin que l’interface web de Graylog soit accessible sur le port 9000, depuis toutes les adresses IP du serveur.

🔗 Configuration de la connexion à OpenSearch :

Ensuite, configurons l’option elasticsearch_hosts en lui assignant la valeur http://127.0.0.1:9200.

Cela permet de déclarer l’instance locale d’OpenSearch à laquelle Graylog va se connecter. Cette étape est indispensable, notamment parce que nous n’utilisons pas de Graylog Data Node. Sans cette configuration, la suite de l’installation ne pourra pas se poursuivre.

Enregistrons et fermonsle fichier.

Cette commande configure Graylog pour qu’il se lance automatiquement au démarrage du système et démarre immédiatement le service Graylog.

```bash
sudo systemctl enable --now graylog-server
```

Une fois cette étape terminée, ouvrez un navigateur et connectez-vous à Graylog en utilisant l’adresse IP (ou le nom) du serveur, suivi du port 9000.

À titre d’information :

Il n’y a pas si longtemps, lors de la première connexion à Graylog, une fenêtre d’authentification similaire à celle ci-dessous apparaissait. Il fallait alors saisir l’identifiant admin ainsi que le mot de passe associé.

Cependant, il arrivait parfois que la connexion échoue sans raison apparente, ce qui pouvait être source de frustration.

Il fallait alors revenir à la ligne de commande sur le serveur Graylog pour consulter les journaux. Ces derniers indiquaient qu’un mot de passe temporaire, spécifié dans les logs, devait être utilisé lors de la première connexion.

```bash
tail -f /var/log/graylog-server/server.log
```

Il suffisait ensuite de se reconnecter avec l’utilisateur admin et le mot de passe temporaire pour accéder à l’interface.

Aujourd’hui, ce procédé n’est plus nécessaire : il suffit d’utiliser directement le compte admin avec le mot de passe configuré lors de la mise en place en ligne de commande.

### E. Graylog : créer un nouveau compte administrateur

Au lieu d’utiliser le compte admin par défaut fourni avec Graylog, il est recommandé de créer votre propre compte administrateur.

Pour cela, accédez au menu « System », puis sélectionnez « Users and Teams ». Cliquez ensuite sur le bouton « Create user », remplissez le formulaire avec les informations souhaitées, et attribuez à ce compte le rôle administrateur.

---

## IV. Conclusion

Félicitations, vous avez installé Graylog sur une machine Debian 12 ! Vous pouvez maintenant centraliser, indexer et analyser vos logs depuis une interface unique et puissante.

---

**Mise à jour :** Juillet 2025

---

<p align="center">
  <b>🔒 Un guide proposé par <a href="https://github.com/0xCyberLiTech">0xCyberLiTech</a> • Pour des tutoriels accessibles à tous. 🔒</b>
</p>





