
### 3.3 Le logiciel 7-Zip
##### 3.3.1 p7zip-full

```bash
sudo apt install -y p7zip-full
```


Commandes utiles :

```bash
7z l fichier.7z                   # liste le contenu
7z x fichier.7z                   # extrait les fichiers
7z l -slt fichier.7z              # détaille le chiffrement (AES, CRC, etc.)
7z e <archive>                    # Décompresse une archive
7z a -pMot_De_Passe  [fichiers]   # Créer une archive 7-Zip avec un mot de passe
7z a -mhe=on -pMot_De_Passe <archive> [fichiers] # Créer une archive 7-Zip avec un mot de passe et le chiffrement des noms de fichiers 
et toujours :
man 7z

```


---

*un exemple de création en cli*
![[creation_archive_ubuntu.jpg]]

*un exemple d' extraction en cli*

![[extraction_archive_ubuntu.jpg]]

##### 3.3.2 unzip

```bash
sudo apt install -y unzip
```

Commandes utiles

```bash
unzip -l fichier.zip       # liste le contenu
unzip fichier.zip          # extrait le contenu
```

---

##### 3.3.3 zipinfo

```bash
sudo apt install -y zipinfo
```

Commandes utiles :

```bash
zipinfo archive.zip          # affiche le contenu de l'archive
zipinfo -v archive.zip       # affiche le contenu détaillé de l'archive
```
## 4. Installation sur les machines cibles (Windows 11 Professionnel & Windows Server 2019)

### 4.2. Le logiciel 7-Zip

#### 4.2.1 ** Installation manuelle **

Le site officiel : [https://www.7-zip.org](https://www.7-zip.org)
![[page_de_telechargement_7zip.png]]


1. Télécharge la version correspondant à ton système :
    
2. Exécute le fichier `.exe` téléchargé avec un clic droit → **Exécuter en tant qu’administrateur**.
    
3. Clique sur **Install**, puis sur **Close** une fois terminé.

 *7-Zip s’ajoute automatiquement au menu clic droit de l’Explorateur.*

#### 4.2.2 ** Installation via PowerShell avec Winget **

Si **Winget** est disponible (Windows Server 2022, 2025, ou si tu l’as ajouté manuellement) :

````
winget install 7zip.7zip

````

   *7-Zip s’ajoute automatiquement au menu clic droit de l’Explorateur.*


# 5. FAQ
<span id="faq"></span>
### 5.3 Le logiciel 7-Zip


**Q : À quoi sert le chiffrement d’un fichier ZIP ?**

Le chiffrement d’un fichier ZIP consiste à le protéger par un mot de passe. Le contenu est brouillé à l’aide d’algorithmes cryptographiques et n’est accessible qu’en entrant le mot de passe correct. Cela empêche tout accès non autorisé, même si quelqu’un intercepte le fichier.

**Q: Lequel est le meilleur, Zipcrypto ou AES-256  ?**

**Il est prouvé que le protocole AES-256 est beaucoup plus sûr que ZipCrypto** , mais si vous choisissez AES-256, le destinataire du fichier zip devra peut-être installer 7-zip ou un autre programme de compression pour lire le contenu du fichier.


**Q: 7-Zip AES-256 est-il sûr  ?**

**Le format de fichier 7-Zip est sûr** . Le chiffrement AES-256 est sûr pour au moins les prochaines décennies, à condition d'utiliser un mot de passe robuste. Pensez à chiffrer les noms de fichiers si vous le souhaitez et à supprimer les fichiers de manière sécurisée après avoir vérifié l'archive. Si vous souhaitez un plus large choix d'algorithmes de chiffrement, essayez PicoCrypt. (12 mai 2023)


**Q : Le chiffrement AES-256 est-il piratable  ?**

**L'AES 256 est inviolable par force brute.**  
Cela rend le chiffrement AES 256 et les données qui le protègent ensuite inviolables pour l'avenir imprévu. (22 juin 2022)


**Q : Quelqu'un a-t-il déjà réussi à casser le chiffrement AES  ?**

La différence entre le décryptage des algorithmes AES-128 et AES-256 est considérée comme minime. Toute avancée permettant de décrypter l'algorithme 128 bits permettra probablement aussi de décrypter l'algorithme 256 bits. En définitive, contrairement à certaines idées reçues, **l'AES n'a jamais été décrypté** et reste inviolable face aux attaques par force brute.


**quelles sont les risques et limites du chiffrement ZIP**

- **Mots de passe faibles**: Évitez les mots de passe courts ou communs.
- **Fuites de métadonnées**: Certains outils ZIP peuvent révéler des noms de fichiers.
- **Compatibilité**: Tous les outils ne peuvent pas ouvrir les fichiers ZIP AES-256.
- **Pas de récupération**: Des mots de passe perdus signifient des fichiers perdus.

Pour éviter autant que possible ces risques, considérez les meilleures pratiques suivantes :

- Utilisez des [mots de passe forts et uniques](https://blog.mailfence.com/fr/mot-de-passe-ou-phrase-de-passe/) (12 caractères et plus).
- [Partagez les mots de passe](https://blog.mailfence.com/fr/partage-de-mot-de-passe-securise/) sur des canaux distincts (par exemple, courrier électronique + SMS).
- Vérifiez que le destinataire dispose d’outils compatibles (par exemple, 7-Zip ou WinRAR).
- Utilisez un hachage de fichier (SHA-256) pour confirmer l’intégrité du fichier après.



Pour en savoir plus sur le cryptage AES :
https://www.winzip.com/en/support/aes-encryption/