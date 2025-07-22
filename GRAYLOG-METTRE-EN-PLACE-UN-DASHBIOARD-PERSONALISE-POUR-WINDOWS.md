<div align="center">
<a href="https://github.com/0xCyberLiTech">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&size=32&pause=1000&color=D14A4A&center=true&vCenter=true&width=1000&lines=SUPERVISION+CENTRALISÉE+AVEC+GRAYLOG;Détection+des+menaces+•+Logs+structurés+•+Alertes;Tutoriel+pédagogique+100%+Debian+12" alt="Typing SVG" />
</a>

<p align="center">
  <em>Tuto, mettre en place un dashboard personnalisé pour Windows.</em><br>
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

**Mise à jour :** Juillet 2025

---

<p align="center">
  <b>🔒 Un guide proposé par <a href="https://github.com/0xCyberLiTech">0xCyberLiTech</a> • Pour des tutoriels accessibles à tous. 🔒</b>
</p>
