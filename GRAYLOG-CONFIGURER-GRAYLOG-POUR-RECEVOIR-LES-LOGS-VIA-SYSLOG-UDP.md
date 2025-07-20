<div align="center">
<a href="https://github.com/0xCyberLiTech">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&size=32&pause=1000&color=D14A4A&center=true&vCenter=true&width=1000&lines=SUPERVISION+CENTRALISÉE+AVEC+GRAYLOG;Détection+des+menaces+•+Logs+structurés+•+Alertes;Tutoriel+pédagogique+100%+Debian+12" alt="Typing SVG" />
</a>

<p align="center">
  <em>Tuto, Configuration rsyslog + Graylog sur Debian 12 (même serveur).</em><br>
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

# Configuration rsyslog + Graylog sur Debian 12 (même serveur).

## Objectif :

Envoyer les logs système de Debian 12 vers Graylog installé localement, en utilisant rsyslog et une entrée Syslog UDP.

---

## 1. Créer une entrée Syslog UDP dans Graylog

1. Connectez-vous à l'interface Web Graylog.  
2. Allez dans **System → Inputs**.  
3. Sélectionnez **Syslog UDP**.  
4. Cliquez sur **Launch new input**.  
5. Configurez :  
   - **Bind address** : `127.0.0.1`  
   - **Port** : `5140`  
   - Laissez les autres paramètres par défaut.  
6. Cliquez sur **Launch**.

---

## 2. Configurer rsyslog pour envoyer les logs à Graylog localement

1. Créez ou éditez le fichier :  
   `/etc/rsyslog.d/90-graylog.conf`

2. Ajoutez la ligne suivante pour envoyer tous les logs vers Graylog via UDP :

    ```
    *.* @127.0.0.1:5140
    ```

> Le `@` indique que la transmission utilise UDP.

3. Sauvegardez et fermez le fichier.

---

## 3. Redémarrer rsyslog

```bash
sudo systemctl restart rsyslog
```

---

## 4. Vérifier la réception des logs dans Graylog

- Dans Graylog, allez dans **Search**.  
- Vous devriez voir les logs système envoyés depuis Debian.  
- Filtrez éventuellement par `source:127.0.0.1` ou hostname local.

---

## Remarques

- Le port `5140` est utilisé car le port `514` nécessite des droits root.  
- Pour une transmission plus fiable, vous pouvez utiliser TCP (`@@127.0.0.1:5140`) à la place d’UDP.  
- Cette configuration fonctionne uniquement sur le même serveur (localhost).

---

**Mise à jour :** Juillet 2025

---

<p align="center">
  <b>🔒 Un guide proposé par <a href="https://github.com/0xCyberLiTech">0xCyberLiTech</a> • Pour des tutoriels accessibles à tous. 🔒</b>
</p>


