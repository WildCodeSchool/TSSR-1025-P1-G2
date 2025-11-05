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

	```
	 sudo snap install john-the-ripper
	```	
	
- Cette méthode a le mérite d'installer une version récente et embarque davantage de bibliothèque, également plus de format supporté . Les mises à jour sont automatique.
	 - une fois la commande exécuté vous devriez avoir ce message :
	
		 photo install john ok

Si la commande **snap** ne fonctionne pas ,c'est parce que le paquet snap n'est pas installé sur votre distribution *Linux*

Dans ce cas veuillez tapé cette commande :

	```
	sudo apt install snap
	```

Une fois le paquet snap installé reporté vous au paragraphe 2 pour installé le logiciel *John the ripper*.

Ensuite il faut téléchargé une wordlist plus conséquente pour utilisé *john* tapons cette commande :

```
sudo snap install seclists
```


      photo : install seclist


Dernière commande avant de pouvoir utiliser  *john* , on copie une liste de **Mots De Passe** sur notre bureau :


# 4. FAQ
<span id="faq"></span>