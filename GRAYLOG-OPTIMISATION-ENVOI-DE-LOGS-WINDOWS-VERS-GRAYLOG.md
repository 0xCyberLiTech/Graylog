<!-- MASTER-HEADER-START -->
<div align="center">

<a href="https://0xcyberlitech.com/">
  <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/headers/header-graylog.svg" alt="ATELIER GRAYLOG // CENTRALISATION SIEM" width="100%" />
</a>

<p align="center">
  <a href="https://0xcyberlitech.com/"><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-portal.svg" alt="Portail 0xCyberLiTech.com" width="24%" /></a>
  <a href="https://0xcyberlitech.com/soc-rd.html"><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-soc-rd.svg" alt="Livre Blanc SOC Cockpit" width="24%" /></a>
  <a href="https://0xcyberlitech.com/jarvis-rd.html"><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-jarvis-rd.svg" alt="Livre Blanc JARVIS IA" width="24%" /></a>
  <a href="https://github.com/0xCyberLiTech?tab=repositories"><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-github.svg" alt="Catalogue des 23 Dépôts" width="24%" /></a>
</p>
<p align="center">
  <a href="README.md"><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-back-readme.svg" alt="Retour au sommaire du dépôt" width="340" /></a>
</p>

<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/divider-hud.svg" alt="" width="100%" />
</div>
<!-- MASTER-HEADER-END -->

<!-- DEBIAN-TRUTH-START -->
> [!IMPORTANT]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-shield.svg" width="18" height="18" align="absmiddle" alt="" /> ** Matrice Officielle Debian — `Debian 12 (Bookworm)` · `Debian 13 (Trixie)` · `Debian 14 (Forky)`**
> - **Sources Officielles Debian.org (`opensearch`) :** `Bookworm (12)` : **`Stable-12`** &nbsp;·&nbsp; `Trixie (13 — Stable)` : **`Stable-13`** &nbsp;·&nbsp; `Forky (14 — Next-Gen)` : **`2.4.1+dfsg-2`**
> - **Références Officielles :** [Paquet Debian Trixie (`default-jre-headless`)](https://packages.debian.org/trixie/default-jre-headless) &nbsp;·&nbsp; [Paquet Debian Forky (`default-jre-headless`)](https://packages.debian.org/forky/default-jre-headless) &nbsp;·&nbsp; [Documentation Officielle Debian](https://www.debian.org/releases/trixie/)
> - **Note d'Ingénierie (Divergence 13 vs 14) :** Sous Debian 13 (Trixie) et Debian 14 (Forky), `/etc/sysctl.conf` monolithique est déprécié au profit de fichiers modulaires dans **`/etc/sysctl.d/99-*.conf`** chargés par `sysctl --system`.

<details>
<summary><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> <b>Afficher les Encarts Ligne de Commande : Debian 13 (Trixie — Stable) vs Debian 14 (Forky — Next-Gen)</b></summary>

#### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-ok.svg" width="42" height="16" align="absmiddle" alt="[OK]" /> Profil Production Stable — Commandes pour `Debian 13 (Trixie)`
```bash
# Debian 13 (Trixie) — Depot GPG en /etc/apt/keyrings/ & suivi systemd :
sudo install -m 0755 -d /etc/apt/keyrings
sudo systemctl status graylog-server && sudo journalctl -u graylog-server -n 50
```

#### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-rd.svg" width="46" height="16" align="absmiddle" alt="[R&D]" /> Profil Anticipation Next-Gen — Commandes pour `Debian 14 (Forky)`
```bash
# Debian 14 (Forky) — Format DEB822 (/etc/apt/sources.list.d/graylog.sources) & vm.max_map_count :
echo 'vm.max_map_count=262144' | sudo tee /etc/sysctl.d/99-opensearch.conf && sudo sysctl --system
```

</details>
<!-- DEBIAN-TRUTH-END -->

<!-- CIEL-PEDAGOGY-START -->
<details>
<summary><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-puzzle.svg" width="18" height="18" align="absmiddle" alt="" /> <b>Synthèse d'Architecture, Standards Officiels &amp; Diagnostic (Niveau 1 : Fondamentaux · Niveau 2 : Repères · Niveau 3 : Diagnostic)</b></summary>

- **Niveau 1 — Fondamentaux &amp; Principe d'Architecture :** **Graylog** est une plateforme centralisée de gestion et d'analyse de journaux (**SIEM / Log Management**) articulée autour de trois composants : **MongoDB** (configuration et métadonnées), **OpenSearch** (indexation et recherche temps réel) et **Graylog Server** (ingestion Syslog/GELF, normalisation et alertes).
- **Niveau 2 — Repères Officiels (Ports IANA, Fichiers Debian &amp; Commandes de Validation) :** **Ports standards :** `TCP 9000` (Web UI & API REST Graylog) · `UDP/TCP 5140` ou `1514` (Inputs Syslog/GELF) · `TCP 9200` (OpenSearch local) · `TCP 27017` (MongoDB local) &nbsp;|&nbsp; **Fichier clé :** `/etc/graylog/server/server.conf`.
- **Niveau 3 — Diagnostic d'Incidents &amp; Ingénierie Avancée :** **Diagnostic & Architecture :** Le démarrage de `graylog-server` requiert que `mongod.service` et `opensearch.service` soient actifs et que les paramètres `password_secret` et `root_password_sha2` soient définis. La déportation temps réel des journaux vers un puits isolé est une exigence fondamentale (ANSSI) pour préserver les preuves d'audit en cas de compromission d'un serveur.
- **Sources de Vérité Officielles Éditeurs &amp; Standards :** [Documentation Officielle Graylog](https://go2docs.graylog.org/) &nbsp;·&nbsp; [Documentation Officielle OpenSearch](https://opensearch.org/docs/latest/) &nbsp;·&nbsp; [Recommandations ANSSI Journalisation](https://cyber.gouv.fr/)

</details>
<!-- CIEL-PEDAGOGY-END -->



---

# <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-shield.svg" width="20" height="20" align="absmiddle" alt="" /> Tutoriel : Envoi optimisé de logs Windows vers Graylog avec NXLog

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> Objectif
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

Configurer NXLog sur une machine Windows pour :

- Collecter efficacement les logs (système, sécurité, application)
- Les formater proprement (JSON / GELF)
- Les envoyer vers Graylog en UDP, TCP ou TLS

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> Prérequis
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

- Poste Windows (client ou serveur)
- Serveur Graylog fonctionnel avec une entrée GELF ou Syslog
- NXLog Community Edition : [https://nxlog.co/products/nxlog-community-edition/download](https://nxlog.co/products/nxlog-community-edition/download)

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> 1. Installation de NXLog
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

1. Télécharger NXLog Community Edition
2. Lancer l’installation sur le poste Windows
3. Fichier de configuration : `C:\Program Files\nxlog\conf\nxlog.conf`

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> 2. Architecture NXLog (rappel)
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> +-------------+      +------------+     +-------------+
> |   Input     | ==>  | Processor  | ==> |   Output     |
> +-------------+      +------------+     +-------------+
> ```
<!-- CODE-WINDOW-END -->

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-puzzle.svg" width="18" height="18" align="absmiddle" alt="" /> 3. Configuration d’une entrée GELF dans Graylog
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

1. Aller dans **System > Inputs**
2. Ajouter une entrée **GELF UDP** ou **GELF TCP**
3. Choisir le port (ex : 12201)
4. Démarrer l’entrée

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-puzzle.svg" width="18" height="18" align="absmiddle" alt="" /> 4. Exemple de configuration NXLog (GELF vers Graylog)
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```sql
> define ROOT C:\Program Files\nxlog
> Moduledir %ROOT%\modules
> CacheDir %ROOT%\data
> Pidfile %ROOT%\data\nxlog.pid
> SpoolDir %ROOT%\data
> LogFile %ROOT%\data\nxlog.log
>
> <Extension _gelf>
>     Module      xm_gelf
> </Extension>
>
> <Extension _json>
>     Module      xm_json
> </Extension>
>
> <Input in_eventlog>
>     Module      im_msvistalog
>     Query       <QueryList>
>                     <Query Id="0">
>                         <Select Path="Application">*</Select>
>                         <Select Path="System">*</Select>
>                         <Select Path="Security">*</Select>
>                     </Query>
>                 </QueryList>
> </Input>
>
> <Output out_graylog>
>     Module      om_udp
>     Host        192.168.1.100     # IP Graylog
>     Port        12201             # Port GELF UDP
>     OutputType  GELF_UDP
> </Output>
>
> <Route route_all>
>     Path        in_eventlog => out_graylog
> </Route>
> ```
<!-- CODE-WINDOW-END -->

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> 5. Filtres personnalisés (optionnels)
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-ok.svg" width="42" height="16" align="absmiddle" alt="[OK]" /> Exemple : logs de niveau « Erreur » uniquement

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```sql
> <Input in_eventlog>
>     Module      im_msvistalog
>     Query       <QueryList>
>                     <Query Id="0">
>                         <Select Path="System">
>                             *[System[(Level=1 or Level=2 or Level=3)]]
>                         </Select>
>                     </Query>
>                 </QueryList>
> </Input>
> ```
<!-- CODE-WINDOW-END -->

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-crypto.svg" width="18" height="18" align="absmiddle" alt="" /> 6. Champs personnalisés
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> <Output out_graylog>
>     Module      om_udp
>     Host        192.168.1.100
>     Port        12201
>     OutputType  GELF_UDP
>     Exec        $Hostname = hostname();
>                 $custom_field = 'poste_windows_marc';
> </Output>
> ```
<!-- CODE-WINDOW-END -->

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> 7. Visualisation dans Graylog
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

- Aller dans **Search**
- Rechercher : `_source:poste_windows_marc`
- Créer un dashboard à partir des champs désirés

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> 8. Redémarrer NXLog
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> net stop nxlog
> net start nxlog
> ```
<!-- CODE-WINDOW-END -->

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-rd.svg" width="46" height="16" align="absmiddle" alt="[R&D]" /> 9. Dépannage
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

| Problème                 | Solution                                         |
| ------------------------ | ------------------------------------------------ |
| NXLog ne démarre pas     | Lire `nxlog.log` dans le dossier `data`          |
| Pas de logs dans Graylog | Vérifier IP / port de l'entrée                   |
| Champs manquants         | S'assurer que `OutputType GELF` est bien utilisé |

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-crypto.svg" width="18" height="18" align="absmiddle" alt="" /> 10. Envoi sécurisé (TLS)
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> <Output out_graylog_tls>
>     Module      om_tcp
>     Host        192.168.1.100
>     Port        12202
>     OutputType  GELF_TCP
>     TLS         TRUE
>     CAFile      %ROOT%\cert\ca.crt
>     CertFile    %ROOT%\cert\client.crt
>     KeyFile     %ROOT%\cert\client.key
> </Output>
> ```
<!-- CODE-WINDOW-END -->

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> 11. Ressources utiles
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

- [https://docs.nxlog.co/](https://docs.nxlog.co/)
- [https://docs.graylog.org/en/latest/pages/sending\_data.html#gelf](https://docs.graylog.org/en/latest/pages/sending_data.html#gelf)
- [https://docs.nxlog.co/)

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-ok.svg" width="42" height="16" align="absmiddle" alt="[OK]" /> Récapitulatif
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

| Étape | Action                                   |
| ----- | ---------------------------------------- |
| 1     | Installer NXLog sur le poste Windows     |
| 2     | Créer une entrée GELF sur Graylog        |
| 3     | Configurer `nxlog.conf` (input + output) |
| 4     | Visualiser les logs dans Graylog         |
| 5     | Filtrer ou sécuriser selon besoin        |

<!-- MASTER-FOOTER-START -->
<div align="center">
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/divider-hud.svg" alt="" width="100%" />

<a href="https://0xcyberlitech.com/">
  <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/footer-master.svg" alt="0xCyberLiTech — Architecture Cyberdéfense, Ingénierie Déterministe & IA Souveraine" width="100%" />
</a>

<p align="center"><a href="https://0xcyberlitech.com/"><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/badge-antigravity.svg" alt="Architecturé par Marc & Antigravity (Google DeepMind)" width="520" /></a></p>

<sub><b>Architecturé &amp; Forgé par Marc &amp; Antigravity (Google DeepMind)</b> &nbsp;·&nbsp; <a href="https://0xcyberlitech.com/"><b>0xcyberlitech.com</b></a> &nbsp;·&nbsp; <a href="https://0xcyberlitech.com/soc-rd.html">Architecture SOC Cockpit v5.5</a> &nbsp;·&nbsp; <a href="https://0xcyberlitech.com/jarvis-rd.html">Architecture JARVIS Mark-VII</a> &nbsp;·&nbsp; <a href="https://0xcyberlitech.com/blueprint-jarvis.html">Blueprint Matériel RTX 5080</a></sub>

</div>
<!-- MASTER-FOOTER-END -->
