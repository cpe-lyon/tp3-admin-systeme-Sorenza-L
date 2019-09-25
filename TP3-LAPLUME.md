`Sorenza Laplume`

# Compte Rendu

# TP3 - Gestion des paquets

## Exercice 1. Commandes de base

### 1. Quels sont les 5 derniers paquets installés sur votre machine ?

Pour savoir  quels sont les 5 derniers paquets installés sur ma machine j'utilise la commande : ***grep "installed" /var/log/dgkp.log | tail -5***

> 240-6ubuntu5.7
> 2.8.5-2
> 0.9.4-1ubuntu1
> 1.12.12-1ubuntu1.1
> 0.131ubuntu19.1

### 2. Utiliser dpkg et apt pour compter le nombre de paquets installés (ne pas hésiter à consulter le manuel !).Comment explique-t-on la (petite) différence de comptage ?

Il y a 514 paquets installés quand j'utilise ***dpkg -l***
Il y a 515 paquet installés quand j'utilise ***apt list | wc -l***
La différence de comptage est surement faite parce que dpkg ne gère pas les dépendances.

### 3. Combien de paquets sont disponibles en téléchargement ?

Il y a 63603 paquets disponibles en téléchargement


### 4. Créer un alias “maj” qui met à jour le système.

Pour créer l'alias ***maj*** on va dans le fichier ***.bashrc*** on ajoute un ***alias maj='sudo apt-get upgrade'*** puis l'on met à jour ce fichier avec la commande ***source ~/.bashrc***.

### 5. A quoi sert le paquet fortunes ? Installez-le.

Le paquet fortunes sert à affichés un petits messages, citations, proverbes, etc à chaque connexion en mode console.

### 6. Quels paquets proposent de jouer au sudoku ?

Ce logiciel est installé par défaut dans Ubuntu. Pour l'installer sous d'autres environnements de bureau, il suffit d'installer le paquet ***apt-get gnome-sudoku*** et sur Kubuntu il faut installer ***apt-get ksudoku***.

### 7. Lister les derniers paquets installés explicitement avec la commande apt install




## Exercice 2.

### A partir de quel paquet est installée la commande ls ? Comment obtenir cette information en une seule commande, pour n’importe quel programme (indice : la réponse est dans le poly de cours 2, dans la liste des commandes utiles) ? Utilisez la réponse a pour écrire un script appelé origine-commande (sans l’extension.sh) prenant en argument le nom d’une commande, et indiquant quel paquet l’a installée.

Il faut utilisé : ***which -a ls | tail -1 | xargs dpkg -S*** nous avons comme réponse à cette requête ***coreutils : /bin/ls***.
<pre>
 #!/bin/bash
  2 #Script origine-commande
  3
  4 commande="$1"
  5
  6 origine="Which -a $1 | tail -1 | xargs dpkg -S"
  7
  8 echo $origine
</pre>

## Exercice 3.

### Ecrire une commande qui affiche “INSTALLÉ” ou “NON INSTALLÉ” selon le nom et le statut du package spécifié dans cette commande.

(dpkg -l "nom_package" | grep "^ii") && echo "installé"
|| echo "non installé"

## Exercice 4.

### Lister les programmes livrés avec coreutils. A quoi sert la commande ’[’ et comment afficher ce qu’elle retourne ?
Pour lister les paquets livrés avec coreutils j'utilise la commande :***apt show coreutils**
La commande ***'['*** est un synonyme de la commande  test en comparant une valeur.

## Exercice 5. aptitude

### Installez le paquet emacs à l’aide de la version graphique d’aptitude.

## Exercice 6. Installation d’un paquet par PPA
Certains logiciels ne figurent pas dans les dépôts officiels. C’est le cas par exemple de la version ”officielle”
de Java depuis qu’elle est développée par Oracle. Dans ces cas, on peut parfois se tourner vers un ”dépôt
personnel” ou PPA.
### 1. Installer la version Oracle de Java (avec l’ajout des PPA)
sudo add-apt-repository ppa:linuxuprising/java
sudo apt update
sudo apt install oracle-java11-installer
### 2. Vérifiez qu’un nouveau fichier a été créé dans /etc/apt/sources.list.d. Que contient-il ?

## Exercice 7. Création de dépôt personnalisé
Dans cet exercice, vous allez créer vos propres paquets et dépôts, ce qui vous permettra de gérer les
programmes que vous écrivez comme s’ils provenaient de dépôts officiels.
Création d’un paquet Debian avec dpkg-deb
### 1. Dans le dossier scripts créé lors du TP 2, créez un sous-dossier origine-commande où vous créerez un sous-dossier DEBIAN, ainsi que l’arborescence usr/local/bin où vous placerez le script écrit à l’exercice 2
### 2. Dans le dossier DEBIAN, créez un fichier control avec les champs suivants :
