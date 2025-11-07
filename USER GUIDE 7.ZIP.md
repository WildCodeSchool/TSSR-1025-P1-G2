## Sommaire

1. [Utilisation de base](#utilisation-de-base)
2. [Utilisation avancée](#utilisation-avancee)
3. [FAQ](#faq)

# 1. Utilisation de base

Pour une utilisation sans chiffrement , nous allons pouvoir créer une archive d'un dossier ou d'un fichier avec la possibilité de compresser ces données et de diminuer son poids .
## Faire une archive 
Clic droit sur l'objet à compresser choisissant **7-Zip → Ajouter à l’archive…**.
Dans la fenêtre qui s’ouvre, sélectionne le **format ZIP** si tu veux que ton archive soit compatible partout, ou **7z** si tu préfères une meilleure compression et laisse la case mot de passe vide.
Laisse le **niveau de compression** sur _Normal_, la **méthode de compression** sur _LZMA_ et le **mode de mise à jour** sur _Ajouter et remplacer les fichiers_.  
![[Ressources/util de base.png]]
##  Extraire une archive
 Clic droit dessus et choisis **Extraire ici** pour tout décompresser dans le dossier actuel, ou **Extraire vers "Nom_du_dossier"** pour créer un dossier dédié.
Si tu veux mettre à jour une archive existante, relance la commande **Ajouter à l’archive…** depuis le dossier d’origine et garde le mode _Ajouter et remplacer les fichiers_.
Enfin, tu peux ouvrir une archive avec **7-Zip → Ouvrir l’archive** pour en afficher le contenu, tester son intégrité ou supprimer certains fichiers sans tout extraire.

# 2. Utilisation avancée

## Remarques sur la compression  

Nous avons vu dans la partie _utilisation de base_ que outre la création d'un mot de passe de l'archive , 7.zip est aussi un outil pour compresser en taille les fichiers.
il applique plusieurs méthodes dont voici le résumé en anglais
il est donc possible de choisir et de regler le taux de compression ( ratio) .

| Method    | Description                                                                                                                                                                                                                                                                                                                                                                                        |
| --------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| LZMA      | It's base compression method for 7z format. Even old versions of 7-Zip can decompress archives created with LZMA method. It provides high compression ratio and very fast decompression.                                                                                                                                                                                                           |
| LZMA2     | Default compression method of 7z format. LZMA2 is LZMA-based compression method. It provides better multithreading support than LZMA. But compression ratio can be worse in some cases. For best compression ratio with LZMA2 use 1 or 2 CPU threads. If you use LZMA2 with more than 2 threads, 7-zip splits data to chunks and compresses these chunks independently (2 threads per each chunk). |
| PPMd      | Dmitry Shkarin's PPMdH algorithm with small changes. Usually it provides high compression ratio and high speed for text files.                                                                                                                                                                                                                                                                     |
| BZip2     | Standard compression method based on BWT algorithm. Usually it provides high speed and pretty good compression ratio for text files.                                                                                                                                                                                                                                                               |
| Deflate   | Standard compression method of ZIP and GZip formats. Compression ratio is not too high. But it provides pretty fast compressing and decompressing. Deflate method supports only 32 KB dictionary.                                                                                                                                                                                                  |
| Deflate64 | Modified version of Deflate algorithm with bigger dictionary (64KB).                                                                                                                                                                                                                                                                                                                               |









## Options de metadonnées de l'archive :

- L’option **« Mode de mise à jour »** (quand tu ajoutes des fichiers à une archive existante) contrôle **ce que le programme fait avec les fichiers déjà présents dans l’archive**.  Autrement dit, cela définit **comment 7-Zip met à jour ou remplace les fichiers** d’une archive .7z, .zip, etc.


![[Ressources/meta.png]]

	Voici les différents modes possibles :
	
| Mode de mise à jour                                                   | Description                                                                                                                                                                            |
| :-------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Ajouter et remplacer les fichiers** _(Add and replace files)_       | Ajoute les nouveaux fichiers et remplace ceux déjà présents dans l’archive s’ils portent le même nom. → C’est le mode le plus courant.                                                 |
| **Mettre à jour les fichiers** _(Update files)_                       | Remplace uniquement les fichiers **plus anciens** dans l’archive (comparaison par date). Si le fichier du disque est plus récent, il est mis à jour. Sinon, il est laissé tel quel.    |
| **Actualiser (Synchroniser) les fichiers** _(Freshen existing files)_ | Ne remplace que les fichiers **déjà présents** dans l’archive, et uniquement s’ils sont plus récents sur le disque. Aucun nouveau fichier n’est ajouté.                                |
| **Remplacer les fichiers** _(Synchronize archive contents)_           | Supprime de l’archive tout fichier qui n’existe plus dans le dossier source et met à jour le reste. En gros, cela rend l’archive **identique** au dossier d’origine (synchronisation). |
| **Ignorer les fichiers existants** _(Skip existing files)_            | Ajoute seulement les nouveaux fichiers, sans modifier ni remplacer ceux qui sont déjà dans l’archive.                                                                                  |


- L’option **« Format de l'archive»** détermine **le type de fichier compressé à créer** — c’est-à-dire **la structure et les capacités** de l’archive (vitesse, taux de compression, chiffrement, compatibilité, etc.).

![[format archive.png]]

Par défaut, 7-Zip ne garde **que la date de modification**, donc la date de dernière modification est préservée **mais** la date de création et celle du dernier accès sont perdues.
C’est un **problème en archivage technique ou légal**, où la date de création ou d’accès à une valeur est  importante.
exemple :
- Sauvegardes système ou serveur
- Archivage réglementaire
- Restauration complète d’environnement (avec hard links, symlinks, ACL) 

````

les options de format TAR / WIM  permettent d’enregistrer aussi les liens symboliques, liens physiques, ACL (Access Control List), NTFS(système de fichiers des systèmes Windows). 

````

## Créer et ouvrir une archive protegée sous Windows ( 10/11/Serveur)

**Le système de chiffrement de 7-Zip protège les documents sensibles contre tout accès non autorisé** . Le contenu des fichiers à protéger est chiffré à l'aide d'un mot de passe que vous définissez.

### créer le .zip

1. Clique droit sur ton dossier
2. **7-Zip → Ajouter à l’archive…**
3. Dans la fenêtre : 
4. ![[creer le zip.png]]
5. 


Laisse les différentes options sur" défauts" et choisis le format de l'archive et la méthode de chiffrement  :_ ( la plus sure actuellement est l'AES 256)_

**Format de l’archive :** 7zip   
**Méthode de chiffrement :** `AES-256` ( pas de choix avec 7.zip )
Pour le format zip proposé dans le menu , tu peux choisir ZipCrypto ou AES 256 ( mais ZipCrypto est moins secure ) par contre ZipCrypto crée une archive compatible avec la plupart des applications d'archivage.

 _il est possible aussi de chiffrer les noms de fichiers dans l'archive._
_Si vous devez partager ce fichier avec un collaborateur, vous devrez lui faire parvenir le mot de passe par un moyen securisé_ 

Puis il te faut genérer ton mot de passe , l'entrer et le confirmer. ( par exemple sur le site de la CNIL )

		# Genère un mot de passe solide sur le site de la CNIL : 

		https://www.cnil.fr/fr/generer-un-mot-de-passe-solide

 
 ![[CNIL.png]]
 
 Entre le mot de passe que tu viens de ** genérer**

Clique **OK**

_Le fichier obtenu sera bien un **.zip chiffré**, compatible avec Windows ._


<span id="utilisation-de-base"></span>

### Pour ouvrir le .zip .

Entre le mot de passe 
clique sur Ok  


![[ouvrir zip.png]]





## Création d'une archive protegée en powershell  


génération d' un mdp via .NET RNG (pas d'openssl requis)

```
$bytes = New-Object byte[] 24; [Security.Cryptography.RandomNumberGenerator]::Create().GetBytes($bytes); $pw=[Convert]::ToBase64String($bytes); & "C:\Program Files\7-Zip\7z.exe" a -t7z -mx=5 -mhe=on -p"$pw" "C:\temp\archive.7z" "C:\temp\dossier\"; $pw=$null; [GC]::Collect()
```
puis la compression de l'objet 

```
$SevenZip = "C:\Program Files\7-Zip\7z.exe"
$Archive = "C:\temp\archive.7z"
$Source  = "C:\temp\dossier\"

génère 24 octets aléatoires -> base64 (≈32 caractères)
$bytes = New-Object byte 24
Security.Cryptography.RandomNumberGenerator:Create().GetBytes($bytes)
pw = [Convert]::ToBase64String(bytes)

appel 7z (attention visibilité du -p)
& SevenZip a -t7z -mx=5 -mhe=on -p"pw" $Archive $Source

effacer le mot de passe en mémoire
$pw = $null
GC:Collect()

````



 

---

# 3. FAQ
<span id="faq"></span>
