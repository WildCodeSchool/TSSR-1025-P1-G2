## Sommaire

1. [Prérequis technique](#prerequis-technique)
2. [Installation sur le serveur](#installation-sur-le-serveur)
3. [Installation sur le client](#installation-sur-le-client)
4. [FAQ](#faq)

# 1. Prérequis techniques

1. VM Client *Linux* : ubu01
2. VM Client *Windows 10/11* :  win01
3. VM Serveur *Debian* :  srvlx01
4. VM Serveur *Windows 22/25 GUI*   :  srvwin01

Les 4 VM sont connecté en réseau et se voit par leur nom.
<span id="prerequis-techniques"></span>

# 2. Installation sur le serveur
<span id="installation-sur-le-serveur"></span>

# 3. Installation sur le client
<span id="installation-sur-le-client"></span>
_________
### Installation du logiciel *John the ripper.*
_________

 Voici la ligne de commande pour l'installation de *John the ripper* :


	 sudo snap install john-the-ripper

	
- Cette méthode a le mérite d'installer une version récente et embarque davantage de bibliothèque, également plus de format supporté . Les mises à jour sont automatique.
	 - une fois la commande exécuté vous devriez avoir ce message :
	
	![exemple](Ressources/install_john_ok.png)


Si la commande **snap** ne fonctionne pas ,c'est parce que le paquet snap n'est pas installé sur votre distribution *Linux*

Dans ce cas veuillez tapé cette commande :


	sudo apt install snap



Une fois le paquet snap installé reporté vous au paragraphe 2 pour installé le logiciel *John the ripper*.

Ensuite il faut téléchargé une wordlist plus conséquente pour utilisé *john* tapons cette commande :

```
sudo snap install seclists
```

![texte](Ressources/install_seclists_ok.png)


Une fois *seclists* installé il faut aller chercher les listes de dictionnaire que nous avons besoins, nous en avons sélectionné deux :

La liste "000webhost.txt" :

```
cp /snap/seclists/1214/Passwords/Leaked-Databases/000webhost.txt ~/Documents/000webhost.txt

```

La liste "rockyou.txt" :

```
cp /snap/seclists/1214/Passwords/Leaked-Databases/rockyou.txt.tar.gz ~/Documents/rockyou.txt.tar.gz

```

Comme vous le voyez le fichier est compressé voici la commande pour le décompréssé :

```
tar -xzf rockyou.txt.tar.gz 
```


---
**POINT DE MONTAGE REPERTOIRE ENTRE WINDOWS ET LINUX**
---



  - Installé **Samba** sur votre distribution **Linux**
   
   Installons le paquet *Samba* avec cette ligne de commande :

```
sudo apt install samba

```

   -Activons le service,ainsi il va demarrer automatiquement au demarrage de la machine avec cette commande :


```
sudo systemctl enable smbd

```

 -  Création du dossier partagé sur *Windows*

    
Pour ce projet on va créé un dossier **C:\Commun**

On commence par créé le dossier à partir de l'Explorateur de fichiers:
	
Clic droit **Nouveau > Dossier.
	

![image](Ressources/dossier_partager_windows.png)	


Pour partagé le dossier suivons les étapes suivantes :
		
Faire un clic droit sur le dossier **Commun**,puis sélectionnez **Propriété**

![image](Ressources/Propriété_de_commun.png)



Cliquez sur l'onglet **Partage** ,puis **Partage avancé** et enfin cochez la case **Partage ce dossier**.Conservez le nom par defaut.


![image](Ressources/partage_avancé.png)

	
Cliquez sur **Autorisation**
	   
Veuillez à ajouter l'utilisateur qui doit avoir acces au partage,en lui donnant les autorisations de **Controle total**.

![photo](Ressources/autorisation.png)


Derniere manipulation sur **Windows** cliquez sur l'onglet **Sécurité**.Ajoutez l'utilisateur également ici et lui octroyer également toutes les autorisations à cet endroit.

![photo](Ressources/sécurité.png)

 - Création du dossier partagé et monter le partage dans le système de fichier dans votre distribution *Linux*

Création des dossiers commun PC UBUNTU et Serveur WINDOWS 

```
sudo mkdir /mnt/Commun/win01
sudo mkdir /mnt/Commun/win01/svrwin01
```

 - Installation du paquet **cifs-utils** (prise en charge du Samba sous Linux)


```
sudo apt install cifs-utils -y
```



- Commande à exécuter pour le montage de notre dossier Commun

```
sudo mount -t cifs //win01/Commun /mnt/Commun/win01 -o username=wilder
```


Vous devez maintenant saisir votre mot de passe Windows.



- Commande à exécuter pour lister le contenu de notre dossier Commun


```
ls /mnt/Commun/win01
```

 ![image](Ressources/cde-ls_win01.png)
 

- Il faut également  faire un point de montage avec le **Serveur Windows**

Commande à exécuter pour le montage de notre dossier Commun :

```
sudo mount -t cifs //svrwin01/Commun /mnt/Commun/win01/svrwin01 -o username=wilder
```

Vous devez maintenant saisir votre mot de passe Windows.

Commande à exécuter pour lister le contenu de notre dossier Commun :

```
ls -l /mnt/Commun/win01/svrwin01

```

photo : ls svrwin01

## Montage automatique au démarrage (Facultatif)

- Pour évité a chaque démarrage de votre machine de refaire les manipulations pour le montage des dossiers voici les étapes à effectuer :

```
sudo nano /etc/fstab
```

- Une fois dans ce fichier nous allons ajouter ces deux lignes :

```
//win01/Commun /mnt/Commun/win01 cifs credentials=/etc/smb-partage-creds 0 0
//svrwin01/Commun /mnt/Commun/win01/svrwin01 cifs credentials=/etc/smb-partage
```

- Ensuite , sauvegardez le fichier (**CTRL+0** puis **ENTER**) et quittez (**CTRL+X**)

- Maintenant, on va créé le fichier **/etc/smb-partage-creds**, il va nous servir à stocker les utilisateurs et mot de passe.

```
sudo nano /etc/smb-partage-creds
```

- Dans ce fichier indiquez le nom d'utilisateur et le mot de passe de votre compte Windows comme ceci :

```
username=wilder
password=Azerty1*
```

- Ensuite on enregistre et on ferme le fichier.

- Pour **éviter les accès non autorisés**,modifions les permissions sur ce fichier avec cette commande :

```
sudo chmod 600 /etc/smb-partage-creds
```

Effectuer le redémarrage de votre machine.
# 4. FAQ
<span id="faq"></span>
