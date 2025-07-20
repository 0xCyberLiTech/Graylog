<div align="center">
<a href="https://github.com/0xCyberLiTech">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&size=32&pause=1000&color=D14A4A&center=true&vCenter=true&width=1000&lines=SUPERVISION+CENTRALISÉE+AVEC+GRAYLOG;Détection+des+menaces+•+Logs+structurés+•+Alertes;Tutoriel+pédagogique+100%+Debian+12" alt="Typing SVG" />
</a>

<p align="center">
  <em>Tuto, installation & configuration de NXLog sur Windows 11.</em><br>
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

<h1 align="center"> 🚧 **Page en cours de développement non finalisée** 🚧</h1>
<h3 align="center"> 🔧 Travail en cours... Merci de revenir plus tard !</h3>

---

# Centraliser les logs de Windows 11 sur Graylog Debian 12.

---

Pour récupérer les logs de votre PC Windows 11 sur votre instance Graylog installée sur Debian 12, vous devez configurer un agent sur Windows qui envoie les logs à Graylog. 

Le plus utilisé est NXLog. 

Voici une procédure claire avec NXLog, car il est simple à configurer pour envoyer les journaux au format GELF (le format natif de Graylog).

✅ Étapes pour envoyer les logs de Windows 11 vers Graylog avec NXLog

---

## 🔧 1. Installer NXLog sur Windows 11

Télécharger NXLog Community Edition depuis :

👉 https://nxlog.co/products/nxlog-community-edition/download

Installer NXLog en suivant l’assistant.

Par défaut, NXLog est installé dans :

C:\Program Files\nxlog

---

## ⚙️ 2. Configurer NXLog pour envoyer les logs à Graylog :

Éditez le fichier :

C:\Program Files\nxlog\conf\nxlog.conf

🔒 Ouvrir avec un éditeur en mode administrateur (ex : Notepad++).

Voici un exemple de configuration minimale au format GELF UDP :

```
define ROOT C:\Program Files\nxlog
Moduledir %ROOT%\modules
CacheDir %ROOT%\data
Pidfile %ROOT%\data\nxlog.pid
SpoolDir %ROOT%\data
LogFile %ROOT%\data\nxlog.log

<Extension gelf>
    Module xm_gelf
</Extension>

<Input in>
    Module im_msvistalog
</Input>

<Output out>
    Module om_udp
    Host <IP_GRAYLOG_DEBIAN>
    Port 12201
    OutputType GELF
</Output>

<Route 1>
    Path in => out
</Route>

```

🔁 Remplacez Host <IP_GRAYLOG_DEBIAN> par l’adresse IP de votre machine Debian (où Graylog est installé).

---

## 🔁 3. Redémarrer le service NXLog.

Ouvrez une invite de commande en mode administrateur et tapez :

```
net stop nxlog
net start nxlog
```

---

## 🟢 4. Côté Graylog : configurer l’entrée GELF UDP.

### 🛠️ Création d'une entrée GELF UDP sur Graylog

1. **Connectez-vous** à l'interface Web de Graylog.
2. Allez dans le menu **System → Inputs**.
3. Dans **Select input**, choisissez **GELF UDP**.
4. Cliquez sur **Launch new input**.
5. Remplissez les champs suivants :
   - **Nom** : par exemple `Logs Windows`
   - **Bind address** : `0.0.0.0` *(ou l’adresse IP de votre serveur Debian)*
   - **Port** : `12201`
   - Laissez les autres paramètres par défaut.
6. Cliquez sur **Launch** pour activer l’entrée.

---

## ✅ 5. Vérifier la réception des logs.

### -1). Allez dans Search (Recherche) dans Graylog.
### -2). Vous devriez voir apparaître des logs provenant de votre machine Windows.

🔍 Astuce : cherchez par source:nom-de-votre-pc-windows pour filtrer.

📁 Exemples de logs que vous recevrez :

- Événements du journal système
- Échecs/succès de connexion
- Erreurs d'application
- Activité réseau si configurée

---

**Mise à jour :** Juillet 2025

---

<p align="center">
  <b>🔒 Un guide proposé par <a href="https://github.com/0xCyberLiTech">0xCyberLiTech</a> • Pour des tutoriels accessibles à tous. 🔒</b>
</p>

