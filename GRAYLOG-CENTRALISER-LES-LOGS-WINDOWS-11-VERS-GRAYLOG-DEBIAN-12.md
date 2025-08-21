<div align="center">

  <br></br>
  
  <a href="https://github.com/0xCyberLiTech">
    <img src="https://readme-typing-svg.herokuapp.com?font=JetBrains+Mono&size=50&duration=6000&pause=1000000000&color=FF0048&center=true&vCenter=true&width=1100&lines=%3EGRAYLOG_" alt="Titre dynamique GRAYLOG" />
  </a>
  
  <br></br>
  
  <p align="center">
    <em>Tuto, installation & configuration de NXLog sur Windows 11.</em><br>
    <b>📊 Monitoring – 📈 Performance – ⚙️ Fiabilité</b>
  </p>
  
  [![🔗 Profil GitHub](https://img.shields.io/badge/Profil-GitHub-181717?logo=github&style=flat-square)](https://github.com/0xCyberLiTech)
  [![📦 Dernière version](https://img.shields.io/github/v/release/0xCyberLiTech/Graylog?label=version&style=flat-square&color=blue)](https://github.com/0xCyberLiTech/Graylog/releases/latest)
  [![📄 CHANGELOG](https://img.shields.io/badge/📄%20Changelog-Graylog-blue?style=flat-square)](https://github.com/0xCyberLiTech/Graylog/blob/main/CHANGELOG.md)
  [![📂 Dépôts publics](https://img.shields.io/badge/Dépôts-publics-blue?style=flat-square)](https://github.com/0xCyberLiTech?tab=repositories)
  [![👥 Contributeurs](https://img.shields.io/badge/👥%20Contributeurs-cliquez%20ici-007ec6?style=flat-square)](https://github.com/0xCyberLiTech/Graylog/graphs/contributors)

</div>

---

### 👨‍💻 **À propos de moi.**

> Bienvenue dans mon **laboratoire numérique personnel** dédié à l’apprentissage et à la vulgarisation de la cybersécurité.  
> Passionné par **Linux**, la **cryptographie** et les **systèmes sécurisés**, je partage ici mes notes, expérimentations et fiches pratiques.  
>  
> Pproposer un contenu clair, structuré et accessible pour étudiants, curieux et professionnels de l’IT.  

<p align="center">
  <a href="https://github.com/0xCyberLiTech" target="_blank" rel="noopener">
    <img src="https://skillicons.dev/icons?i=linux,debian,bash,docker,nginx,git,vim" alt="Skills" alt="Logo techno" width="300">
  </a>
</p>

---

### 🎯 **Objectif de ce dépôt.**

> Ce dépôt a pour vocation de centraliser un ensemble de notions clés concernant la journalisation des logs avec Graylog. Il s'adresse aux passionnés, étudiants et professionnels souhaitant mieux comprendre les enjeux de cet équipement de
> sécurité fondamental, apprendre à mettre en place ses configurations efficaces, et se familiariser avec les concepts et bonnes pratiques pour maintenir la performance et la stabilité de leurs systèmes
> d'information face aux menaces externes.

---

# Centraliser les logs de Windows 11 sur Graylog Debian 12.

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

<p align="center">
  <b>🔒 Un guide proposé par <a href="https://github.com/0xCyberLiTech">0xCyberLiTech</a> • Pour des tutoriels accessibles à tous. 🔒</b>
</p>

