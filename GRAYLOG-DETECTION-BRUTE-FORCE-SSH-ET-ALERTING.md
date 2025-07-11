<!-- MASTER-HEADER-START -->
<div align="center">

<a href="https://0xcyberlitech.com/">
  <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/headers/header-graylog.svg" alt="0xCyberLiTech // Graylog" width="100%" />
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


# <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-shield.svg" width="20" height="20" align="absmiddle" alt="" /> Détection des Attaques Brute-Force SSH & Alerting Temps Réel dans Graylog (Debian 13 & 14)

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 01 // COMPRENDRE LA SIGNATURES DES ATTAQUES BRUTE-FORCE SSH
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

Le démon **OpenSSH (`ssh.service`)** est la cible numéro 1 des robots de scan et de pulvérisation de mots de passe (*Credential Stuffing* / *Brute-Force*).

Sous **Debian 13 (Trixie — OpenSSH 9.9+)** et **Debian 14 (Forky — OpenSSH 10.x)**, chaque tentative d'authentification échouée génère un événement explicite dans `systemd-journald` :
- `Failed password for invalid user <user> from <IP> port <port> ssh2`
- `Failed password for root from <IP> port <port> ssh2`
- `Connection closed by authenticating user <user> <IP> port <port> [preauth]`

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 02 // COLLECTE ET TRANSFERT DES JOURNAUX `ssh.service` VERS GRAYLOG
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

Configurez `/etc/rsyslog.d/25-graylog-ssh.conf` sur vos serveurs Debian pour transmettre en temps réel tous les événements d'authentification (`auth`, `authpriv`) vers Graylog :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```ini
> # /etc/rsyslog.d/25-graylog-ssh.conf
> auth,authpriv.* @192.168.1.50:5140;RSYSLOG_SyslogProtocol23Format
> ```
<!-- CODE-WINDOW-END -->

Vérifiez immédiatement les événements SSH locaux via `journalctl` :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo systemctl restart rsyslog
> sudo journalctl -u ssh.service -n 30 --no-hostname
> ```
<!-- CODE-WINDOW-END -->

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 03 // PIPELINE GRAYLOG D'EXTRACTION DE L'IP ATTAQUANTE & DE L'UTILISATEUR CIBLÉ
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

Dans **Graylog (`System > Pipelines`)**, ajoutez une règle qui extrait l'adresse IP source (`ssh_attacker_ip`) et le compte visé (`ssh_target_user`) :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```yaml
> rule "Parse OpenSSH Brute Force Attempts"
> when
>     has_field("message") AND contains(to_string($message.message), "Failed password for ")
> then
>     let m = regex(
>         pattern: "Failed password for (?:invalid user )?(\\S+) from ([0-9a-fA-F:\\.]+) port (\\d+)",
>         value: to_string($message.message)
>     );
>     set_field("ssh_event_type", "AUTH_FAILURE");
>     set_field("ssh_target_user", m["0"]);
>     set_field("ssh_attacker_ip", m["1"]);
>     set_field("ssh_src_port", to_long(m["2"]));
> end
> ```
<!-- CODE-WINDOW-END -->

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 04 // CRÉATION DE L'ALERTE CORRÉLÉE (SEUIL >= 5 ÉCHECS EN 60 SECONDES)
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

Dans **Graylog (`Alerts > Event Definitions > Create Event Definition`)** :
1. **Titre :** `SOC // Alerte Brute-Force SSH Détecté (>= 5 échecs / 1 min)`
2. **Condition Type :** `Filter & Aggregation`
3. **Search Query :** `ssh_event_type:AUTH_FAILURE`
4. **Search within the last :** `1 minute` / **Execute search every :** `1 minute`
5. **Group by Field(s) :** `ssh_attacker_ip`, `source`
6. **Create Events for Definition if :** `count() >= 5`
7. **Priorité :** `High (Niveau 3 — Critique)`

Vous pouvez coupler cette alerte à **Fail2ban** ou **CrowdSec** sur l'hôte Debian pour bannir automatiquement l'IP au niveau noyau `nftables` :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo apt update && sudo apt install -y fail2ban
> sudo fail2ban-client status sshd
> ```
<!-- CODE-WINDOW-END -->

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
