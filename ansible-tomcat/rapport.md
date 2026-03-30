# Rapport : Configuration et déploiement Tomcat

## 1. Déploiement par `webapps`
- **Playbook utilisé** : `playbook_full_tomcat_webapps.yml`
- **Méthode** :
  - L'application est copiée directement depuis un fichier `.war` (exemple : `sample.war`) vers le répertoire `webapps` de Tomcat.
  - Utilisation de la tâche `copy` pour transférer le fichier `.war` dans `/opt/tomcat/webapps/`.
  - Tomcat détecte automatiquement le fichier `.war` et déploie l'application.
- **Avantages** :
  - Simple et rapide.
  - Pas besoin de configuration supplémentaire.
- **Inconvénients** :
  - Moins flexible pour des configurations avancées.

---

## 2. Création de contextes XML dans un seul playbook
- **Playbook utilisé** : `playbook_full_tomcat_xml.yml`
- **Méthode** :
  - Les fichiers de configuration XML (exemple : `context.xml`) sont créés pour chaque application.
  - Ces fichiers sont placés dans le répertoire `/opt/tomcat/conf/Catalina/localhost/`.
  - Utilisation de la tâche `template` ou `copy` pour gérer les fichiers XML.
- **Avantages** :
  - Permet une configuration fine des applications (exemple : gestion des ressources, chemins spécifiques, etc.).
  - Utile pour des déploiements complexes.
- **Inconvénients** :
  - Nécessite une gestion manuelle des fichiers XML.

---

## 3. Structuration par rôles
- **Point d'entrée** : `playbook-main.yml`
- **Méthode** :
  - Structuration des tâches dans des rôles pour une meilleure organisation et réutilisabilité.
  - Rôles définis :
    - **`roles/tomcat`** : Installation et configuration de Tomcat.
    - **`roles/tomcat_webapps`** : Déploiement des applications via `webapps`.
    - **`roles/tomcat_xml`** : Gestion des fichiers de configuration XML.
  - Le fichier `playbook-main.yml` appelle les rôles nécessaires en fonction des besoins.
- **Avantages** :
  - Organisation claire et modulaire.
  - Réutilisation des rôles dans d'autres projets.
  - Maintenance simplifiée.
- **Inconvénients** :
  - Nécessite une structuration initiale plus complexe.

---

## Inventaire utilisé
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
  - Chaque VM est utilisée pour tester les différentes méthodes de déploiement.

---

## Résumé des méthodes
| **Méthode**          | **Playbook**                     | **Description**                                                                 |
|-----------------------|----------------------------------|---------------------------------------------------------------------------------|
| Déploiement `webapps` | `playbook_full_tomcat_webapps.yml` | Copie directe des fichiers `.war` dans le répertoire `webapps`.                 |
| Configuration XML     | `playbook_full_tomcat_xml.yml`    | Création de fichiers `context.xml` pour chaque application.                     |
| Structuration par rôles | `playbook-main.yml`              | Organisation des tâches dans des rôles pour une meilleure modularité et clarté. |

---

## Conclusion
Votre travail est bien structuré et couvre plusieurs approches pour le déploiement et la configuration de Tomcat :
1. Une méthode simple et rapide via `webapps`.
2. Une méthode avancée et flexible via des fichiers XML.
3. Une structuration modulaire et réutilisable via des rôles.

Ces approches permettent de répondre à différents besoins et scénarios de déploiement.