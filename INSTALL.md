## Sommaire

1. [Prérequis technique](#prerequis-technique)
2. [Installation sur le serveur](#installation-sur-le-serveur)
3. [Installation sur le client](#installation-sur-le-client)
4. [FAQ](#faq)

# 1. Prérequis techniques
<span id="prerequis-techniques"></span>

# 2. Installation sur le serveur
<span id="installation-sur-le-serveur"></span>

### Pré-requis — se connecter en root / sudo

Travaille avec un compte ayant `sudo`, ou passe en root :

### Mettre à jour APT

```
sudo apt update
sudo apt upgrade -y
```

### Installation simple depuis les dépôts

```
sudo apt install -y hashcat hashcat-data
```

Vérification de l’installation :

```
hashcat --version
```

Le paquet officiel Debian inclut les données dans **hashcat-data**. 

### Tester Hashcat

#### Etalonnage :

```
hashcat -b
```

#### Informations sur le matériel de l'appareil :

```
hashcat -I
```

#### Aide :

```
hashcat --help
```
# 3. Installation sur le client
<span id="installation-sur-le-client"></span>

# 4. FAQ
<span id="faq"></span>