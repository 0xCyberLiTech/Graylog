<div align="center">

  <br></br>
  
  <a href="https://github.com/0xCyberLiTech">
    <img src="https://readme-typing-svg.herokuapp.com?font=JetBrains+Mono&size=50&duration=6000&pause=1000000000&color=FF0048&center=true&vCenter=true&width=1100&lines=%3EGRAYLOG_" alt="Titre dynamique GRAYLOG" />
  </a>
  
  <br></br>
  
  <p align="center">
    <em>Filtrage & enrichissement avec Pipelines.</em><br>
    <b>📊 Monitoring – 📈 Performance – ⚙️ Fiabilité</b>
  </p>
  
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

---

### 👨‍💻 **À propos de moi**

> Bienvenue sur le dépôt <strong>0xCyberLiTech</strong>, votre laboratoire numérique pour l'<strong>apprentissage</strong> et la <strong>vulgarisation</strong> de la <strong>cybersécurité</strong>, de l'<strong>administration Linux Debian</strong> et de la <strong>sécurité informatique</strong>.
> Passionné par <strong>Linux</strong>, la <strong>cryptographie</strong>, la <strong>supervision réseau</strong> et les <strong>systèmes sécurisés</strong>, je partage ici des <strong>tutoriels</strong>, <strong>guides pratiques</strong>, <strong>fiches techniques</strong> et <strong>retours d'expérience</strong> pour renforcer vos compétences IT.
>
> 🎯 <strong>Objectif :</strong> Offrir un contenu structuré, accessible et optimisé pour le référencement naturel, destiné aux étudiants, professionnels, administrateurs système, experts en sécurité et curieux du monde numérique.

<p align="center">
  <a href="https://github.com/0xCyberLiTech" target="_blank" rel="noopener">
    <img src="https://skillicons.dev/icons?i=linux,debian,bash,docker,nginx,git,vim,python,markdown" alt="Skills" width="420">
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

<p align="center">
  <b>🔒 Un guide proposé par <a href="https://github.com/0xCyberLiTech">0xCyberLiTech</a> • Pour des tutoriels accessibles à tous. 🔒</b>
</p>
