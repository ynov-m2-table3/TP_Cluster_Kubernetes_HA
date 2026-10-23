# TP_Cluster_Kubernetes_HA
TP_Cluster_Kubernetes_HA

# 1.2 : Swap, modules noyau, sysctl

## Contexte SWAP

Le swap sous Linux est un espace de stockage sur le disque (partition dédiée ou fichier) utilisé comme extension de la mémoire vive (RAM). Il sert à stocker les données inactives pour libérer de la RAM ou à permettre la mise en hibernation du système.

## Q1 : 

Le swap est désactivé afin d'assurer des limites de mémoire prévisibles pour le cluster. Le composant kubelet doit gérer précisément les ressources allouées à chaque conteneur.

Si le système d'exploitation bascule de la RAM vers le disque dur (swap), les performances des applications se dégradent de manière aléatoire et Kubernetes perd sa capacité à isoler, mesurer et expulser correctement les Pods en cas de surcharge mémoire

# 1.3 

## Q2

L'option SystemdCgroup = true indique au moteur d'exécution containerd d'utiliser le gestionnaire natif de Linux (systemd) pour gérer les cgroups (les limites de CPU et de mémoire allouées aux conteneurs). Il est impératif d'aligner ce paramètre avec kubelet (l'agent de Kubernetes). Si kubelet utilise systemd alors que containerd utilise un autre gestionnaire (comme cgroupfs), la double gestion entraînera une instabilité du système et une incapacité à expulser proprement les Pods en cas de surcharge.
