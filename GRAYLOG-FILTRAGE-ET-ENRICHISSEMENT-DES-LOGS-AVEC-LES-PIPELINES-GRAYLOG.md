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
# Filtrage et enrichissement des logs avec les Pipelines Graylog

## ✨ Objectif
Configurer des pipelines dans Graylog pour :
- Filtrer les logs entrants (par contenu, source, type, etc.)
- Enrichir les messages avec des champs personnalisés
- Rediriger ou supprimer des messages inutiles

---

## 📆 1. Concepts de base

### ✅ Pipeline
Un ensemble de règles (stages) qui sont appliquées dans l’ordre pour modifier ou filtrer des messages.

### ✅ Rule
Une règle écrite en langage de pipeline Graylog, contenant :
- une **condition** (`when`)
- une ou plusieurs **actions** (`then`)

### ✅ Stage
Une étape dans un pipeline contenant une ou plusieurs règles.

---

## 🛠️ 2. Activer les Pipelines

1. Aller dans **System > Pipelines**
2. Créer un **nouveau pipeline** (`Create pipeline`)
3. Créer les **règles** associées (`Manage rules`)
4. Connecter le pipeline à un ou plusieurs **streams** (`Connect pipeline to stream`)

---

## 🥪 3. Exemple 1 – Supprimer les logs inutiles

### 🎯 Objectif
Supprimer les messages contenant `WindowsUpdateClient`

### 📂 Rule
```ruby
rule "drop_windows_update"
when
  contains(to_string($message.message), "WindowsUpdateClient")
then
  drop_message();
end
```

---

## 🥪 4. Exemple 2 – Ajouter un champ personnalisé selon l’IP source

### 🎯 Objectif
Si l’adresse IP source est dans le réseau interne, ajouter `source_zone: internal`

### 📂 Rule
```ruby
rule "tag_internal_source"
when
  cidr_match("192.168.0.0/16", to_string($message.source))
then
  set_field("source_zone", "internal");
end
```

---

## 🥪 5. Exemple 3 – Extraire un nom d’utilisateur

### 🎯 Objectif
Extraire le nom d'utilisateur d'un message de type :
> "Login attempt failed for user 'admin' from 10.0.0.5"

### 📂 Rule
```ruby
rule "extract_username"
when
  contains(to_string($message.message), "Login attempt")
then
  let username = regex(".+user '([^']+)'", to_string($message.message));
  set_field("username", username["0"]);
end
```

---

## 🥪 6. Exemple 4 – Réécrire ou enrichir un champ

### 🎯 Objectif
Changer `level` de "WARN" en "WARNING"

### 📂 Rule
```ruby
rule "standardize_warn_level"
when
  to_string($message.level) == "WARN"
then
  set_field("level", "WARNING");
end
```

---

## 🔄 7. Connexion à un Stream

Pour appliquer tes règles :

1. Créer un **Stream** (ex: "Logs Applicatifs Windows")
2. Ajouter une **règle de stream** pour filtrer (ex: `source` contient `windows`)
3. Connecter le **pipeline** à ce stream via `Manage Connections`

---

## 🧰 8. Astuces utiles

- Utilise `debug()` pour tester une valeur dans les logs Graylog.
- `drop_message()` supprime le message.
- `remove_field()` supprime un champ inutile.
- Les **pipelines sont chaînables** en plusieurs stages avec priorités.

---

## 📁 9. Références utiles

- [Documentation officielle Graylog - Pipelines](https://docs.graylog.org/docs/pipelines/pipelines)
- [Fonctions de pipeline disponibles](https://docs.graylog.org/docs/pipelines/functions)

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

