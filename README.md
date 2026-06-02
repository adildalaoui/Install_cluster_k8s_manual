# 🚀 Déploiement d'une Application sur Kubernetes avec Kubeadm

## 📖 Présentation

Ce projet a pour objectif de mettre en place un cluster Kubernetes manuellement à l'aide de **Kubeadm**, puis de déployer une application conteneurisée dans un environnement Kubernetes.

L'objectif est de comprendre les composants principaux de Kubernetes, la mise en place d'un cluster, la gestion du réseau des Pods et le déploiement d'une application en utilisant les bonnes pratiques DevOps.

---

# 🏗️ Architecture

```text
Utilisateur
     |
     v
+----------------------+
| Service Kubernetes   |
| LoadBalancer         |
+----------+-----------+
           |
           v
+----------------------+
| Deployment           |
| Replicas : 2         |
+----------+-----------+
           |
     +-----+-----+
     |           |
     v           v
+---------+ +---------+
|  Pod 1  | |  Pod 2  |
+---------+ +---------+
```

---

# ⚙️ Technologies utilisées

- Ubuntu Server
- Kubernetes
- Kubeadm
- Kubelet
- Kubectl
- Containerd
- Calico CNI
- Git
- GitHub

---

# ☸️ Les composants Kubernetes

## Kubeadm

Kubeadm est l'outil utilisé pour créer et initialiser un cluster Kubernetes.

Il permet notamment :

- La création du Control Plane
- La génération des certificats Kubernetes
- La configuration des composants du cluster
- L'ajout des nœuds Workers

Exemple :

```bash
sudo kubeadm init --pod-network-cidr=192.168.0.0/16
```

---

## Kubelet

Kubelet est un agent exécuté sur chaque nœud du cluster.

Son rôle est de :

- Communiquer avec l'API Kubernetes
- Lancer les Pods
- Surveiller les conteneurs
- Remonter l'état du nœud au cluster

---

## Kubectl

Kubectl est l'outil en ligne de commande permettant d'administrer Kubernetes.

Exemples :

```bash
kubectl get nodes
kubectl get pods
kubectl get services
kubectl logs <pod-name>
```

---

## Containerd

Containerd est le runtime de conteneurs utilisé par Kubernetes.

Il est responsable de :

- Télécharger les images
- Créer les conteneurs
- Exécuter les Pods
- Gérer le cycle de vie des conteneurs

---

## Calico

Calico est le plugin réseau (CNI) utilisé dans ce projet.

Il permet :

- La communication entre les Pods
- La communication entre les nœuds
- La gestion des adresses IP
- L'application des politiques réseau

---

# 🔧 Mise en place du cluster

## 1. Préparation des nœuds

Sur tous les serveurs :

- Mise à jour du système
- Désactivation du Swap
- Configuration du noyau Linux
- Activation du routage IP

---

## 2. Installation de Containerd

```bash
sudo apt install -y containerd.io
```

Configuration du pilote Systemd :

```bash
SystemdCgroup = true
```

---

## 3. Installation des composants Kubernetes

```bash
sudo apt install -y kubelet kubeadm kubectl
```

---

## 4. Initialisation du cluster

```bash
sudo kubeadm init --pod-network-cidr=192.168.0.0/16
```

---

## 5. Installation du réseau Calico

```bash
kubectl apply -f calico.yaml
```

---

## 6. Ajout des nœuds Workers

```bash
kubeadm join <MASTER-IP>:6443 --token <TOKEN> --discovery-token-ca-cert-hash sha256:<HASH>
```

---

# 🚀 Déploiement de l'application

Création du namespace :

```bash
kubectl create namespace webapps
```

Déploiement :

```bash
kubectl apply -f deployement-service.yaml -n webapps
```

Vérification :

```bash
kubectl get all -n webapps
```

---

# 🔍 Vérification du cluster

Afficher les nœuds :

```bash
kubectl get nodes
```

Afficher les Pods :

```bash
kubectl get pods -n webapps
```

Afficher les services :

```bash
kubectl get svc -n webapps
```

Afficher les événements d'un Pod :

```bash
kubectl describe pod <pod-name> -n webapps
```

Afficher les logs :

```bash
kubectl logs <pod-name> -n webapps
```

---

# 📸 Résultat

Après le déploiement :

✅ Cluster Kubernetes opérationnel

✅ Réseau Calico fonctionnel

✅ Application déployée avec succès

✅ Réplication des Pods

✅ Service exposé et accessible

---

# 🧠 Compétences démontrées

- Administration Linux
- Kubernetes
- Containerd
- Réseau Kubernetes
- Déploiement d'applications conteneurisées
- Troubleshooting Kubernetes
- Git & GitHub
- DevOps

---




**Adil Dalaoui**

