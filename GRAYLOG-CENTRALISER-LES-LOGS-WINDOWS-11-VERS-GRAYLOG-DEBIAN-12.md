<div align="center">

  <br></br>
  
  <a href="https://github.com/0xCyberLiTech">
    <img src="https://readme-typing-svg.herokuapp.com?font=JetBrains+Mono&size=50&duration=6000&pause=1000000000&color=FF0048&center=true&vCenter=true&width=1100&lines=%3EGRAYLOG_" alt="Titre dynamique GRAYLOG" />
  </a>
  
  <br></br>
  
  <h2>Laboratoire numérique pour la cybersécurité, Linux & IT</h2>

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

<!--
Optimisation SEO : mots-clés Graylog, 0xCyberLiTech, Linux, sécurité informatique, tutoriels, guides, administration système, scripts Bash, Debian, logs, rsyslog, graylog, ressources techniques, étudiants, professionnels, formation, réseau, IT, bonnes pratiques, passionnés.
-->

<div align="center">
  <img src="https://img.icons8.com/fluency/96/000000/cyber-security.png" alt="CyberSec" width="80"/>
</div>

<div align="center">
  <p>
    <strong>Cybersécurité</strong> <img src="https://img.icons8.com/color/24/000000/lock--v1.png"/> • <strong>Linux Debian</strong> <img src="https://img.icons8.com/color/24/000000/linux.png"/> • <strong>Sécurité informatique</strong> <img src="https://img.icons8.com/color/24/000000/shield-security.png"/>
  </p>
</div>

---

## 🚀 À propos & Objectifs

Ce projet propose des solutions innovantes et accessibles en cybersécurité, avec une approche centrée sur la simplicité d’utilisation et l’efficacité. Il vise à accompagner les utilisateurs dans la protection de leurs données et systèmes, tout en favorisant l’apprentissage et le partage des connaissances.

Le contenu est structuré, accessible et optimisé SEO pour répondre aux besoins de :
- 🎓 Étudiants : approfondir les connaissances
- 👨‍💻 Professionnels IT : outils et pratiques
- 🖥️ Administrateurs système : sécuriser l’infrastructure
- 🛡️ Experts cybersécurité : ressources techniques
- 🚀 Passionnés du numérique : explorer les bonnes pratiques

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

<div align="center">
  <a href="https://github.com/0xCyberLiTech" target="_blank" rel="noopener">
    <img src="https://skillicons.dev/icons?i=linux,debian,bash,docker,nginx,git,vim,python,markdown" alt="Skills" width="440">
  </a>
</div>

<div align="center">
  <b>🔒 Un guide proposé par <a href="https://github.com/0xCyberLiTech">0xCyberLiTech</a> • Pour des tutoriels accessibles à tous. 🔒</b>
</div>
