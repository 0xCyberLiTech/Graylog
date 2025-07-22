<div align="center">
<a href="https://github.com/0xCyberLiTech">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&size=32&pause=1000&color=D14A4A&center=true&vCenter=true&width=1000&lines=SUPERVISION+CENTRALISÉE+AVEC+GRAYLOG;Détection+des+menaces+•+Logs+structurés+•+Alertes;Tutoriel+pédagogique+100%+Debian+12" alt="Typing SVG" />
</a>

<p align="center">
  <em>Tuto, installation & configurations d'un serveur Graylog sur Debian 12.</em><br>
  <b>📊 Monitoring – 📈 Performance – ⚙️ Fiabilité</b>
</p>

![GitHub release (latest by date)](https://img.shields.io/github/v/release/0xCyberLiTech/Graylog?label=version&logo=github)
[![Changelog](https://img.shields.io/badge/📄%20CHANGELOG-Graylog-blue)](./CHANGELOG.md)


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

### 🧭 **Sommaire :**

---

<div align="center" style="margin-bottom: 10px;">

Légende des couleurs des boutons :

🟢 **Actif** – Dépôt totalement accessible  
🟠 **Partiel** – Dépôt partiellement accessible  
🔴 **Inactif** – Dépôt inaccessible ou indisponible

</div>

---

<div align="center">

| Catégorie | Sujet | Accès Rapide |
|:---:|:---|:---:|
| **Installation** | Installation & configuration de Graylog sur Debian 12.| [<img src="https://img.shields.io/badge/EXPLORER-brightgreen?style=for-the-badge&logo=github&logoColor=white">](GRAYLOG-INSTALLATION-CONFIGURATION-DEBIAN-12.md) |
| **Configuration** | Centraliser les logs de Windows 11 sur Graylog Debian 12.| [<img src="https://img.shields.io/badge/EXPLORER-brightgreen?style=for-the-badge&logo=github&logoColor=white">](GRAYLOG-CENTRALISER-LES-LOGS-WINDOWS-11-VERS-GRAYLOG-DEBIAN-12.md) |
| **Configuration** | Configuration rsyslog + Graylog sur Debian 12 (même serveur).| [<img src="https://img.shields.io/badge/EXPLORER-orange?style=for-the-badge&logo=github&logoColor=white">](GRAYLOG-CONFIGURER-GRAYLOG-POUR-RECEVOIR-LES-LOGS-VIA-SYSLOG-UDP.md) |
| **Configuration** | Optimisation des logs Windows vers Graylog.| [<img src="https://img.shields.io/badge/EXPLORER-red?style=for-the-badge&logo=github&logoColor=white">]() |
| **Configuration** | Filtrage et enrichissement des logs avec les Pipelines Graylog.| [<img src="https://img.shields.io/badge/EXPLORER-red?style=for-the-badge&logo=github&logoColor=white">]() |
| **Configuration** | Configurer une alerte en cas d'événement critique de niveau 1.| [<img src="https://img.shields.io/badge/EXPLORER-red?style=for-the-badge&logo=github&logoColor=white">]() |
| **Configuration** | Mettre en place un dashboard personnalisé pour Windows.| [<img src="https://img.shields.io/badge/EXPLORER-red?style=for-the-badge&logo=github&logoColor=white">]() |
| **Configuration** | Visualiser les connexions entrantes/sortantes d’un pare-feu.| [<img src="https://img.shields.io/badge/EXPLORER-red?style=for-the-badge&logo=github&logoColor=white">]() |

</div>

---

## 🧠 Introduction à Graylog

### Qu'est-ce que Graylog ?

**Graylog** est une solution de gestion centralisée des journaux (*logs*) conçue pour collecter, stocker, analyser et visualiser des données de log provenant de différentes sources du système informatique.

Il est particulièrement utilisé dans les domaines suivants :
- 🔒 **Cybersécurité** : détection d’activités suspectes et d’intrusions.
- 🛠️ **Supervision système** : surveillance de l’état des serveurs, applications et réseaux.
- 📊 **Audit et conformité** : conservation des traces pour répondre à des obligations légales (RGPD, PCI-DSS, etc.).

---

### À quoi sert Graylog concrètement ?

Graylog agit comme un **centre de pilotage des événements** :

- 📥 **Collecte** des logs provenant de : serveurs Linux/Windows, routeurs, pare-feu, applications, etc.
- 🧹 **Normalisation** des données pour les rendre lisibles et exploitables.
- 🔎 **Recherche** rapide grâce à Elasticsearch.
- 📈 **Visualisation** à travers des tableaux de bord personnalisables.
- ⚠️ **Alertes** automatiques en cas d'événements critiques.
- 🗄️ **Archivage** sécurisé des données de log.

---

### Comment ça fonctionne ?

Graylog repose sur plusieurs composants clés :
| Composant       | Rôle                                                                 |
|----------------|----------------------------------------------------------------------|
| **MongoDB**     | Stocke les métadonnées et les configurations de Graylog             |
| **Elasticsearch** | Sert de moteur de recherche pour interroger les logs               |
| **Graylog Server** | Composant principal qui reçoit, traite et affiche les logs        |
| **Interface Web** | Permet à l'utilisateur d'interagir avec les données via un navigateur |

---

### Pourquoi utiliser Graylog ?

- ✅ Interface web moderne, ergonomique et accessible
- 🚀 Capacité à gérer un grand volume de logs
- 🧩 Architecture modulaire et évolutive
- 🔐 Idéal pour la détection d’anomalies, de fuites ou d’attaques
- 💡 Parfait pour les analystes SOC, admins systèmes, DevOps et responsables conformité

---

### Cas d’usage typiques

- Collecter les logs de tous les serveurs d’une infrastructure Linux.
- Superviser les connexions SSH ou les tentatives de brute force.
- Être alerté en cas de crash applicatif ou de saturation CPU/RAM.
- Visualiser les connexions entrantes/sortantes d’un pare-feu.
- Auditer les accès aux services critiques (ex : bases de données).

---

### Conclusion

Graylog est un outil puissant de centralisation et d’analyse des logs, **indispensable dans un contexte de supervision et de cybersécurité**. Il permet de garder le contrôle, d’agir rapidement en cas de problème, et d’assurer la traçabilité de toutes les activités système.

---

**Mise à jour :** Juillet 2025

---

<p align="center">
  <b>🔒 Un guide proposé par <a href="https://github.com/0xCyberLiTech">0xCyberLiTech</a> • Pour des tutoriels accessibles à tous. 🔒</b>
</p>

