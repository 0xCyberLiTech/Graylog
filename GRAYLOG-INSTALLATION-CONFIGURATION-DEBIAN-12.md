<div align="center">
<a href="https://github.com/0xCyberLiTech">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&size=32&pause=1000&color=D14A4A&center=true&vCenter=true&width=700&lines=SUPERVISION+AVEC+GRAYLOG;Installation+•+Sécurité+•+Backup;Tutoriels+pour+Debian+12" alt="Typing SVG" />
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

<h1 align="center"> 🚧 **Page en cours de développement** 🚧</h1>
<h3 align="center"> 🔧 Travail en cours... Merci de revenir plus tard !</h3>

---

# 📘 Procédure d'Installation de Graylog (dernière version stable) sur Debian 12

**Auteur** : CyberLiTech  
**Date** : 2025-07  
**Objectif** : Installer Graylog pas à pas sur Debian 12, avec des explications détaillées.

---

## Prérequis

- Un serveur Debian 12 à jour, accès root ou utilisateur avec `sudo`.
- Connexion internet sur la machine.
- Au moins 4 Go de RAM recommandés.
- Temps estimé : environ 30-45 minutes.

---

## Étape 1 : Mise à jour du système

Avant toute installation, on met à jour la liste des paquets et les paquets installés pour éviter des conflits.

```bash
sudo apt update && sudo apt upgrade -y
```

*Explication* :  
- `apt update` : met à jour la liste des paquets disponibles.  
- `apt upgrade -y` : installe les dernières versions des paquets installés sans demander confirmation.

---

## Étape 2 : Installer Java (OpenJDK 17)

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

## Étape 3 : Installer MongoDB

Graylog utilise MongoDB pour stocker les métadonnées.

### 3.1 Ajouter la clé publique officielle MongoDB

```bash
wget -qO - https://www.mongodb.org/static/pgp/server-6.0.asc | sudo tee /usr/share/keyrings/mongodb-server-6.0.gpg > /dev/null
```

### 3.2 Ajouter le dépôt MongoDB

Créons le fichier `/etc/apt/sources.list.d/mongodb-org-6.0.list` :

```bash
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/mongodb-server-6.0.gpg] https://repo.mongodb.org/apt/debian bookworm/mongodb-org/6.0 main" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list
```

### 3.3 Mettre à jour et installer MongoDB

```bash
sudo apt update
sudo apt install -y mongodb-org
```

### 3.4 Démarrer et activer MongoDB

```bash
sudo systemctl start mongod
sudo systemctl enable mongod
```

### 3.5 Vérifier le statut

```bash
sudo systemctl status mongod
```

Tu dois voir que le service est actif (running).

---

## Étape 4 : Installer Elasticsearch

Graylog utilise Elasticsearch comme moteur de recherche.

### 4.1 Importer la clé Elasticsearch

```bash
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo tee /usr/share/keyrings/elasticsearch-keyring.gpg > /dev/null
```

### 4.2 Ajouter le dépôt Elasticsearch

```bash
echo "deb [signed-by=/usr/share/keyrings/elasticsearch-keyring.gpg] https://artifacts.elastic.co/packages/8.x/apt stable main" | sudo tee /etc/apt/sources.list.d/elastic-8.x.list
```

### 4.3 Mettre à jour et installer Elasticsearch

```bash
sudo apt update
sudo apt install elasticsearch -y
```

### 4.4 Configurer Elasticsearch

Éditer le fichier `/etc/elasticsearch/elasticsearch.yml` :

```bash
sudo nano /etc/elasticsearch/elasticsearch.yml
```

Ajouter ou modifier les lignes suivantes :

```yaml
network.host: 127.0.0.1
http.port: 9200
discovery.type: single-node
```

> *Explication* :  
> - `network.host` définit l'interface réseau écoutée (ici uniquement localhost pour la sécurité).  
> - `discovery.type: single-node` indique que c'est un cluster à un seul nœud.

Sauvegarde et ferme (`Ctrl+O`, `Entrée`, `Ctrl+X`).

### 4.5 Démarrer et activer Elasticsearch

```bash
sudo systemctl daemon-reload
sudo systemctl enable elasticsearch
sudo systemctl start elasticsearch
```

### 4.6 Vérifier qu'Elasticsearch fonctionne

```bash
curl -X GET "localhost:9200"
```

Tu dois obtenir une réponse JSON avec le nom du cluster.

---

## Étape 5 : Installer Graylog

### 5.1 Ajouter la clé et le dépôt Graylog

```bash
wget https://packages.graylog2.org/repo/packages/graylog-5.1-repository_latest.deb
sudo dpkg -i graylog-5.1-repository_latest.deb
sudo apt update
```

### 5.2 Installer Graylog server

```bash
sudo apt install graylog-server -y
```

---

## Étape 6 : Configuration de Graylog

### 6.1 Générer un mot de passe secret (secret key)

Graylog nécessite une clé secrète pour sécuriser les sessions.

```bash
pwgen -N 1 -s 96
```

Si `pwgen` n’est pas installé, installer avec :

```bash
sudo apt install pwgen -y
```

Copie la sortie (une longue chaîne alphanumérique).

### 6.2 Modifier la configuration principale

Ouvre le fichier :

```bash
sudo nano /etc/graylog/server/server.conf
```

Trouve et modifie les paramètres suivants :

- `password_secret` : colle la clé générée plus haut.

```conf
password_secret = <ta_cle_secrete>
```

- `root_password_sha2` : c’est le mot de passe admin (chiffré en SHA-256). Pour le générer :

```bash
echo -n "monmotdepasse" | sha256sum
```

Remplace `monmotdepasse` par ton mot de passe souhaité pour l’utilisateur admin.

Colle la valeur (sans espace) dans la ligne :

```conf
root_password_sha2 = <valeur_sha256>
```

- Vérifie également que la ligne suivante est présente (pour utiliser Elasticsearch en localhost) :

```conf
elasticsearch_hosts = http://127.0.0.1:9200
```

Sauvegarde et quitte.

---

## Étape 7 : Démarrer Graylog

```bash
sudo systemctl daemon-reload
sudo systemctl enable graylog-server
sudo systemctl start graylog-server
```

---

## Étape 8 : Vérifier que Graylog fonctionne

Tu peux regarder les logs :

```bash
sudo journalctl -u graylog-server -f
```

La première ligne importante attendue est :

```
Server running, Graylog web interface is available.
```

---

## Étape 9 : Accéder à l’interface web Graylog

- Ouvre un navigateur web et rends-toi sur :

```
http://<adresse_ip_de_ton_serveur>:9000/
```

- Connecte-toi avec :

  - Login : `admin`
  - Mot de passe : celui que tu as défini (étape 6.2)

---

## Résumé rapide

| Composant      | Port       | Rôle                                      |
|----------------|------------|-------------------------------------------|
| MongoDB        | 27017      | Base de données pour métadonnées          |
| Elasticsearch  | 9200       | Moteur de recherche                        |
| Graylog server | 9000       | Interface web / collecte des logs         |

---

## Conseils supplémentaires

- Si tu veux accéder à Graylog via HTTPS plus tard, tu devras configurer un reverse proxy (ex : Nginx) avec certificat SSL.
- N’hésite pas à consulter la documentation officielle Graylog : https://docs.graylog.org/
- Pour assurer la sécurité, ne laisse pas Elasticsearch ou MongoDB exposés publiquement.

---

## Nettoyage

Tu peux supprimer le paquet du dépôt Graylog si tu le souhaites :

```bash
rm graylog-5.1-repository_latest.deb
```

---

# Fin de la procédure d'installation

---

**Mise à jour :** Juillet 2025

---

<p align="center">
  <b>🔒 Un guide proposé par <a href="https://github.com/0xCyberLiTech">0xCyberLiTech</a> • Pour des tutoriels accessibles à tous. 🔒</b>
</p>





