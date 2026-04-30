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

<h1 align="center"> 🚧 **Page en cours de développement non finalisée** 🚧</h1>
<h3 align="center"> 🔧 Travail en cours... Merci de revenir plus tard !</h3>

---

## 🔬 Mise en place d'un dashboard personnalisé pour les logs Windows dans Graylog

## 🔎 Objectif
Créer un **dashboard personnalisé Graylog** permettant de visualiser les logs critiques, système, et sécurité des machines Windows, avec des widgets clairs et filtrables.

---

## 🛠️ 1. Prérequis

- Logs Windows collectés via **NXLog**, **Winlogbeat**, ou **Sysmon**
- Données disponibles dans Graylog avec champs structurés (`event_id`, `level`, `source_name`, etc.)

---

## 📒 2. Création du Stream Windows (si besoin)

1. Aller dans **Streams > Create Stream**
2. Nom : `Logs Windows`
3. Exemple de règle :
   - Field : `source`
   - Match regex : `(?i)windows` ou `.*\.domain\.local`
4. Activer le stream

---

## 📅 3. Création du Dashboard

1. Aller dans **Dashboards > Create new dashboard**
2. Nom : `Dashboard Windows`
3. Ajouter une description : "Vue centralisée des événements Windows critiques et système"

---

## 📊 4. Widgets recommandés

### 🔍 A. Volume d'événements critiques
- **Type** : Aggregation
- **Champ** : `level`
- **Filtre** : `level:1 OR severity:"critical"`
- **Group by** : `timestamp (date histogram)`
- **Affichage** : Bar chart ou area chart

### 🔍 B. Top 10 sources les plus bavardes
- **Type** : Aggregation
- **Champ** : `source`
- **Filtre** : `source:*`
- **Group by** : `source`
- **Aggregation** : `count()`
- **Affichage** : Pie chart ou tableau

### 🔍 C. Répartition par Event ID
- **Type** : Aggregation
- **Champ** : `event_id`
- **Filtre** : `source_name:Security`
- **Group by** : `event_id`
- **Objectif** : identifier les événements sécurité récurrents

### 🔍 D. Derniers messages critiques
- **Type** : Messages
- **Filtre** : `level:1 OR severity:"critical"`
- **Colonnes à afficher** : `timestamp`, `message`, `source`, `user`, `event_id`
- **Affichage** : tableau dynamique

### 🔍 E. Utilisateurs liés aux échecs de connexion
- **Type** : Aggregation
- **Filtre** : `event_id:4625`
- **Group by** : `user`
- **Objectif** : lister les utilisateurs ayant généré des erreurs de login

---

## 🔄 5. Astuces pour la personnalisation

- Tu peux **ajouter des paramètres dynamiques** (par source, machine, utilisateur)
- Utilise la **mise en forme conditionnelle** (par ex. rouge si `level=1`)
- Regroupe les widgets par catégorie : Activité Système, Sécurité, Utilisateurs

---

## 📁 6. Export ou partage du dashboard

- Clique sur `Share` pour rendre le dashboard visible à d'autres utilisateurs ou groupes
- Possibilité d'**exporter la configuration en JSON** via l'API REST de Graylog

---

> Ce dashboard est idéal pour surveiller l'activité critique Windows, corrélée aux alertes définies dans les fichiers précédents. Tu peux l'adapter facilement à d'autres OS ou composants en filtrant autrement.

---

<div align="center">

<table>
<tr>
<td align="center"><b>🖥️ Infrastructure &amp; Sécurité</b></td>
<td align="center"><b>💻 Développement &amp; Web</b></td>
<td align="center"><b>🤖 Intelligence Artificielle</b></td>
</tr>
<tr>
<td align="center">
  <a href="https://www.kernel.org/"><img src="https://skillicons.dev/icons?i=linux" width="48" title="Linux" /></a>
  <a href="https://www.debian.org"><img src="https://skillicons.dev/icons?i=debian" width="48" title="Debian" /></a>
  <a href="https://www.gnu.org/software/bash/"><img src="https://skillicons.dev/icons?i=bash" width="48" title="Bash" /></a>
  <br/>
  <a href="https://nginx.org"><img src="https://skillicons.dev/icons?i=nginx" width="48" title="Nginx" /></a>
  <a href="https://www.docker.com"><img src="https://skillicons.dev/icons?i=docker" width="48" title="Docker" /></a>
  <a href="https://git-scm.com"><img src="https://skillicons.dev/icons?i=git" width="48" title="Git" /></a>
</td>
<td align="center">
  <a href="https://www.python.org"><img src="https://skillicons.dev/icons?i=python" width="48" title="Python" /></a>
  <a href="https://flask.palletsprojects.com"><img src="https://skillicons.dev/icons?i=flask" width="48" title="Flask" /></a>
  <a href="https://developer.mozilla.org/docs/Web/HTML"><img src="https://skillicons.dev/icons?i=html" width="48" title="HTML5" /></a>
  <br/>
  <a href="https://developer.mozilla.org/docs/Web/CSS"><img src="https://skillicons.dev/icons?i=css" width="48" title="CSS3" /></a>
  <a href="https://developer.mozilla.org/docs/Web/JavaScript"><img src="https://skillicons.dev/icons?i=js" width="48" title="JavaScript" /></a>
  <a href="https://code.visualstudio.com"><img src="https://skillicons.dev/icons?i=vscode" width="48" title="VS Code" /></a>
</td>
<td align="center">
  <a href="https://pytorch.org"><img src="https://skillicons.dev/icons?i=pytorch" width="48" title="PyTorch" /></a>
  <a href="https://www.tensorflow.org"><img src="https://skillicons.dev/icons?i=tensorflow" width="48" title="TensorFlow" /></a>
  <a href="https://www.raspberrypi.com"><img src="https://skillicons.dev/icons?i=raspberrypi" width="48" title="Raspberry Pi" /></a>
  <br/><br/>
  <a href="https://ollama.com"><img src="https://img.shields.io/badge/Ollama-000000?style=for-the-badge&logo=ollama&logoColor=white" alt="Ollama" /></a>
  &nbsp;
  <a href="https://anthropic.com"><img src="https://img.shields.io/badge/Anthropic-D97757?style=for-the-badge&logo=anthropic&logoColor=white" alt="Anthropic" /></a>
</td>
</tr>
</table>

<br/>

<b>🔒 Un projet proposé par <a href="https://github.com/0xCyberLiTech">0xCyberLiTech</a> • Développé en collaboration avec <a href="https://claude.ai">Claude AI</a> (Anthropic) 🔒</b>

</div>

