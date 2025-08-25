<div align="center">

  <br></br>
  
  <a href="https://github.com/0xCyberLiTech">
    <img src="https://readme-typing-svg.herokuapp.com?font=JetBrains+Mono&size=50&duration=6000&pause=1000000000&color=FF0048&center=true&vCenter=true&width=1100&lines=%3EGRAYLOG_" alt="Titre dynamique GRAYLOG" />
  </a>
  
  <br></br>
  
  <p align="center">
    <em>Optimisation des logs Windows vers Graylog.</em><br>
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

# Tutoriel : Envoi optimisé de logs Windows vers Graylog avec NXLog

## 🧹 Objectif

Configurer NXLog sur une machine Windows pour :

- Collecter efficacement les logs (système, sécurité, application)
- Les formater proprement (JSON / GELF)
- Les envoyer vers Graylog en UDP, TCP ou TLS

---

## 📉 Prérequis

- Poste Windows (client ou serveur)
- Serveur Graylog fonctionnel avec une entrée GELF ou Syslog
- NXLog Community Edition : [https://nxlog.co/products/nxlog-community-edition/download](https://nxlog.co/products/nxlog-community-edition/download)

---

## 📁 1. Installation de NXLog

1. Télécharger NXLog Community Edition
2. Lancer l’installation sur le poste Windows
3. Fichier de configuration : `C:\Program Files\nxlog\conf\nxlog.conf`

---

## 🔠 2. Architecture NXLog (rappel)

```
+-------------+      +------------+     +-------------+
|   Input     | ==>  | Processor  | ==> |   Output     |
+-------------+      +------------+     +-------------+
```

---

## 📦 3. Configuration d’une entrée GELF dans Graylog

1. Aller dans **System > Inputs**
2. Ajouter une entrée **GELF UDP** ou **GELF TCP**
3. Choisir le port (ex : 12201)
4. Démarrer l’entrée

---

## ⚙️ 4. Exemple de configuration NXLog (GELF vers Graylog)

```conf
define ROOT C:\Program Files\nxlog
Moduledir %ROOT%\modules
CacheDir %ROOT%\data
Pidfile %ROOT%\data\nxlog.pid
SpoolDir %ROOT%\data
LogFile %ROOT%\data\nxlog.log

<Extension _gelf>
    Module      xm_gelf
</Extension>

<Extension _json>
    Module      xm_json
</Extension>

<Input in_eventlog>
    Module      im_msvistalog
    Query       <QueryList>
                    <Query Id="0">
                        <Select Path="Application">*</Select>
                        <Select Path="System">*</Select>
                        <Select Path="Security">*</Select>
                    </Query>
                </QueryList>
</Input>

<Output out_graylog>
    Module      om_udp
    Host        192.168.1.100     # IP Graylog
    Port        12201             # Port GELF UDP
    OutputType  GELF_UDP
</Output>

<Route route_all>
    Path        in_eventlog => out_graylog
</Route>
```

---

## 🔍 5. Filtres personnalisés (optionnels)

### ✅ Exemple : logs de niveau « Erreur » uniquement

```conf
<Input in_eventlog>
    Module      im_msvistalog
    Query       <QueryList>
                    <Query Id="0">
                        <Select Path="System">
                            *[System[(Level=1 or Level=2 or Level=3)]]
                        </Select>
                    </Query>
                </QueryList>
</Input>
```

---

## 🔒 6. Champs personnalisés

```conf
<Output out_graylog>
    Module      om_udp
    Host        192.168.1.100
    Port        12201
    OutputType  GELF_UDP
    Exec        $Hostname = hostname();
                $custom_field = 'poste_windows_marc';
</Output>
```

---

## 📊 7. Visualisation dans Graylog

- Aller dans **Search**
- Rechercher : `_source:poste_windows_marc`
- Créer un dashboard à partir des champs désirés

---

## ⚒️ 8. Redémarrer NXLog

```bat
net stop nxlog
net start nxlog
```

---

## 🚧 9. Dépannage

| Problème                 | Solution                                         |
| ------------------------ | ------------------------------------------------ |
| NXLog ne démarre pas     | Lire `nxlog.log` dans le dossier `data`          |
| Pas de logs dans Graylog | Vérifier IP / port de l'entrée                   |
| Champs manquants         | S'assurer que `OutputType GELF` est bien utilisé |

---

## 🔐 10. Envoi sécurisé (TLS)

```conf
<Output out_graylog_tls>
    Module      om_tcp
    Host        192.168.1.100
    Port        12202
    OutputType  GELF_TCP
    TLS         TRUE
    CAFile      %ROOT%\cert\ca.crt
    CertFile    %ROOT%\cert\client.crt
    KeyFile     %ROOT%\cert\client.key
</Output>
```

---

## 📚 11. Ressources utiles

- [https://docs.nxlog.co/](https://docs.nxlog.co/)
- [https://docs.graylog.org/en/latest/pages/sending\_data.html#gelf](https://docs.graylog.org/en/latest/pages/sending_data.html#gelf)
- [https://docs.nxlog.co/refman/input/im\_msvistalog.html#example-queries](https://docs.nxlog.co/refman/input/im_msvistalog.html#example-queries)

---

## ✅ Récapitulatif

| Étape | Action                                   |
| ----- | ---------------------------------------- |
| 1     | Installer NXLog sur le poste Windows     |
| 2     | Créer une entrée GELF sur Graylog        |
| 3     | Configurer `nxlog.conf` (input + output) |
| 4     | Visualiser les logs dans Graylog         |
| 5     | Filtrer ou sécuriser selon besoin        |



---

<p align="center">
  <b>🔒 Un guide proposé par <a href="https://github.com/0xCyberLiTech">0xCyberLiTech</a> • Pour des tutoriels accessibles à tous. 🔒</b>
</p>
