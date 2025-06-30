<h1 align="center">
  <img src="https://img.icons8.com/color/96/000000/electric-scooter.png" width="48" alt="Jolt Logo"/>
  <br>
  JOLT_KUBE - Chart Helm Microservices
</h1>

<p align="center">
  <strong>Déploiement Kubernetes de l’architecture microservices Jolt.</strong><br>
  Helm chart pour orchestrer Gateway, Auth, Users, Vehicles, Navigate, Maintains et Notifications.<br>
  <a href="https://github.com/Valt1-0/Jolt-API">Voir la version microservices</a>
</p>

<p align="center">
  <a href="./LICENSE">
    <img src="https://img.shields.io/badge/license-MIT-blue.svg" alt="MIT License" />
  </a>
  <img src="https://img.shields.io/badge/Helm-3%2B-blue" alt="Helm" />
  <img src="https://img.shields.io/badge/Kubernetes-1.24%2B-blueviolet" alt="Kubernetes" />
  <img src="https://img.shields.io/badge/MongoDB-5%2B-brightgreen" alt="MongoDB" />
  <img src="https://img.shields.io/badge/RabbitMQ-AMQP-orange" alt="RabbitMQ" />
  <img src="https://img.shields.io/badge/Redis-OK-red" alt="Redis" />
  <img src="https://img.shields.io/badge/status-en%20développement-yellow" alt="Status" />
</p>

<h3 align="center">
  <a href="#-présentation">Présentation</a>
  <span> · </span>
  <a href="#-architecture">Architecture</a>
  <span> · </span>
  <a href="#-installation">Installation</a>
  <span> · </span>
  <a href="#️-configuration">Configuration</a>
  <span> · </span>
  <a href="#-contribution">Contribution</a>
</h3>

---

## ✨ Présentation

**JOLT_KUBE** est un chart Helm prêt à l’emploi pour déployer l’architecture microservices Jolt sur Kubernetes.  
Chaque microservice dispose de sa propre base MongoDB, communique via HTTP et RabbitMQ, et bénéficie d’une configuration centralisée et sécurisée.

---

## 🏗️ Architecture

- **Gateway** : API Gateway, point d’entrée unique.
- **Auth** : Authentification, gestion JWT, sessions, sécurité.
- **Users** : Gestion des utilisateurs, profils, rôles.
- **Vehicles** : Gestion des véhicules, images, historique.
- **Navigate** : Gestion des trajets, groupes, géolocalisation.
- **Maintains** : Gestion des maintenances, historiques, notifications.
- **Notifications** : Emails transactionnels et notifications push Expo.

Chaque microservice a son propre Service, Deployment, PVC MongoDB, et ses variables d’environnement.

---

## 🚦 Badges d’état

| Service       | Port | Statut                                                                      |
| ------------- | ---- | --------------------------------------------------------------------------- |
| Gateway       | 5000 | ![Gateway](https://img.shields.io/badge/Gateway-OK-brightgreen)             |
| Auth          | 5002 | ![Auth](https://img.shields.io/badge/Auth-OK-brightgreen)                   |
| Users         | 5003 | ![Users](https://img.shields.io/badge/Users-OK-brightgreen)                 |
| Vehicles      | 5004 | ![Vehicles](https://img.shields.io/badge/Vehicles-OK-brightgreen)           |
| Maintains     | 5005 | ![Maintains](https://img.shields.io/badge/Maintains-OK-brightgreen)         |
| Navigate      | 5006 | ![Navigate](https://img.shields.io/badge/Navigate-OK-brightgreen)           |
| Notifications | 5001 | ![Notifications](https://img.shields.io/badge/Notifications-OK-brightgreen) |

---

## 📋 Prérequis

- **Helm** 3.x
- **Kubernetes** 1.24+
- **MongoDB** (déployé automatiquement)
- **RabbitMQ** (déployé automatiquement)
- **Redis** (déployé automatiquement)

---

## 🚀 Installation

1. **Cloner le dépôt Helm :**

   ```bash
   git clone https://github.com/votre-utilisateur/jolt-kube-helm.git
   cd jolt-kube-helm
   ```

2. **Installer le chart sur votre cluster :**

   ```bash
   helm install jolt-kube .
   ```

   > Personnalisez le fichier `values.yaml` avant installation si besoin.

3. **Mettre à jour le chart :**

   ```bash
   helm upgrade jolt-kube .
   ```

4. **Désinstaller :**

   ```bash
   helm uninstall jolt-kube
   ```

---

## ⚡ Installation avec kubectl (sans Helm)

Générez les manifests puis appliquez-les :

```bash
helm template jolt-kube . > all.yaml
kubectl apply -f all.yaml
```

---

## ⚙️ Configuration

- Modifiez `values.yaml` pour adapter les images, ports, secrets, variables d’environnement, etc.
- Vous pouvez aussi surcharger des valeurs à l’installation :

  ```bash
  helm install jolt-kube . --set microservices[0].image=ghcr.io/monuser/gateway:latest
  ```

---

## 🗂 Structure du Chart

- `Chart.yaml` : Métadonnées du chart
- `values.yaml` : Valeurs de configuration par défaut
- `templates/` : Manifests Kubernetes templates (Deployments, Services, PVC, Secrets…)

---

## 🔑 Exemples de variables d’environnement

Chaque microservice reçoit automatiquement ses variables d’environnement via Helm et Kubernetes Secrets.  
Voir le fichier [`values.yaml`](./values.yaml) pour la structure complète.

<details>
<summary><strong>Exemple pour Auth</strong></summary>

```yaml
env:
  - name: API_PORT
    value: "5002"
  - name: JWT_ACCESS_KEY
    valueFrom:
      secretKeyRef:
        name: auth-secret
        key: JWT_ACCESS_KEY
  - name: MSG_QUEUE_URL
    valueFrom:
      secretKeyRef:
        name: auth-secret
        key: MSG_QUEUE_URL
  # ...
```
</details>

---

## 💡 Bonnes pratiques

- **Ne versionnez jamais de secrets réels dans Git.**
- **Adaptez les ressources (CPU, mémoire, stockage) selon vos besoins.**
- **Utilisez des StorageClass compatibles avec votre cluster pour la persistance MongoDB, Redis, RabbitMQ.**
- **RabbitMQ et Redis sont nécessaires pour la communication inter-services et la gestion des sessions.**

---

## 🤝 Contribution

1. Fork le projet
2. Crée une branche (`git checkout -b feature/ma-feature`)
3. Commit tes modifications (`git commit -am 'Ajout de ma feature'`)
4. Push la branche (`git push origin feature/ma-feature`)
5. Ouvre une Pull Request

---

## 📄 Licence

Ce projet est sous licence MIT. Voir le fichier [LICENSE](./LICENSE) pour plus d’informations.

---

<p align="center">
Pour toute question, contacte l’équipe Jolt à <a href="mailto:contact@joltz.fr">contact@joltz.fr</a>