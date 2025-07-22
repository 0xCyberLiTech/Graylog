<div align="center">
<a href="https://github.com/0xCyberLiTech">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&size=32&pause=1000&color=D14A4A&center=true&vCenter=true&width=1000&lines=SUPERVISION+CENTRALISÉE+AVEC+GRAYLOG;Détection+des+menaces+•+Logs+structurés+•+Alertes;Tutoriel+pédagogique+100%+Debian+12" alt="Typing SVG" />
</a>

<p align="center">
  <em>Tuto, filtrage et enrichissement des logs avec les Pipelines Graylog.</em><br>
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

# 🧩 Filtrage et enrichissement des logs avec les Pipelines Graylog

## 🎯 Objectif

Utiliser les pipelines Graylog pour filtrer ou enrichir les messages journaux à la volée, afin de :
- Réduire les logs stockés
- Supprimer les messages inutiles ou trop verbeux
- Taguer ou enrichir les événements critiques

---

## 🛠️ Étapes de création d’un pipeline

### 1. Créer une règle de pipeline

Aller dans **System > Pipelines > Manage Rules > Create Rule**

#### Exemple 1 : Ignorer les logs de niveau trop bas

```pipelinerule
rule "Supprimer les logs de niveau Information ou Audit Success"
when
  to_long($message.level) >= 4 OR contains(to_string($message.Message), "Audit Success")
then
  drop_message();
end
```

✅ Supprime les événements :
- De niveau 4 (Information)
- Qui contiennent "Audit Success" dans leur message

---

#### Exemple 2 : Taguer les événements critiques de sécurité

```pipelinerule
rule "Filtrer source Security et niveau critique"
when
  has_field("source") AND
  to_string($message.source) == "Security" AND
  to_long($message.level) <= 2
then
  set_field("critical_event", true);
end
```

🎯 Crée un champ `critical_event` pour les logs critiques venant de la source `Security`.

---

### 2. Créer un pipeline

- Aller dans **System > Pipelines > Create Pipeline**
- Nom suggéré : `FiltrageMinimal`
- Ajouter les règles créées dans l’ordre souhaité

---

### 3. Attacher le pipeline à un flux

1. Dans `System > Pipelines`, cliquer sur `Connect pipeline to stream`
2. Sélectionner le flux `All messages` ou un flux personnalisé (`Windows logs`)
3. Le pipeline est désormais actif sur ce flux

---

## 🔍 Résultat

| Étape                     | Action                                                       |
|--------------------------|--------------------------------------------------------------|
| 🎛 NXLog                 | Envoie un sous-ensemble de logs (filtrés localement)         |
| 🧩 Pipeline Graylog      | Supprime/enrichit/transforme les logs restants               |
| 🗄️ Stockage final       | Contient uniquement ce qui est utile à l'analyse             |

---

## 🧠 Astuce

Tu peux enchaîner plusieurs règles dans le même pipeline pour :
- Supprimer certains logs
- Ajouter des tags (`set_field`)
- Rediriger vers un flux spécifique (`route_to_stream`)

---

## ✅ Bonnes pratiques

- Teste toujours tes règles avec l'outil `Simulate rule` dans Graylog
- Utilise des noms explicites pour les règles et pipelines
- Gère les priorités si plusieurs pipelines sont actifs sur le même flux

---

🛠 Maintenu par [TonNom ou @GitHubID] — adapté à un environnement Graylog 6.x

---

**Mise à jour :** Juillet 2025

---

<p align="center">
  <b>🔒 Un guide proposé par <a href="https://github.com/0xCyberLiTech">0xCyberLiTech</a> • Pour des tutoriels accessibles à tous. 🔒</b>
</p>




