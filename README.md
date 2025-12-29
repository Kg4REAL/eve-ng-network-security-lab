# 🔐 Network Security & Pentest Lab – EVE-NG

## 📌 Présentation
Ce projet est un **lab complet de sécurité réseau** réalisé sous **EVE-NG**, combinant :

- la **conception d’un réseau campus redondant**
- et la **réalisation d’un scénario de pentest réaliste**

L’objectif est de reproduire une infrastructure d’entreprise, puis d’analyser sa surface d’attaque, d’exploiter certaines faiblesses et de proposer des mesures de mitigation.

---

## 🧠 Architecture réseau
Le réseau suit une architecture hiérarchique classique (Accès / Distribution) avec mécanismes de redondance.

### Équipements
- 2 switches **Layer 3** (Distribution)
- 2 switches **Layer 2** (Accès)
- Machines clientes Linux
- Une machine **Kali Linux** (attaquant)

### VLANs
| VLAN | Nom        |
|-----:|------------|
| 10   | RG         |
| 20   | MARKETING  |
| 30   | DRH        |
| 40   | GUEST      |

### Redondance et haute disponibilité
- **RSTP** pour la prévention des boucles
- **EtherChannel (LACP)** pour l’agrégation de liens
- **HSRP** avec répartition de charge par VLAN

| VLAN | Root STP | HSRP Active |
|-----:|----------|-------------|
| 10   | phede-1  | phede-1    |
| 20   | phede-1  | phede-1    |
| 30   | phede-2  | phede-2    |
| 40   | phede-2  | phede-2    |

Un schéma du réseau est disponible dans `network-diagram.png`.

---

## ⚙️ Technologies utilisées
### Réseau
- Cisco IOS
- VLAN / 802.1Q
- RSTP
- EtherChannel (LACP)
- HSRP

### Sécurité
- Kali Linux
- Nmap
- Hydra
- SSH
- Webmin

---

## 🔍 Scénario de pentest
Le pentest est réalisé **depuis le réseau interne**, dans un contexte réaliste d’entreprise.

Les différentes phases sont documentées dans le dossier `pentest/` :

| Étape | Description |
|-----:|-------------|
| 00 | Présentation du scénario |
| 01 | Reconnaissance réseau |
| 02 | Scan des services |
| 03 | Exploitation Webmin |
| 04 | Pivoting |
| 05 | Attaque VLAN Hopping |
| 06 | Findings et constats |

Des captures d’écran sont disponibles dans `pentest/screen/` afin d’illustrer chaque phase.

---

## 🧪 Tests et validations réseau
Les mécanismes de redondance ont été testés via :

- Vérification des EtherChannel
- Vérification du STP
- Vérification du DHCP
- Vérification des états HSRP
- Vérification VTP
- Simulation de pannes (liens et équipements)

Les résultats des commandes sont disponibles dans le dossier `verifications/`.


## 📂 Structure du projet
```text
configs/              → configurations des switches et routeurs
eve-ng/               → topologie EVE-NG
pentest/              → méthodologie et exploitation
│ └── screen/         → preuves et captures d’écran
verifications/        → commandes de validation réseau
network-diagram.png  → schéma du réseau
```

##🎯 Objectifs pédagogiques

Concevoir une infrastructure réseau résiliente

Comprendre les mécanismes de redondance

Identifier des failles dans un réseau interne

Réaliser un pentest structuré

Proposer des mesures de sécurisation adaptées
---
