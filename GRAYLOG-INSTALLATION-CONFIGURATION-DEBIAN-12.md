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

## 📘 Installation Graylog stable sur Debian 12.

**Auteur** : CyberLiTech  
**Date** : 2025-07  
**Objectif** : Installer Graylog pas à pas sur Debian 12, avec des explications détaillées.

---

### Prérequis

- Un serveur Debian 12 à jour, accès root ou utilisateur avec `sudo`.
- Connexion internet sur la machine.
- Au moins 4 Go de RAM recommandés.
- Temps estimé : environ 30-45 minutes.

---

### Étape 1 : Installer sudo si ce n'est pas déja fait :

### Rappel sur la commande  `sudo` :

- sudo (superuser do) permet d’exécuter une commande avec les privilèges administrateur (root) sans se connecter en root.

- C’est utile pour les opérations qui nécessitent des droits élevés, comme l’installation de logiciels, la modification de fichiers système, etc.

- Par défaut, la plupart des distributions Linux l’ont installé, mais il peut arriver qu’il manque sur certaines installations minimales.

Se connecter en root :

```bash
su -
```

Mettre à jour la liste des paquets (optionnel mais recommandé) :

```bash
apt update
```

Installer sudo :

```bash
apt install sudo
```

Ajouter votre utilisateur au groupe sudo (remplacez votre_utilisateur par votre nom d’utilisateur) :

```bash
usermod -aG sudo votre_utilisateur
```

Se déconnecter puis se reconnecter pour que les changements prennent effet.

Avant toute installation, on met à jour la liste des paquets et les paquets installés pour éviter des conflits.

```bash
sudo apt update && sudo apt upgrade -y
```

---

### Étape 2 : Installer Java (OpenJDK 17)

Graylog nécessite Java 17 (OpenJDK). Debian 12 le propose en paquet officiel.

```bash
sudo apt install openjdk-17-jre-headless -y
```

*Vérification* :

```bash
java -version
```

Tu dois obtenir quelque chose comme :

```
openjdk version "17.0.x" 202x-xx-xx
```

---

### Étape 3 : Installer MongoDB

Graylog utilise MongoDB pour stocker les métadonnées.

#### 3.1 Paquets de base

```bash
sudo apt-get install -y gnupg curl
```

#### 3.2 Clé GPG officielle MongoDB 8.0

```bash
curl -fsSL https://www.mongodb.org/static/pgp/server-8.0.asc \
  | sudo gpg --dearmor -o /usr/share/keyrings/mongodb-server-8.0.gpg
```

#### 3.3 Dépôt pour Debian 12 (bookworm).

```bash
echo "deb [signed-by=/usr/share/keyrings/mongodb-server-8.0.gpg] \
  http://repo.mongodb.org/apt/debian bookworm/mongodb-org/8.0 main" \
  | sudo tee /etc/apt/sources.list.d/mongodb-org-8.0.list
```

#### 3.4 Mise à jour de l’index et installation.

```bash
sudo apt-get update
```

```bash
sudo apt-get install -y mongodb-org
```

#### 3.5 Lancer et activer le service.

```bash
sudo systemctl enable --now mongod
```

#### 3.6 Redémarrer le service mongod.

```bash
sudo systemctl restart mongod
```

#### 3.7 Vérification du statut

Vérification :

mongod --version

```bash
db version v8.0.11
Build Info: {
    "version": "8.0.11",
    "gitVersion": "bed99f699da6cb2b74262aa6d473446c41476643",
    "openSSLVersion": "OpenSSL 3.0.16 11 Feb 2025",
    "modules": [],
    "allocator": "tcmalloc-google",
    "environment": {
        "distmod": "debian12",
        "distarch": "x86_64",
        "target_arch": "x86_64"
    }
}
```

### Étape 4 : Installer Elasticsearch

Graylog utilise Elasticsearch comme moteur de recherche.

#### 4.1 Importer la clé Elasticsearch

```bash
curl -fsSL https://artifacts.elastic.co/GPG-KEY-elasticsearch | \
  gpg --dearmor | sudo tee /usr/share/keyrings/elasticsearch-keyring.gpg > /dev/null
```
#### 4.2 Ajouter le dépôt Elasticsearch

```bash
echo "deb [signed-by=/usr/share/keyrings/elasticsearch-keyring.gpg] https://artifacts.elastic.co/packages/8.x/apt stable main" | sudo tee /etc/apt/sources.list.d/elastic-8.x.list
```

#### 4.3 Mettre à jour et installer Elasticsearch

```bash
sudo apt update
sudo apt install elasticsearch -y
```

#### 4.4 Configurer Elasticsearch

Éditer le fichier `/etc/elasticsearch/elasticsearch.yml` :

```bash
sudo nano /etc/elasticsearch/elasticsearch.yml
```

Dans le fichier /etc/elasticsearch/elasticsearch.yml, tu dois ajouter ou modifier ces lignes précisément pour que la configuration soit correcte.

Concrètement :

Si ces lignes n’existent pas encore dans le fichier, tu les ajoutes à la fin du fichier.

Si elles existent déjà, il faut les retrouver et les modifier pour qu'elles correspondent exactement à :

```yaml
network.host: 127.0.0.1
http.port: 9200
discovery.type: single-node
```

> *Explication* :  
> - `network.host` définit l'interface réseau écoutée (ici uniquement localhost pour la sécurité).  
> - `discovery.type: single-node` indique que c'est un cluster à un seul nœud.

Sauvegarde et ferme (`Ctrl+O`, `Entrée`, `Ctrl+X`).

Ces réglages permettent à Elasticsearch de fonctionner en mode "single-node" (pas de cluster multi-nœuds), d’écouter uniquement sur l’interface locale (localhost) pour des raisons de sécurité, et d’utiliser le port 9200 par défaut.

#### 4.5 Démarrer et activer Elasticsearch

```bash
sudo systemctl daemon-reload
sudo systemctl enable elasticsearch
sudo systemctl start elasticsearch
```

#### 4.6 Vérifier qu'Elasticsearch fonctionne

```bash
curl -X GET "localhost:9200"
```

Tu dois obtenir une réponse JSON avec le nom du cluster.

Ce que tu dois voir si tout est OK :

Une réponse en JSON qui ressemble à ça (exemple simplifié) :

```bash
{
  "name" : "nom-de-ton-serveur",
  "cluster_name" : "elasticsearch",
  "cluster_uuid" : "un-identifiant-unique",
  "version" : {
    "number" : "8.x.x",
    "build_flavor" : "default",
    "build_type" : "deb",
    "build_hash" : "...",
    "build_date" : "...",
    "build_snapshot" : false,
    "lucene_version" : "...",
    "minimum_wire_compatibility_version" : "...",
    "minimum_index_compatibility_version" : "..."
  },
  "tagline" : "You Know, for Search"
}
```

---

### Étape 5 : Installer Graylog

#### 5.1 Ajouter la clé et le dépôt Graylog

```bash
wget https://packages.graylog2.org/repo/packages/graylog-5.1-repository_latest.deb
sudo dpkg -i graylog-5.1-repository_latest.deb
sudo apt update
```

#### 5.2 Installer Graylog server

```bash
sudo apt install graylog-server -y
```

---

### Étape 6 : Configuration de Graylog

#### 6.1 Générer un mot de passe secret (secret key)

Graylog nécessite une clé secrète pour sécuriser les sessions.

```bash
pwgen -N 1 -s 96
```

Si `pwgen` n’est pas installé, installer avec :

```bash
sudo apt install pwgen -y
```

Relance la commande `pwgen` :

```bash
pwgen -N 1 -s 96
```

Par exemple, cela va te donner un résultat comme :

```bash
7p0gEqEgNyyusvPj58H4CU7bOyr7MWKd5gOQFhcLWNwOljOX5DJi0VA2LK4q86HMEipmEbAmc8WMfitHLgKQuY2a0S3jzDm0 (96 caractères)
```

Copie la sortie (une longue chaîne alphanumérique), tu en auras besoin après.

#### 6.2 Modifier la configuration principale

Ouvre le fichier :

```bash
sudo nano /etc/graylog/server/server.conf
```

Trouve et modifie les paramètres suivants :

- `password_secret` : colle la clé générée plus haut avec `pwgen -N 1 -s 96`.

```conf
password_secret = <ta_cle_secrete>
```

- `root_password_sha2` : c’est le mot de passe admin (chiffré en SHA-256).

Pour créer le mot de passe de l’utilisateur admin :

Tape la commande suivante pour hasher ton mot de passe admin (remplace "MonMotDePasse" par celui que tu veux utiliser) :

```conf
echo -n "MonMotDePasse" | sha256sum | awk '{print $1}'
```

Ex :

```conf
echo -n "S@B85-2025-SID" | sha256sum | awk '{print $1}'
```

Colle la valeur (sans espace) dans la ligne :

```conf
root_password_sha2 = <valeur_sha256>
```

#### 6.3 Autres variables importantes à vérifier dans server.conf `/etc/graylog/server/server.conf` :

##### 6.31 - `root_timezone` : Définit le fuseau horaire utilisé par Graylog.  

Exemple :  

```conf
root_timezone = Europe/Paris
```

##### 6.32 - `http_publish_uri` : URL sur laquelle l’API web Graylog écoute.

Exemple : 

```
http_bind_address = 0.0.0.0:9000
http_publish_uri = http://<IP_locale>:9000/
```
📌 Détails importants :

🔹 http_bind_address
Indique l’interface réseau et le port sur lesquels Graylog écoute.

0.0.0.0:9000 signifie toutes les interfaces disponibles, sur le port 9000.

🔹 http_publish_uri
C’est l’URL publique utilisée par Graylog pour générer des liens dans l’interface web (notifications, API, etc.).

Tu dois mettre ici l’adresse IP locale de ton serveur ou son nom DNS si applicable.

Cette configuration permet à Graylog d’écouter sur toutes les interfaces réseau (utile pour accès distant).

Exemple final recommandé :

```
http_bind_address = 0.0.0.0:9000
http_publish_uri = http://192.168.1.100:9000/
```

##### 6.33 - `elasticsearch_hosts` : Adresse(s) du(des) serveur(s) Elasticsearch.

Exemple :

```
elasticsearch_hosts = http://127.0.0.1:9200
```

Par défaut, Graylog se connecte à Elasticsearch local.

N’oublie pas de sauvegarder et redémarrer Graylog après modification.

---

### Étape 7 : Démarrer Graylog

```bash
sudo systemctl daemon-reload
sudo systemctl enable graylog-server
sudo systemctl start graylog-server
```

---

### Étape 8 : Vérifier que Graylog fonctionne

Tu peux regarder les logs :

```bash
sudo journalctl -u graylog-server -f
```

La première ligne importante attendue est :

```
Server running, Graylog web interface is available.
```

---

### Étape 9 : Accéder à l’interface web Graylog

- Ouvre un navigateur web et rends-toi sur :

```
http://<adresse_ip_de_ton_serveur>:9000/
```

- Connecte-toi avec :

  - Login : `admin`
  - Mot de passe : celui que tu as défini (étape 6.2)

---

### Résumé rapide

| Composant      | Port       | Rôle                                      |
|----------------|------------|-------------------------------------------|
| MongoDB        | 27017      | Base de données pour métadonnées          |
| Elasticsearch  | 9200       | Moteur de recherche                        |
| Graylog server | 9000       | Interface web / collecte des logs         |

---

### Conseils supplémentaires

- Si tu veux accéder à Graylog via HTTPS plus tard, tu devras configurer un reverse proxy (ex : Nginx) avec certificat SSL.
- N’hésite pas à consulter la documentation officielle Graylog : https://docs.graylog.org/
- Pour assurer la sécurité, ne laisse pas Elasticsearch ou MongoDB exposés publiquement.

---

### Nettoyage

Tu peux supprimer le paquet du dépôt Graylog si tu le souhaites :

```bash
rm graylog-5.1-repository_latest.deb
```

---

## Fin de la procédure d'installation

---

**Mise à jour :** Juillet 2025

---

<p align="center">
  <b>🔒 Un guide proposé par <a href="https://github.com/0xCyberLiTech">0xCyberLiTech</a> • Pour des tutoriels accessibles à tous. 🔒</b>
</p>





