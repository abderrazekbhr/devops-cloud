# Rapport : TP Zabbix

## 1. Introduction
Zabbix est une solution de supervision open-source permettant de surveiller les performances et la disponibilité des systèmes, réseaux, et applications. Ce TP a pour objectif de déployer et configurer Zabbix à l'aide d'Ansible pour automatiser le processus.

---

## 2. Structure du projet
Le projet est organisé comme suit :

- **Playbook principal** : `playbook.yml`
  - Contient les tâches principales pour installer et configurer Zabbix.
- **Rôles** :
  - `roles/zabbix` :
    - `tasks/main.yml` : Définit les étapes d'installation et de configuration.
    - `defaults/main.yml` : Contient les variables par défaut pour personnaliser le déploiement.
    - `handlers/main.yml` : Gère les redémarrages des services si nécessaire.
    - `vars/main.yml` : Variables spécifiques au rôle.
    - `meta/main.yml` : Métadonnées du rôle.
- **Inventaire** : `hosts.yml`
  - Définit les machines cibles pour le déploiement.

---

## 3. Méthodologie

### 3.1 Installation de Zabbix
- **Tâches principales** :
  - Mise à jour des dépôts et installation des dépendances nécessaires.
  - Installation du serveur Zabbix, de l'agent et de la base de données (MySQL/PostgreSQL).
  - Configuration des fichiers principaux de Zabbix (zabbix_server.conf, zabbix_agentd.conf).
  - Démarrage et activation des services Zabbix et base de données.

### 3.2 Configuration de l'agent Zabbix
- **Objectif** : Permettre à chaque machine supervisée de communiquer avec le serveur Zabbix.
- **Étapes** :
  - Installation de l'agent Zabbix sur les machines cibles.
  - Configuration du fichier `zabbix_agentd.conf` pour spécifier l'adresse du serveur Zabbix.
  - Redémarrage du service Zabbix Agent.

---

## 4. Inventaire utilisé
- **Fichier** : `hosts.yml`
- **Contenu** :
```yaml
---
all:
  hosts:
    vm-alpha:
      ansible_host: 35.241.224.131
    vm-beta:
      ansible_host: 34.38.123.95
    vm-gamma:
      ansible_host: 35.205.215.122
```
- **Description** :
  - Trois machines virtuelles (VM) créées sur Google Cloud Platform (GCP).
  - `ma propre machine`: Serveur Zabbix principal.
  - `vm-alpha` `vm-beta` et `vm-gamma` : Agents supervisés.

---

## 5. Résumé des tâches principales
| **Tâche**                  | **Description**                                                                 |
|----------------------------|---------------------------------------------------------------------------------|
| Installation du serveur    | Installation et configuration de Zabbix Server et de la base de données.       |
| Installation des agents    | Déploiement et configuration des agents Zabbix sur les machines supervisées.   |
| Tests et validation        | Vérification de la connectivité et de la remontée des données dans Zabbix.     |

---

## 6. Conclusion
Ce TP a permis de mettre en œuvre une solution complète de supervision avec Zabbix en utilisant Ansible pour automatiser le déploiement et la configuration. Les rôles et playbooks définis assurent une modularité et une réutilisabilité pour des projets futurs. Les tests réalisés sur les machines GCP ont validé le bon fonctionnement de la solution.