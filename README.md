# GUIDE COMPLET DE CONFIGURATION PRATIQUE DES SWITCHES CISCO

## De la configuration de base aux fonctionnalités avancées

> Manuel de référence technique en français, orienté Cisco IOS / IOS XE, adapté à l’apprentissage, au laboratoire, à Packet Tracer et aux équipements compatibles.

---

## Table des matières

1. [Introduction et méthode de travail](#1-introduction-et-methode-de-travail)
2. [Inventaire général des domaines de configuration](#2-inventaire-general-des-domaines-de-configuration)
3. [Catalogue de couverture des commandes](#3-catalogue-de-couverture-des-commandes)
4. [Partie I — Fondamentaux et configuration initiale](#4-partie-i--fondamentaux-et-configuration-initiale)
   1. [Présentation des switches Cisco](#41-prsentation-des-switches-cisco)
   2. [Familles de switches et différences entre Layer 2 et Layer 3](#42-familles-de-switches-et-differences-entre-layer-2-et-layer-3)
   3. [Cisco IOS et IOS XE](#43-cisco-ios-et-ios-xe)
   4. [Modes de commande et navigation dans le CLI](#44-modes-de-commande-et-navigation-dans-le-cli)
   5. [Aide intégrée `?` et complétion des commandes](#45-aide-intgre--et-completion-des-commandes)
   6. [Configuration initiale](#46-configuration-initiale)
   7. [Hostname](#47-hostname)
   8. [Mots de passe et privilèges](#48-mots-de-passe-et-privileges)
   9. [Bannière MOTD](#49-banniere-motd)
   10. [Configuration de la console](#410-configuration-de-la-console)
   11. [Configuration des lignes VTY](#411-configuration-des-lignes-vty)
   12. [Désactivation des fonctions inutiles](#412-desactivation-des-fonctions-inutiles)
   13. [Sauvegarde et restauration de configuration](#413-sauvegarde-et-restauration-de-configuration)
   14. [Commandes de vérification générales](#414-commandes-de-verification-generales)
5. [Annexes](#5-annexes)
   - [Glossaire français-anglais](#glossaire-francais-anglais)
   - [Index alphabétique des commandes](#index-alphabetique-des-commandes)
   - [Liste des commandes par mode IOS](#liste-des-commandes-par-mode-ios)
   - [Liste des commandes par fonctionnalité](#liste-des-commandes-par-fonctionnalite)
   - [Révision et exercices](#revision-et-exercices)

---

# 1. Introduction et méthode de travail

Ce guide a pour objectif de servir de manuel de travail pratique et de référence pour la configuration, la vérification, l’administration et le dépannage des switches Cisco. Il s’adresse à des étudiants en réseaux et systèmes, à des techniciens de laboratoire et à des personnes préparant le CCNA.

Le document est volontairement structuré en trois axes :

- la théorie utile,
- la configuration pratique en CLI,
- la vérification et le dépannage.

Il ne prétend pas à l’universalité absolue sur tous les modèles Cisco. Les commandes peuvent varier selon :

- la famille de matériel,
- la version IOS / IOS XE,
- la présence ou l’absence d’une fonctionnalité,
- la plateforme (Packet Tracer, Catalyst, Nexus, etc.).

Les syntaxes sont présentées avec leurs précautions d’usage, avec un souci d’exactitude et d’exploitation immédiate en laboratoire.

---

# 2. Inventaire général des domaines de configuration

Avant de documenter les commandes une à une, il faut établir un inventaire des domaines fonctionnels. Cela permet de contrôler qu’aucun sujet important n’est oublié et qu’aucune commande ne soit oubliée ou répétée inutilement.

## 2.1 Domaines d’administration de base

- configuration initiale du switch,
- hostname,
- mots de passe,
- privilèges,
- console,
- VTY,
- services inutiles,
- sauvegarde / restauration,
- vérifications générales.

## 2.2 Domaines des interfaces et ports

- sélection d’interfaces,
- description,
- vitesse / duplex,
- activation / désactivation,
- états administratifs et opérationnels,
- compteurs et erreurs,
- diagnostics des ports,
- interfaces de management,
- interfaces virtuelles et logiques.

## 2.3 Domaines VLAN

- création et suppression,
- nommage,
- affectation d’un port access,
- trunk,
- VLAN natif,
- VLAN de management,
- Voice VLAN,
- vérification et dépannage.

## 2.4 Domaines trunk, DTP et VTP

- modes Access / Trunk,
- encapsulation 802.1Q,
- VLAN autorisés,
- native VLAN,
- DTP,
- VTP,
- compatibilité et versions,
- problèmes de propagation.

## 2.5 Domaines STP et robustesse de la couche 2

- STP,
- PVST+,
- MST,
- Root Bridge,
- PortFast,
- BPDU Guard,
- Root Guard,
- Loop Guard,
- UDLD,
- récupération et diagnostic.

## 2.6 Domaines EtherChannel

- LACP,
- PAgP,
- mode statique,
- Port-Channel,
- vérification de l’agrégation,
- dépannage des liens groupés.

## 2.7 Sécurité des switches

- Port Security,
- DHCP Snooping,
- DAI,
- IP Source Guard,
- storm control,
- ACL,
- 802.1X,
- AAA,
- SSH,
- durcissement.

## 2.8 Administration et supervision

- IP de management,
- SVI,
- SSH,
- SNMP,
- syslog,
- NTP,
- CDP,
- LLDP,
- surveillance des ressources et de la configuration.

## 2.9 Switching Layer 3

- SVI,
- routage inter-VLAN,
- routes statiques,
- routes par défaut,
- OSPF / EIGRP / RIP selon plateforme,
- ACL couche 3,
- IPv6,
- diagnostics de routage.

## 2.10 Fonctionnalités avancées

- QoS,
- SPAN / Port Mirroring,
- PoE,
- support de licences,
- mise à jour logicielle,
- sauvegarde / restauration,
- surveillance matérielle.

## 2.11 Dépannage et diagnostics

- show running-config,
- show interfaces,
- show vlan brief,
- show spanning-tree,
- show etherchannel summary,
- show mac address-table,
- ping,
- traceroute,
- debug avec précautions,
- clear et remise à zéro des compteurs.

---

# 3. Catalogue de couverture des commandes

Le catalogue ci-dessous sert de référence de suivi. Il ne remplace pas la documentation de commande, mais permet de vérifier qu’un domaine important a bien été traité.

## 3.1 Commandes de configuration de base

- `enable`
- `disable`
- `configure terminal`
- `hostname`
- `enable secret`
- `enable password`
- `service password-encryption`
- `banner motd`
- `line console 0`
- `line vty 0 15`
- `logging synchronous`
- `exec-timeout`
- `login`
- `password`
- `ip domain-name`
- `crypto key generate rsa`
- `ip ssh version 2`
- `ip default-gateway`
- `ip address`
- `interface vlan`
- `ip routing`
- `no ip domain-lookup`
- `no cdp run`
- `no ip http server`
- `no ip http secure-server`

## 3.2 Commandes d’interfaces

- `interface FastEthernet 0/1`
- `interface GigabitEthernet 0/1`
- `interface range`
- `description`
- `shutdown` / `no shutdown`
- `speed`
- `duplex`
- `negotiation auto`
- `switchport`
- `no switchport`
- `switchport mode access`
- `switchport mode trunk`
- `switchport access vlan`
- `switchport trunk allowed vlan`
- `switchport trunk native vlan`
- `switchport trunk encapsulation dot1q`
- `switchport port-security`
- `storm-control`

## 3.3 Commandes VLAN

- `vlan 10`
- `name ADMIN`
- `show vlan`
- `show vlan brief`
- `show interfaces switchport`
- `show interfaces trunk`
- `switchport access vlan 10`
- `switchport voice vlan 50`
- `switchport mode access`
- `switchport mode trunk`
- `no vlan 10`

## 3.4 Commandes trunk, DTP et VTP

- `switchport mode trunk`
- `switchport trunk encapsulation dot1q`
- `switchport trunk allowed vlan 10,20,30`
- `switchport trunk native vlan 99`
- `switchport nonegotiate`
- `vtp domain DOMAIN1`
- `vtp password secret`
- `vtp mode server`
- `vtp mode client`
- `vtp mode transparent`
- `vtp version 2`
- `show vtp status`
- `show interfaces trunk`

## 3.5 Commandes STP

- `spanning-tree mode rapid-pvst`
- `spanning-tree vlan 10 root primary`
- `spanning-tree vlan 10 root secondary`
- `spanning-tree vlan 10 priority 4096`
- `spanning-tree portfast`
- `spanning-tree portfast default`
- `spanning-tree bpduguard enable`
- `spanning-tree guard root`
- `spanning-tree guard loop`
- `show spanning-tree`
- `show spanning-tree summary`

## 3.6 Commandes EtherChannel

- `interface range g0/1 - 2`
- `channel-group 1 mode active`
- `channel-group 1 mode passive`
- `channel-group 1 mode desirable`
- `channel-group 1 mode auto`
- `interface Port-channel 1`
- `switchport mode trunk`
- `show etherchannel summary`
- `show lacp neighbor`
- `show pagp neighbor`

## 3.7 Commandes de sécurité

- `switchport port-security`
- `switchport port-security maximum 2`
- `switchport port-security violation restrict`
- `switchport port-security mac-address sticky`
- `switchport port-security mac-address 0011.2233.4455`
- `ip dhcp snooping`
- `ip dhcp snooping vlan 10`
- `ip arp inspection vlan 10`
- `ip verify source`
- `storm-control broadcast level 20.00`
- `aaa new-model`
- `username admin secret Cisco123!`
- `ip access-list standard ACL-LAN`
- `permit 10.10.10.0 0.0.0.255`
- `ssh` / `ip ssh version 2`

## 3.8 Commandes de supervision et administration

- `show running-config`
- `show startup-config`
- `show version`
- `show interfaces status`
- `show interfaces counters errors`
- `show mac address-table`
- `show cdp neighbors`
- `show lldp neighbors`
- `show logging`
- `show ip route`
- `show ip interface brief`
- `ping`
- `traceroute`
- `debug`
- `clear counters`
- `clear mac address-table dynamic`

---

# 4. Partie I — Fondamentaux et configuration initiale

## 4.1. Présentation des switches Cisco

Un switch Cisco est un équipement central dans un réseau local. Il remplit plusieurs fonctions :

- agrégation de plusieurs hôtes sur un même domaine de diffusion,
- segmentation par VLAN,
- contrôle de la couche 2 via le protocole STP,
- extension des fonctionnalités de routage sur certains modèles,
- fourniture de services de sécurité et de supervision.

### Rôle d’un switch

Le switch agit principalement à la couche 2 du modèle OSI, mais certains matériels peuvent également fournir des fonctions de couche 3 et de routage inter-VLAN.

### Différences importantes

- Switch Layer 2 : commutation de trames, VLAN, STP, EtherChannel, Port Security.
- Switch Layer 3 : routage IP, interfaces VLAN, SVI, routes statiques et protocols de routage.

### Types d’équipements Cisco courants

- Cisco Catalyst 2960, 3560, 3650, 3850, 9300.
- Cisco Catalyst 1000/1200 selon les gammes de bureau.
- Cisco Catalyst 9300/9400 pour infrastructures plus avancées.
- Cisco Nexus pour data center, utilisant NX-OS, non identique à IOS.

### Considérations de laboratoire

Les exercices de ce guide supposent en général :

- un switch Cisco Catalyst avec IOS ou IOS XE,
- au minimum deux switchs pour les TP de VLAN et de trunk,
- quelques PC ou serveurs virtuels,
- des câbles Ethernet de qualité,
- le mode simulation Packet Tracer ou un équipement réel.

### points importants

- Un switch Cisco n’est pas un routeur.
- Les fonctionnalités avancées dépendent du modèle et du logiciel.
- Un switch Layer 2 peut être embarqué dans un design simplifié.
- Un switch Layer 3 simplifie les inter-VLAN mais exige une stratégie d’adressage plus rigoureuse.

---

## 4.2. Familles de switches et différences entre Layer 2 et Layer 3

### 4.2.1. Familles de switch Cisco

Cisco propose plusieurs familles de switch, selon les cas d’usage.

#### Famille Catalyst

- très utilisée dans les LAN d’entreprise,
- supporte VLAN, STP, EtherChannel, port security,
- réunit les fonctionnalités habitude de la couche 2, parfois la couche 3 sur certains modèles.

#### Famille Nexus

- orientée data center,
- utilise NX-OS,
- diffère sensiblement de IOS / IOS XE.

### 4.2.2. Layer 2 vs Layer 3

| Fonctionnalité | Layer 2 | Layer 3 |
|---|---|---|
| Commutation de trames | Oui | Oui |
| VLAN | Oui | Oui |
| STP | Oui | Oui |
| Trunk 802.1Q | Oui | Oui |
| Routage IP | Non | Oui |
| SVI | Non ou partiel | Oui |
| Inter-VLAN | Non | Oui |
| ACL L3 | Non | Oui |

### 4.2.3. Cas d’usage

- Layer 2 : accès réseau aux postes, VLAN locaux, sécurité portuaire.
- Layer 3 : segmentation plus fine, inter-VLAN, gateways, routage interne.

### 4.2.4. Commandes de vérification utiles

```text
Switch# show ip interface brief
Switch# show interfaces status
Switch# show vlan brief
Switch# show running-config | section interface
```

### 4.2.5. Points importants

- Tous les switches Cisco ne routent pas par défaut.
- La commande `ip routing` est nécessaire sur un switch Layer 3 pour activer le routage IP.
- Sur un switch Layer 2, le routage inter-VLAN ne fonctionne pas sans configuration spécifique.

---

## 4.3. Cisco IOS et IOS XE

### 4.3.1. IOS

Cisco IOS est le système d’exploitation historique des routeurs et switches Cisco. Sa syntaxe CLI est la plus répandue sur les équipements de bureau et de campus.

### 4.3.2. IOS XE

IOS XE est une évolution de l’architecture Cisco, surtout présente sur les plateformes modernes. Il repose sur une structure logicielle plus récente, mais conserve la CLI traditionnellement exploitable par les administrateurs.

### 4.3.3. Différences de présentation

Le CLI reste généralement très proche, mais certains services ou commandes peuvent être spécifiques à IOS XE.

Exemples de vérification :

```text
Switch# show version
Switch# show inventory
Switch# show running-config
```

### 4.3.4. Points importants

- Les commandes ne sont pas toujours identiques sur tous les modèles.
- Certaines commandes peuvent exister seulement sur les modèles capables de les supporter.
- Les switchs Cisco Nexus utilisent NX-OS, pas IOS / IOS XE.

---

## 4.4. Modes de commande et navigation dans le CLI

La navigation dans l’interface de commande est essentielle pour comprendre les commandes Cisco.

### Modes principaux

```text
Switch> 
Switch#
Switch(config)#
Switch(config-if)#
Switch(config-vlan)#
Switch(config-line)#
Switch(config-router)#
```

### Exemple de progression

```text
Switch> enable
Switch# configure terminal
Switch(config)# hostname S1
S1(config)# interface gigabitethernet 0/1
S1(config-if)# description Serveur Web
S1(config-if)# exit
S1(config)# exit
S1#
```

### Commandes de navigation

- `enable` : passe du mode utilisateur au mode privilégié.
- `disable` : repasse au mode utilisateur.
- `configure terminal` : passe en mode configuration globale.
- `interface ...` : entre dans le mode d’interface.
- `exit` : remonte au mode précédent.
- `end` : quitte tous les sous-modes et revient au mode privilégié.

### 4.4.1. Vérification

```text
S1# show privilege
S1# show running-config | begin hostname
```

### 4.4.2. Points importants

- La structure des modes est un élément fondamental du fonctionnement IOS.
- Une erreur fréquente est de lancer une commande dans le mauvais mode.
- Le prompt indique souvent le mode actuel.

---

## 4.5. Aide intégrée `?` et complétion des commandes

Cisco IOS dispose d’une aide très utile. Elle permet de :

- afficher la liste des commandes disponibles,
- connaître les paramètres attendus,
- vérifier la syntaxe,
- réduire les erreurs de frappe.

### Exemples

```text
Switch> ?
Switch# conf?
Switch# configure ?
Switch(config)# interface ?
Switch(config)# interface gigabitEthernet 0/1 ?
```

### Complétion partielle

```text
Switch# sh ru?
Switch# show runn
Switch# show running-config
```

### Commandes typiques d’aide

- `?` : affiche la liste des commandes disponibles.
- `command ?` : affiche les sous-options disponibles.
- `Tab` : complète la commande selon le contexte.

### Points importants

- L’aide `?` est un outil central pour apprendre l’IOS.
- Une commande invalide peut être corrigée en observant le message de l’IOS.
- Les options varient selon le modèle et la version.

---

## 4.6. Configuration initiale

La configuration initiale d’un switch Cisco consiste à mettre en place les éléments indispensables à un fonctionnement sûr et exploitable.

### 4.6.1. Étapes usuelles

1. Accéder au CLI.
2. Passer en mode privilégié.
3. Définir le nom du switch.
4. Définir les mots de passe.
5. Configurer la bannière.
6. Sécuriser les accès administratifs.
7. Paramétrer le management réseau.
8. Vérifier la configuration.
9. Sauvegarder la configuration.

### 4.6.2. Exemple de base

```text
Switch> enable
Switch# configure terminal
Switch(config)# hostname S1
S1(config)# enable secret Cisco123!
S1(config)# service password-encryption
S1(config)# banner motd # Acces reserver au personnel autorise #
S1(config)# line console 0
S1(config-line)# logging synchronous
S1(config-line)# exec-timeout 5 0
S1(config-line)# password Console123!
S1(config-line)# login
S1(config-line)# exit
S1(config)# line vty 0 15
S1(config-line)# password Vty123!
S1(config-line)# login
S1(config-line)# exit
S1(config)# exit
S1# copy running-config startup-config
```

### 4.6.3. Vérification

```text
S1# show running-config | section hostname
S1# show running-config | section line
S1# show startup-config
```

### 4.6.4. Points importants

- `enable secret` est préférable à `enable password` pour sécuriser les privilèges.
- `service password-encryption` protège les mots de passe en clair dans la configuration.
- Les mots de passe sont des paramètres sensibles ; ils doivent respecter la politique de sécurité.

---

## 4.7. Hostname

### 4.7.1. Objectif / Rôle

La commande `hostname` permet de donner un nom explicite au switch afin de le distinguer dans le réseau, dans les journaux et dans la supervision.

### 4.7.2. Mode requis

```text
Switch>
Switch#
Switch(config)#
```

### 4.7.3. Configuration

```text
Switch> enable
Switch# configure terminal
Switch(config)# hostname S1
S1(config)#
```

### 4.7.4. Vérification

```text
S1# show running-config | include hostname
```

Résultat attendu :

```text
hostname S1
```

### 4.7.5. Points importants

- Le nom est local au switch.
- Un nom explicite de type `S1`, `S2`, `CORE-AGG-01` facilite la gestion.
- Un nom de switch doit rester cohérent avec la topologie.

### 4.7.6. Résultat final

Le prompt devient :

```text
S1#
```

---

## 4.8. Mots de passe et privilèges

### 4.8.1. Objectif / Rôle

Les commandes de sécurité permettent de protéger l’accès au switch, notamment l’accès en mode privilégié et le contrôle des sessions administratives.

### 4.8.2. Modes requis

```text
Switch(config)#
Switch(config-line)#
```

### 4.8.3. Configuration

```text
Switch> enable
Switch# configure terminal
Switch(config)# enable secret Cisco123!
Switch(config)# username admin privilege 15 secret Admin2025!
Switch(config)# line console 0
Switch(config-line)# password Console123!
Switch(config-line)# login
Switch(config-line)# exit
Switch(config)# line vty 0 15
Switch(config-line)# password Vty123!
Switch(config-line)# login
Switch(config-line)# exit
```

### 4.8.4. Vérification

```text
Switch# show running-config | include enable secret
Switch# show running-config | section line vty
Switch# show running-config | section username
```

### 4.8.5. Points importants

- `enable secret` est la méthode recommandée.
- `enable password` est moins sûr et plus ancien.
- `privilege 15` donne les droits administrateurs complets.
- `username ... secret ...` est souvent utilisé avec SSH et AAA.

### 4.8.6. Exemple de suppression

```text
Switch(config)# no enable secret
Switch(config)# no username admin
```

---

## 4.9. Bannière MOTD

### 4.9.1. Objectif / Rôle

La bannière MOTD affiche un message lors de la connexion au switch. Elle sert à informer les utilisateurs et à formaliser l’accès aux équipements.

### 4.9.2. Mode requis

```text
Switch(config)#
```

### 4.9.3. Configuration

```text
Switch> enable
Switch# configure terminal
Switch(config)# banner motd #
************************************************************************
* ACCES RESERVE AU PERSONNEL AUTORISE *
* Toute tentative non autorisee est interdite. *
************************************************************************
#
```

### 4.9.4. Vérification

```text
Switch# show running-config | include banner motd
```

### 4.9.5. Points importants

- Les délimiteurs `#` ou `%` peuvent être utilisés comme marqueurs de début/fin.
- Le message ne remplace pas la sécurité ; il sert surtout à alerter.
- Il faut éviter les caractères pouvant être interprétés comme des séquences de fin de ligne.

---

## 4.10. Configuration de la console

### 4.10.1. Objectif / Rôle

La console permet un accès local au switch pendant les phases d’installation, de dépannage et de maintenance.

### 4.10.2. Mode requis

```text
Switch(config-line)#
```

### 4.10.3. Configuration

```text
Switch> enable
Switch# configure terminal
Switch(config)# line console 0
Switch(config-line)# password Console123!
Switch(config-line)# login
Switch(config-line)# exec-timeout 5 0
Switch(config-line)# logging synchronous
Switch(config-line)# exit
```

### 4.10.4. Vérification

```text
Switch# show line console 0
Switch# show running-config | section line console 0
```

### 4.10.5. Points importants

- `logging synchronous` évite que les messages système interrompent la saisie de commande.
- `exec-timeout` règle l’inactivité avant retour au prompt.
- Les valeurs de timeout doivent être adaptées au contexte de maintenance.

---

## 4.11. Configuration des lignes VTY

### 4.11.1. Objectif / Rôle

Les lignes VTY (Virtual Terminal) sont utilisées pour l’accès distant via SSH ou Telnet (si activé). Elles doivent être protégées par mot de passe et, idéalement, fermées ou limitées à SSH.

### 4.11.2. Mode requis

```text
Switch(config-line)#
```

### 4.11.3. Configuration

```text
Switch> enable
Switch# configure terminal
Switch(config)# line vty 0 15
Switch(config-line)# password Vty123!
Switch(config-line)# login
Switch(config-line)# exec-timeout 10 0
Switch(config-line)# transport input ssh
Switch(config-line)# exit
```

### 4.11.4. Vérification

```text
Switch# show line vty 0 15
Switch# show running-config | section line vty
```

### 4.11.5. Points importants

- `transport input ssh` est préférable à `telnet` si SSH est disponible.
- Les lignes VTY peuvent être restreintes selon le besoin.
- SSH nécessite au préalable des clés RSA et un nom de domaine.

---

## 4.12. Désactivation des fonctions inutiles

### 4.12.1. Objectif / Rôle

Il est recommandé d’éteindre les services inutiles pour réduire la surface d’attaque, limiter le bruit et sécuriser le switch.

### 4.12.2. Commandes fréquentes

```text
Switch(config)# no ip domain-lookup
Switch(config)# no cdp run
Switch(config)# no ip http server
Switch(config)# no ip http secure-server
Switch(config)# service tcp-keepalives-in
Switch(config)# no service config
```

### 4.12.3. Vérification

```text
Switch# show running-config | include ip domain-lookup
Switch# show running-config | include cdp
Switch# show running-config | include ip http
```

### 4.12.4. Points importants

- Les services inutiles peuvent avoir un impact sur le fonctionnement, la sécurité ou la supervision.
- `no cdp run` peut empêcher la découverte de voisins sur des équipements Cisco.
- Dans certains contextes de support, CDP ou LLDP peuvent être utiles.

---

## 4.13. Sauvegarde et restauration de configuration

### 4.13.1. Objectif / Rôle

La sauvegarde de la configuration est fondamentale. Elle permet de restaurer le switch après un changement, une panne ou une mauvaise manipulation.

### 4.13.2. Commandes principales

```text
Switch# copy running-config startup-config
Switch# write memory
Switch# show startup-config
Switch# show running-config
```

### 4.13.3. Restauration

```text
Switch# configure replace nvram:startup-config
Switch# copy startup-config running-config
```

### 4.13.4. Nettoyage et réinitialisation

```text
Switch# write erase
Switch# erase startup-config
Switch# reload
```

### 4.13.5. Précautions

- `erase` et `reload` peuvent interrompre le réseau.
- Les opérations de suppression et de reboot doivent être planifiées.
- Avant effacement, sauvegarder la configuration actuelle.

---

## 4.14. Commandes de vérification générales

Les commandes de vérification permettent de confirmer l’état du switch avant et après modification.

### 4.14.1. Commandes de base

```text
Switch# show version
Switch# show running-config
Switch# show startup-config
Switch# show interfaces status
Switch# show ip interface brief
Switch# show vlan brief
Switch# show mac address-table
Switch# show spanning-tree summary
```

### 4.14.2. Diagnostics de base

```text
Switch# ping 192.168.10.1
Switch# traceroute 192.168.10.1
Switch# show logging
Switch# show history
```

### 4.14.3. Points importants

- Les `show` sont la clé du dépannage.
- La vérification doit être systématique après chaque modification.
- Une commande sans vérification peut masquer une erreur de configuration.

---

# 5. Annexes

## Glossaire français-anglais

- Interface : Interface
- VLAN : Virtual LAN
- Trunk : Trunk link
- Access : Access port
- Port-Channel : Port aggregation / EtherChannel
- SVI : Switched Virtual Interface
- STP : Spanning Tree Protocol
- BPDU : Bridge Protocol Data Unit
- ACL : Access Control List
- DHCP Snooping : DHCP Snooping
- DAI : Dynamic ARP Inspection
- PoE : Power over Ethernet
- CLI : Command Line Interface
- IOS : Internetwork Operating System
- IOS XE : IOS XE
- LACP : Link Aggregation Control Protocol
- PAgP : Port Aggregation Protocol

## Index alphabétique des commandes

- `aaa new-model`
- `banner motd`
- `copy running-config startup-config`
- `debug`
- `enable secret`
- `hostname`
- `interface range`
- `ip dhcp snooping`
- `ip route`
- `line console 0`
- `ping`
- `show interfaces status`
- `show running-config`
- `show spanning-tree`
- `show vlan brief`
- `switchport mode trunk`
- `vlan`
- `vtp mode server`

## Liste des commandes par mode IOS

### Mode utilisateur

```text
Switch>
show ?
ping
traceroute
enable
```

### Mode privilégié

```text
Switch#
show running-config
show interfaces
show vlan brief
copy running-config startup-config
reload
```

### Mode configuration globale

```text
Switch(config)#
hostname S1
enable secret Cisco123!
line vty 0 15
vlan 10
ip domain-name example.com
```

### Mode interface

```text
Switch(config-if)#
description Serveur Web
switchport mode access
switchport access vlan 10
shutdown
```

### Mode VLAN

```text
Switch(config-vlan)#
name ADMIN
```

### Mode ligne

```text
Switch(config-line)#
password Console123!
login
exec-timeout 5 0
logging synchronous
```

## Liste des commandes par fonctionnalité

### Configuration initiale
- `hostname`
- `enable secret`
- `service password-encryption`
- `banner motd`

### VLAN
- `vlan 10`
- `name ADMIN`
- `switchport access vlan 10`
- `switchport mode trunk`

### STP
- `spanning-tree mode rapid-pvst`
- `spanning-tree vlan 10 root primary`
- `spanning-tree portfast`

### EtherChannel
- `interface Port-channel 1`
- `channel-group 1 mode active`
- `show etherchannel summary`

### Sécurité
- `switchport port-security`
- `ip dhcp snooping`
- `ip arp inspection vlan 10`
- `aaa new-model`

### Dépannage
- `show running-config`
- `show interfaces status`
- `show spanning-tree`
- `ping`
- `traceroute`

## Révision et exercices

### Exercices de révision

1. Créer un switch nommé `S1` et sécuriser l’accès console.
2. Configurer un VLAN 10 nommé `ADMIN`.
3. Affecter le port `Fa0/1` en mode access dans VLAN 10.
4. Vérifier la configuration avec `show vlan brief`.
5. Configurer un trunk entre `S1` et `S2` sur `Gi0/1`.
6. Vérifier l’état du trunk avec `show interfaces trunk`.
7. Définir un root bridge primaire pour VLAN 10.
8. Vérifier la topologie STP avec `show spanning-tree`.
9. Activer la sécurité sur un port d’accès.
10. Sauvegarder la config avec `copy running-config startup-config`.

### Questions de contrôle

- À quel mode faut-il être pour configurer le hostname ?
- Quelle commande permet de sécuriser l’accès privilégié ?
- Quelle est la différence entre `switchport mode access` et `switchport mode trunk` ?
- Pourquoi `show interfaces status` est-il essentiel pour le dépannage ?
- Quelles précautions avant `reload` ou `write erase` ?

---

## Conclusion

Ce document représente une base technique solide pour la configuration pratique des switches Cisco. Il est organisé de manière progressive, avec des commandes réelles, des modes IOS mentionnés, une logique de vérification et des recommandations de sécurité.

La suite du manuel doit être enrichie par les parties suivantes :

- Partie II : Interfaces et ports
- Partie III : VLAN
- Partie IV : Trunk, DTP et VTP
- Partie V : Spanning Tree
- Partie VI : EtherChannel
- Partie VII : Sécurité des switches
- Partie VIII : Administration et accès distant
- Partie IX : Switching Layer 3
- Partie X : Fonctionnalités avancées
- Partie XI : Commandes de dépannage
- Partie XII : Travaux pratiques complets

Ce document a été créé dans le dépôt GitHub associé à ce projet et peut être complété chapitre par chapitre selon les besoins pédagogiques.

---

> Le livre est en cours de construction selon la méthode d’inventaire demandée. Les sections suivantes peuvent être ajoutées progressivement, en respectant strictement le modèle de documentation Cisco IOS / IOS XE.
