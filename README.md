![[read me premiere page.jpg]]

## Sommaire 

- [🎯 Présentation du projet](#presentation-du-projet)
- [📜 Introduction](#introduction)
- [👥 Membres du groupe par sprint](#membres-du-groupe-par-sprint)
- [⚙️ Choix Techniques](#choix-techniques)
- [🧗Difficultés rencontrées](#difficultes-rencontrees)
- [💡 Solutions trouvées](#solutions-trouvees)
- [🚀 Améliorations possibles](#ameliorations-possibles)

# 🎯 Présentation du projet
<span id="presentation-du-projet"></span>
**Sujet choisi** 
# Audit de robustesse de mots de passe

## **Présentation**

**Tâche principale** : Audit de robustesse de mots de passe
Les attaques se font depuis les systèmes Linux vers les systèmes Windows 
Les attaques ciblent des fichiers protégés par mot de passe
Tâche secondaire : Audit de robustesse sur le mot de passe d'un utilisateur local

### Détail de la tâche principale :
Le logiciel John the Ripper est installé sur un client Linux
Utilisation d’attaque par force brut et par dictionnaire
Le logiciel Hashcat est installé sur un serveur Linux
Utilisation de masques d’attaque
Les fichiers cibles (accessible de base) sont :
“fichier1.zip” mis sur un client Windows
“fichier2.zip” mis sur un serveur Windows

### Détail de la tâche secondaire :
Effectuer des attaques sur le mot de passe d’un compte local du serveur

 
🎯 Objectifs

## ligne de Défense
Les mots de passe constituent une ligne de défense contre les attaques de données informatiques à l'intérieur d'un réseau local. Ce n'est pas la seule , VPN, Pare feu etc protégent nos réseaux  mais du point de vue fichier utilisateur c'est la première ligne.  
## l'Audit : évaluation
Le rôle de cet audit va donc être d'évaluer la robustesse des mots de passe utilisés sur les fichiers utilisateurs du parc informatique .
Pour cela nous sommes équipé de deux machines virtuelles pouvant générer des listes de mots de passe grâçe à deux logiciels : **John the ripper et Haschcat**.
## l'Audit : recommandations
Si les mots de passes utilisés ne sont pas assez solides , nos deux méthodes d'attaques vont les récupérer rapidement.
Cette approche permet d'examiner les mots de passe existants et de proposer des recommandations pour renforcer la sécurité des données.



## Organisation du travail au sein du groupe



⚙️ Méthodologie


Tests d’attaque simulés : dictionnaires, hybrides brute-force.

🧠 Sensibilisation et amélioration continue

.


# 📜 Introduction
<span id="introduction"></span>

# 👥 Membres du groupe par sprint
<span id="membres-du-groupe-par-sprint"></span>
## **Sprint 1**

|  Franck Paisant  |     PO     | Dialogue avec dominique /mise en place du logiciel  Hashcat/                |
| :--------------: | :--------: | --------------------------------------------------------------------------- |
| Frederick flavil |     SM     | Création du tableau Trello/mise en place du logiciel John the Ripper/       |
|  Renaud Michel   | Technicien | rédaction du fichier Readme/ recherche sur le chiffrement des mots de passe |
### PO-SM-TEC

Franck notre PO ( product owner) a bien cerné le projet et les incertitudes du débuts ont été levées après plusieurs discussions avec Dominique notamment sur le rôle un peu flou de chaque machine au début.

Frederick notre SM( srum master ) en organiseur force tranquille  nous a bien installé et guidé dans nos rôle à chacun .


le  rôle de Renaud notre tec a été de faire des recherches sur le chiffrement des mots de passe. 
En partant de logiciel de compression et de protection , il a fait des recherches sur les manières de gérer les mots de passe de leurs créations à leurs sauvegardes .


Franck et Fréderick se sont penchés sur la mise en place d'outils permettants l'analyse de la protection des données .



## **Sprint 2**

| Membre           | Rôle       | Missions                                                       |
| ---------------- | ---------- | -------------------------------------------------------------- |
| Franck Paisant   | Technicien | Finalisation de la doc et du user guide de John  the Ripper    |
| Frederick flavil | SM         | Mise en place et protocole d'attaque avec Hashcat              |
| Renaud Michel    | PO         | test solution logicielle mise en place par Franck et Frederick |
 Cette deuxième semaine de projet va nous permettre de finaliser l'attaque avec le logiciel john the Ripper, nous avons tous mis en place le dispositif établi par Franck et nous avons réussi le cassage du hash pour des mots de passe simple .
 Avec l'utilisation du logiciel 7 zip nous avons convenu de protéger les deux fichiers en type ;zip et chiffrage en AES 256.
 John the ripper , lorsqu'il visualise le fichier .zip reconnait les caracteristiques de ces protections et nous propose de les utiliser en option . Son utilisation est plutôt simple une fois le fichier récuperé et le hash sorti .

# ⚙️ Choix techniques
<span id="choix-techniques"></span>
## **Matériel**

Pour effectuer ce projet, nous avons 4 machines virtuelles connectées entre elle sur un réseau local 172.16.10.0/24

Une machine sous Windows serveur "SRVWIN01"  ip local:172.16.10.5 
Une machine sous Linux Debian "SRVLX01" ip local 172.16.10.6 
Une machine sous Windows 11" WIN01" ip local 172.16.10.10 
Une machine sous Ubuntu" UBU01" ip local 172.16.10.20 

**Logiciel**
Pour compresser les fichiers : 7.zip
Génération de code sur le site de la CNIL
Le logiciel John the Ripper est installé sur un client Linux 
Le logiciel Hashcat est installé sur un serveur Linux Debian
le logiciel Semba pour permettre à UBU01 de récupérer le file1.zip sur WIN 01
*John the ripper* : est un outil open source conçu pour casser des mots de passe, c’est-à-dire retrouver le mot de passe original à partir de son empreinte (ou _hash_). Il fonctionne en testant rapidement des milliers, voire des millions de combinaisons, grâce à différentes techniques comme les attaques par dictionnaire ou force brute.

photo : icone_John_The_Ripper


# 🧗 Difficultés rencontrées

*John the ripper* ,pour une attaque par dictionnaire la liste original de *John* est trop limité
Avoir des listes de mots de dictionnaire plus conséquentes
Communication entre le PC client Linux et le PC client et serveur Windows
<span id="difficultes-rencontrees"></span>

# 💡 Solutions trouvées

*john* = téléchargement d'une wordlist plus conséquentes pour que l'attaque soit plus efficace
Installation du paquet seclists
Installation de Samba et de cifs sur pc client Linux
<span id="solutions-trouvees"></span>

# 🚀 Améliorations possibles
<span id="ameliorations-possibles"></span>

[^1]: 
