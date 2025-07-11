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

# 📘 Procédure d'installation de Graylog 6.3 sur Debian 12 (Bookworm)

## 📑 Sommaire
1. [🛠️ Prérequis](#1-🛠️-prérequis)
2. [📦 Installer MongoDB 7](#2-📦-installer-mongodb-7)  
3. [📦 Installer OpenSearch 2.14](#3-📦-installer-opensearch-214)  
4. [☕ Installer Java 17](#4-☕-installer-java-17)  
5. [📥 Installer Graylog](#5-📥-installer-graylog)  
6. [⚙️ Configurer Graylog](#6-⚙️-configurer-graylog)  
7. [▶️ Démarrer les services](#7-▶️-démarrer-les-services)  
8. [🌐 Accéder à l’interface Graylog](#8-🌐-accéder-à-linterface-graylog)  
9. [📊 Résumé](#9-📊-résumé)  
10. [⚠️ OpenSearch : plugin sécurité & URL indisponible](#10-⚠️-opensearch--plugin-sécurité--url-indisponible)  
11. [🧠 Adapter le Java Heap à la RAM](#11-🧠-adapter-le-java-heap-à-la-ram)  
12. [✅ Finalisation](#12-✅-finalisation)  

---

## 1. 🛠️ Prérequis

- **Debian 12 64‑bit** à jour
- **8 Go de RAM minimum** (16 Go recommandés)
- Ports ouverts :  
  - `27017` → MongoDB  
  - `9200` → OpenSearch  
  - `9000` → Graylog

### 📅 Fuseau horaire & NTP

```bash
sudo timedatectl set-timezone Europe/Paris
```
```bash
sudo apt update && sudo apt install -y ntp
```

### 💤 Désactiver la mise en veille (environnement graphique)

```bash
sudo systemctl mask sleep.target suspend.target hibernate.target hybrid-sleep.target
```

Pour réactiver :

```bash
sudo systemctl unmask sleep.target suspend.target hibernate.target hybrid-sleep.target
```

### 👤 Ajout de l’utilisateur courant au groupe `sudo`

Si vous installez Graylog avec un utilisateur non-root, donnez-lui les droits d’administration :

```bash
sudo adduser "$USER" sudo
```

> Déconnectez-vous / reconnectez-vous pour que l’ajout au groupe soit pris en compte.

---

## 2. 📦 Installer MongoDB 7

```bash
sudo apt update
```
```bash
sudo apt install -y gnupg curl
```
```bash
curl -fsSL https://www.mongodb.org/static/pgp/server-7.0.asc   | sudo gpg -o /usr/share/keyrings/mongodb-server-7.0.gpg --dearmor
```
```bash
echo "deb [signed-by=/usr/share/keyrings/mongodb-server-7.0.gpg] https://repo.mongodb.org/apt/debian bookworm/mongodb-org/7.0 main"   | sudo tee /etc/apt/sources.list.d/mongodb-org-7.0.list
```
```bash
sudo apt update
```
```bash
sudo apt install -y mongodb-org
```
```bash
sudo systemctl enable --now mongod
```

---

## 3. 📦 Installer OpenSearch 2.14

```bash
wget https://artifacts.opensearch.org/releases/bundle/opensearch/2.14.0/opensearch-2.14.0-linux-x64.tar.gz
```
```bash
tar -xvzf opensearch-2.14.0-linux-x64.tar.gz
```
```bash
sudo mv opensearch-2.14.0 /usr/share/opensearch
```
```bash
sudo useradd -r -M -s /usr/sbin/nologin opensearch
```
```bash
sudo chown -R opensearch:opensearch /usr/share/opensearch
```

### 💡 Des modifications vont devoir être effectués :

Recommandation :

Tu es visiblement en train de mettre en place Graylog avec OpenSearch :

➡️ Je recommande de désactiver temporairement le plugin de sécurité (plugins.security.disabled: true) pour valider que tout fonctionne, puis configurer les certificats SSL ensuite si besoin.

Si /etc/opensearch n'existe pas, cela signifie que ton installation d'OpenSearch :

- a été faite via une archive .tar.gz (et non via apt ou yum),
- ou que la configuration est ailleurs (ex: /usr/share/opensearch/config/).

✅ Étapes pour retrouver et modifier opensearch.yml
Localise le fichier opensearch.yml :

```bash
sudo find / -name opensearch.yml 2>/dev/null
```

Tu devrais voir un chemin du type :

```bash
/usr/share/opensearch/config/opensearch.yml
```

Édite ce fichier :

```bash
sudo nano /usr/share/opensearch/config/opensearch.yml
```

Ajoute cette ligne tout en bas pour désactiver la sécurité :

```bash
plugins.security.disabled: true
```

Redémarre OpenSearch :

```bash
sudo systemctl restart opensearch
```

Teste ensuite avec :

```bash
curl http://localhost:9200
```

Tu devrais voir une réponse JSON avec des infos sur OpenSearch.

```bash
{
  "name" : "srv-labo",
  "cluster_name" : "opensearch",
  "cluster_uuid" : "iM-KPxoYRQ-dVvECnHrbzw",
  "version" : {
    "distribution" : "opensearch",
    "number" : "2.14.0",
    "build_type" : "tar",
    "build_hash" : "aaa555453f4713d652b52436874e11ba258d8f03",
    "build_date" : "2024-05-09T18:51:00.973564994Z",
    "build_snapshot" : false,
    "lucene_version" : "9.10.0",
    "minimum_wire_compatibility_version" : "7.10.0",
    "minimum_index_compatibility_version" : "7.0.0"
  },
  "tagline" : "The OpenSearch Project: https://opensearch.org/"
}
```

Parfait ! 🎉 OpenSearch est maintenant en ligne et opérationnel :

- ✅ Réponse valide de curl http://localhost:9200
- ✅ OpenSearch version 2.14.0 active
- ✅ Mode tar confirmé (installation via archive, d'où l'absence de /etc/opensearch)
- ✅ Plus d’erreur de plugin bloquant (plugins.security...)
- ✅ Graylog devrait maintenant pouvoir se connecter à OpenSearch

---

### Créer le service systemd

```bash
sudo tee /etc/systemd/system/opensearch.service <<EOF
[Unit]
Description=OpenSearch
After=network.target

[Service]
User=opensearch
ExecStart=/usr/share/opensearch/bin/opensearch
Restart=always
LimitNOFILE=65536

[Install]
WantedBy=multi-user.target
EOF
```

```bash
sudo systemctl daemon-reload
```
```bash
sudo systemctl enable opensearch
```
```bash
sudo systemctl start opensearch
```

---

## 4. ☕ Installer Java 17

```bash
sudo apt install -y openjdk-17-jre-headless
```

---

## 5. 📥 Installer Graylog

```bash
wget https://packages.graylog2.org/repo/packages/graylog-6.3-repository_latest.deb
```
```bash
sudo dpkg -i graylog-6.3-repository_latest.deb
```
```bash
sudo apt update
```
```bash
sudo apt install -y graylog-server
```

---

## 6. ⚙️ Configurer Graylog

### 🔐 Générer les secrets

```bash
sudo apt install -y pwgen            # Si nécessaire
pwgen -N 1 -s 96                     # → password_secret
echo -n "MonMotDePasse" | sha256sum  # → root_password_sha2
```

### Modifier `/etc/graylog/server/server.conf`

```
password_secret = <clé aléatoire générée>
root_password_sha2 = <hash sha256>
root_timezone = Europe/Paris
web_listen_uri = http://0.0.0.0:9000/api/
elasticsearch_hosts = http://127.0.0.1:9200
```

---

## 7. ▶️ Démarrer les services

```bash
sudo systemctl daemon-reload
```
```bash
sudo systemctl enable --now graylog-server
```

---

## 8. 🌐 Accéder à l’interface Graylog

```
http://<IP_SERVEUR>:9000
```

Identifiants par défaut :  
**admin / MonMotDePasse**

> 🔒 **En production** : activez **HTTPS** !

---

## 9. 📊 Résumé

| Composant          | Port  | Rôle                              |
|--------------------|-------|-----------------------------------|
| MongoDB 7          | 27017 | Base de données Graylog           |
| OpenSearch 2.14    | 9200  | Moteur d’indexation               |
| Graylog 6.3        | 9000  | Interface & API                   |

---

## 10. ⚠️ OpenSearch : plugin sécurité & URL indisponible

### Symptôme

Accès à `http://<IP>:9000` indisponible → souvent dû au plugin de sécurité d’OpenSearch.

### Solution rapide (labo/dev)

1. Trouver puis modifier `opensearch.yml` :

```bash
sudo find / -name opensearch.yml
```
```bash
sudo nano /usr/share/opensearch/config/opensearch.yml
```

---

2. Désactiver la sécurité :

```yaml
plugins.security.disabled: true
```

3. Redémarrer le service :

```bash
sudo systemctl restart opensearch
```
```bash
curl http://localhost:9200
```

> Une réponse JSON valide confirme que OpenSearch fonctionne.

---

## 11. 🧠 Adapter le Java Heap à la RAM

### Règles

- **≤ 32 Go** (sinon perte de Compressed OOPs)
- En pratique : 25 % de la RAM, max 8 Go pour OpenSearch si 16 Go RAM.

### Exemple (RAM = 16 Go)

#### OpenSearch

```bash
sudo nano /usr/share/opensearch/config/jvm.options
```

```
-Xms4g
-Xmx4g
```

#### Graylog

```bash
sudo nano /etc/default/graylog-server
```

```bash
GRAYLOG_SERVER_JAVA_OPTS="-Xms2g -Xmx2g"
```

Redémarrer les services :

```bash
sudo systemctl restart opensearch
```
```bash
sudo systemctl restart graylog-server
```

---

## 12. ✅ Finalisation

### 🔍 Logs

```bash
sudo tail -f /var/log/graylog-server/server.log
```

### 🌐 Accès

- **Labo** : `http://127.0.0.1:9000` ou `http://<IP_LOCAL>:9000`
- **Production** : `https://127.0.0.1:9000` ou `https://<IP_PUBLIC>:9000`







---

🎉 Bon logging ! 🚀

---

**Mise à jour :** Juillet 2025

---

<p align="center">
  <b>🔒 Un guide proposé par <a href="https://github.com/0xCyberLiTech">0xCyberLiTech</a> • Pour des tutoriels accessibles à tous. 🔒</b>
</p>





