<div align="center">
<a href="https://github.com/0xCyberLiTech">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&size=32&pause=1000&color=D14A4A&center=true&vCenter=true&width=1000&lines=SUPERVISION+CENTRALISÉE+AVEC+GRAYLOG;Détection+des+menaces+•+Logs+structurés+•+Alertes;Tutoriel+pédagogique+100%+Debian+12" alt="Typing SVG" />
</a>

<p align="center">
  <em>Tuto, optimisation des logs Windows vers Graylog.</em><br>
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

# 🎯 Optimisation de l’envoi de logs Windows vers Graylog

## 📝 Objectif

Limiter les logs envoyés par NXLog au strict nécessaire afin de :

- Réduire la consommation de bande passante
- Éviter la saturation du disque sur le serveur Graylog
- Conserver uniquement les événements critiques ou utiles

---

## 🖥️ 1. Côté Windows – Configuration de NXLog

### ✅ Étapes

1. Installer [NXLog Community Edition](https://nxlog.co/products/nxlog-community-edition/download)
2. Remplacer le fichier `nxlog.conf` par la configuration ci-dessous
3. Redémarrer le service `nxlog` (`services.msc` ou PowerShell)

### ⚙️ Fichier `nxlog.conf` optimisé

```ini
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
    Query <QueryList>
        <Query Id="0">
            <!-- Journaux de sécurité : erreurs et critiques -->
            <Select Path="Security">*[System[(Level=1 or Level=2)]]</Select>
            <!-- Journaux système : erreurs et critiques -->
            <Select Path="System">*[System[(Level=1 or Level=2)]]</Select>
            <!-- Journaux applicatifs : uniquement les erreurs -->
            <Select Path="Application">*[System[(Level=1 or Level=2)]]</Select>
        </Query>
    </Query>
</Input>

<Output out>
    Module om_udp
    Host <IP_DE_TON_GRAYLOG>
    Port 12201
    OutputType GELF
</Output>

<Route r>
    Path in => out
</Route>
```

> 💡 N'oublie pas de remplacer `<IP_DE_TON_GRAYLOG>` par l'adresse IP de ton serveur Graylog.

### 📌 Niveaux d’événements Windows

| Niveau | Signification     |
|--------|-------------------|
| 1      | Critical          |
| 2      | Error             |
| 3      | Warning           |
| 4      | Information (ignoré ici) |
| 5      | Verbose (ignoré ici)     |

---

## 🧱 2. Côté serveur – Configuration de Graylog

### 📦 A. Créer une entrée GELF UDP (si non déjà existante)

1. Accéder à l’interface Graylog
2. Aller dans **System > Inputs**
3. Sélectionner `GELF UDP` → Lancer une nouvelle entrée
4. Port par défaut : `12201`
5. Lier à l’adresse `0.0.0.0` ou à une IP spécifique

---

### 🔁 B. Configurer la rotation des index

1. Menu : **System > Indices**
2. Sélectionner `Default index set` ou ton index personnalisé
3. **Index rotation strategy** :
   - Type : `Index Size` ou `Message Count`
   - Exemple : 2 GB maximum par index
4. **Max number of indices** : par exemple `5` ou `10`
5. **Index retention strategy** : `Delete` (supprime les anciens automatiquement)

| Option                        | Recommandation               |
|------------------------------|------------------------------|
| Rotation par taille          | 2 Go                         |
| Nombre d’index conservés     | 5 (donc max 10 Go)           |
| Stratégie de rétention       | Supprimer les anciens index |

---

## 🔄 Optionnel : Passer en TCP + compression

Pour activer la compression entre NXLog et Graylog :

1. Côté NXLog :

```ini
<Output out>
    Module om_tcp
    Host <IP_DE_TON_GRAYLOG>
    Port 12201
    OutputType GELF
</Output>
```

2. Côté Graylog :
   - Créer une **entrée GELF TCP** dans `System > Inputs`
   - Port : `12201` (ou un autre dédié)

> 🔐 Avantage : fiabilité + possibilité de compression
>  
> 📉 Inconvénient : plus de configuration + besoin de sécuriser le canal (SSL/TLS recommandé)

---

## ✅ Résultat attendu

- Seuls les logs **critiques et erreurs** sont envoyés
- Réduction de la **bande passante**
- Moindre **consommation d’espace disque**
- Journaux utiles pour la sécurité ou le diagnostic uniquement

---

Fichier nxlog.conf en version prête à copier :

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
    Query <QueryList>
        <Query Id="0">
            <!-- Journaux de sécurité : erreurs et critiques -->
            <Select Path="Security">*[System[(Level=1 or Level=2)]]</Select>
            <!-- Journaux système : erreurs et critiques -->
            <Select Path="System">*[System[(Level=1 or Level=2)]]</Select>
            <!-- Journaux applicatifs : uniquement les erreurs -->
            <Select Path="Application">*[System[(Level=1 or Level=2)]]</Select>
        </Query>
    </Query>
</Input>

<Output out>
    Module om_udp
    Host <IP_DE_TON_GRAYLOG>
    Port 12201
    OutputType GELF
</Output>

<Route r>
    Path in => out
</Route>
```

---

## 🧩 Pour aller plus loin

- Ajouter un **pipeline Graylog** pour enrichir/filtrer davantage les logs
- Configurer une **alerte** en cas d’événement critique (niveau 1)
- Mettre en place un **dashboard** personnalisé pour Windows

---

🛠 Maintenu par [TonNom ou @GitHubID] — basé sur un déploiement Graylog 6.x sur Debian 12

---

**Mise à jour :** Juillet 2025

---

<p align="center">
  <b>🔒 Un guide proposé par <a href="https://github.com/0xCyberLiTech">0xCyberLiTech</a> • Pour des tutoriels accessibles à tous. 🔒</b>
</p>



