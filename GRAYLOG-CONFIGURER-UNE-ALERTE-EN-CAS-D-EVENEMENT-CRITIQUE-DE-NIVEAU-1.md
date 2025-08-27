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
Optimisation SEO : mots-clés cybersécurité, Linux, administration système, sécurité informatique, tutoriels, guides, expertise, formation, supervision, Docker, OpenVAS, firewall, proxy, DNS, SSH, Debian, IT, réseau, cryptographie, open source, ressources techniques, étudiants, professionnels, passionnés.
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

<h1 align="center"> 🚧 **Page en cours de développement non finalisée** 🚧</h1>
<h3 align="center"> 🔧 Travail en cours... Merci de revenir plus tard !</h3>

---

## 🚨 Configuration d'une alerte Graylog pour un événement critique de (niveau 1)

## 🔎 Objectif
Configurer une alerte dans Graylog dès qu'un **message critique de niveau 1** est reçu, avec une notification par e-mail ou webhook.

---

## 🛠️ 1. Prérequis

- Un champ `level` ou `severity` doit être présent dans les messages
- Il est recommandé d'utiliser un **stream dédié** pour ces messages
- Configuration du serveur SMTP (si notification par e-mail)

---

## 📒 2. Création d'un Stream (facultatif mais recommandé)

1. Aller dans **Streams > Create Stream**
2. Nom : `Critique Niveau 1`
3. Règle :
   - Field : `level`
   - Match : `1`
4. Coche : `Remove messages from 'All messages' stream`
5. Lancer le stream

---

## 📋 3. Définir l'événement (Event Definition)

Aller dans **Alerts > Event Definitions > Create Event Definition**

### Détails :

- **Title** : `Alerte Critique Niveau 1`
- **Description** : `Détection d'un message de niveau critique (level = 1)`
- **Stream** : Sélectionner le stream configuré (ou "All messages" si filtre direct)
- **Filter** :
```sql
level:1
```
OU
```sql
severity:"critical"
```

### Condition :

- Type : `Filter & Aggregation`
- Search in last : `1 minute`
- Execute every : `1 minute`
- Condition : `Count > 0`

---

## 📧 4. Notifications

### A. Email

1. Aller dans **Alerts > Notifications > Create Notification**
2. Choisir **Email Notification**
3. Configuration SMTP dans `System > Configurations > Email Transport`
4. Exemple de contenu :
   - **To** : `admin@example.com`
   - **Subject** : `[Graylog] Alerte critique niveau 1`
   - **Body** :
```
Alerte critique détectée !
Message : ${message.message}
Niveau : ${message.level}
Source : ${message.source}
```

### B. Webhook (Slack, Discord, API)

- Choisir `HTTP Notification`
- Coller l'URL du webhook
- Corps JSON personnalisable

---

## 🥪 5. Exemple de message déclencheur

```json
{
  "timestamp": "2025-07-22T20:45:00.000Z",
  "message": "Erreur critique dans le module de sécurité",
  "source": "firewall-core",
  "level": 1
}
```

---

## 🧰 6. Astuce : normalisation avec pipeline

Si le champ `level` n'est pas toujours cohérent, utiliser une **rule de pipeline** :

```ruby
rule "normalize_level_critical"
when
  to_string($message.severity) == "critical"
then
  set_field("level", 1);
end
```

---

## 📁 7. Pour aller plus loin

- Ajouter des tags ou des champs supplémentaires lors du traitement pipeline
- Combiner avec une alerte Slack, Microsoft Teams ou Grafana
- Intégrer dans un SIEM plus large (ex: alerting Zabbix ou Grafana)

---

<p align="center">
  <b>🔒 Un guide proposé par <a href="https://github.com/0xCyberLiTech">0xCyberLiTech</a> • Pour des tutoriels accessibles à tous. 🔒</b>
</p>
