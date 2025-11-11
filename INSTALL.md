## Sommaire

1. [Prérequis technique](#prerequis-technique)
2. [Installation sur le serveur](#installation-sur-le-serveur)
3. [Installation sur le client](#installation-sur-le-client)
4. [FAQ](#faq)

# 1. Prérequis techniques

<span id="prerequis-techniques"></span>
- avoir un accès internet !

# 2. Installation sur  Windows  10 / 11 et Serveur


## ** Installation manuelle **
<span id="installation-sur-le-serveur"></span>
Le site officiel : [https://www.7-zip.org](https://www.7-zip.org)

![[page de telechargement 7zip.png]](Ressources/page_de_telechargement_7zip.png)



1. Télécharge la version correspondant à ton système :
    
2. Exécute le fichier `.exe` téléchargé avec un clic droit → **Exécuter en tant qu’administrateur**.
    
3. Clique sur **Install**, puis sur **Close** une fois terminé.

 *7-Zip s’ajoute automatiquement au menu clic droit de l’Explorateur.*

## ** Installation via PowerShell avec Winget **

Si **Winget** est disponible (Windows Server 2022, 2025, ou si tu l’as ajouté manuellement) :

````
winget install 7zip.7zip

````

   *7-Zip s’ajoute automatiquement au menu clic droit de l’Explorateur.*


## ** Installation sur Ubuntu **



````
sudo apt-get install p7zip
````



###  A SAVOIR: 
p7zip-full fournit 7za et 7z qui gèrent non seulement les archives 7z mais aussi les archives ZIP, Zip64, CAB, ARJ, GZIP, BZIP2, TAR, CPIO, RPM, ISO, DEB et RAR (si le paquet non-libre p7zip-rar est installé). Ce paquet est également nécessaire pour une bonne gestion des mots de passes (creation et extraction)

 Quelques exemples :

**Lister le contenu d'une archive :**

```
7z l <archive>
```


Décompresser une archive sans respecter l'arborescence des fichiers extraits :

```
7z e <archive>
```


Décompresser une archive en respectant l'arborescence des fichiers (crée un fichier du nom de l'archive contenant les fichiers extraits) :

```
7z x <archive>
```

Créer une archive 7-Zip avec un mot de passe (le mot de passe est demandé pour extraire les fichiers) :


```
7z a -pMot_De_Passe <archive> <fichiers>
``` 

Créer une archive 7-Zip avec un mot de passe et le chiffrement des noms de fichiers 
(le mot de passe est demandé pour afficher les fichiers contenu dans l'archive) :


```
7z a -mhe=on -pMot_De_Passe <archive> <fichiers>
``` 




# 4. FAQ
<span id="faq"></span>
