<div align="center">
<a href="https://github.com/0xCyberLiTech">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&size=32&pause=1000&color=D14A4A&center=true&vCenter=true&width=1000&lines=SUPERVISION+CENTRALISÉE+AVEC+GRAYLOG;Détection+des+menaces+•+Logs+structurés+•+Alertes;Tutoriel+pédagogique+100%+Debian+12" alt="Typing SVG" />
</a>

<p align="center">
  <em>Tuto, configurer une alerte en cas d'événement critique de niveau 1.</em><br>
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
> 🎯 **Objectif :** proposer un contenu clair, structuré et accessible pour étudiants, curieux et professionnels de l’IT.  
> 🔗 [Mon GitHub principal](https://github.com/0xCyberLiTech)

<p align="center">
  <a href="https://skillicons.dev">
    <img src="https://skillicons.dev/icons?i=linux,debian,bash,docker,nginx,git,vim" alt="Skills" />
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

**Mise à jour :** Juillet 2025

---

<p align="center">
  <b>🔒 Un guide proposé par <a href="https://github.com/0xCyberLiTech">0xCyberLiTech</a> • Pour des tutoriels accessibles à tous. 🔒</b>
</p>
