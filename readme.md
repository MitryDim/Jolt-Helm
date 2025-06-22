# JOLT_KUBE Helm Chart

Ce dépôt contient le chart Helm pour déployer l’application **JOLT_KUBE** sur Kubernetes.

## Prérequis

- [Helm](https://helm.sh/) 3.x
- Un cluster Kubernetes fonctionnel

## Installation

```bash
helm repo add jolt-kube https://votre-repo-helm-url/
helm install jolt-kube jolt-kube/jolt-kube
```

## Configuration

Vous pouvez personnaliser le déploiement en modifiant le fichier `values.yaml` ou en passant des valeurs via la ligne de commande :

```bash
helm install jolt-kube jolt-kube/jolt-kube --set key=value
```

## Mise à jour

```bash
helm upgrade jolt-kube jolt-kube/jolt-kube
```

## Désinstallation

```bash
helm uninstall jolt-kube
```

## Installation avec kubectl (sans Helm)

Générez les manifests puis appliquez-les :

```bash
helm template jolt-kube . > all.yaml
kubectl apply -f all.yaml
```

## Structure du Chart

- `Chart.yaml` : Métadonnées du chart
- `values.yaml` : Valeurs de configuration par défaut
- `templates/` : Manifests Kubernetes templates

## Licence

Ce projet est sous licence MIT.
