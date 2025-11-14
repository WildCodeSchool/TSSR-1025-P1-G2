## Sommaire

1. [Utilisation de base](#utilisation-de-base)
2. [Utilisation avancée](#utilisation-avancee)
3. [FAQ](#faq)

# 1. Utilisation de base

### 1.1  Fichier1.zip

Une fois le logiciel *John the ripper* installé sur notre machine, voici la procédure pour récupérer le fichier et lancer notre logiciel sur notre fichier  compressé protéger par un mot de passe :

- On se déplace dans notre dossier commun pour accéder au fichiers qui nous intéresse :

Pour se rendre sur notre **fichier1.zip** , voici la commande :

```bash
cd /mnt/Commun/win01/
```

et ensuite la commande avec la commande **ls** :

![image](Ressources/affichage_fichier1.png)

- On va copier le **fichier1.zip** dans notre répertoire **/home/wilder**

```bash
cp fichier1.zip /home/wilder
```
<span id="utilisation-de-base"></span>

![image](Ressources/copie.fichier1.zip.png)


- Maintenant nous allons commencer par récupérer le **HASH** de notre fichier par cette commande:

```bash
john-the-ripper.zip2john fichier1.zip > empreinte1.txt
```

- Ensuite comme vous pouvez le voir sur cette *screenshot* nous avons un fichier **empreinte1.txt** de créé avec le *hash*


![image](Ressources/hash_fichier1.zip.png)

- Grâce à ce fichier nous allons pouvoir lancer *John* pour nous casser le mot de passe par force brut avec cette commande :

```bash
john-the-ripper empreinte1.txt
```

Et voici le résultat tant attendu :

![image](Ressources/mdp_fichier1.zip.png)

Opération réussi comme vous pouvez voir le mot de passe était : **Essai**

### 1.2 Fichier2.zip

- Place au deuxième fichier cela va ressemblé au fichier 1 sauf que le chemin est différent :
- On se rend au bonne endroit et on copie le fichier sur le **/home/wilder**

```bash
cd /mnt/Commun/win01/svrwin01
cp fichier2.zip /home/wilder
```

![image](Ressources/copie_fichier2.zip.png)

- Récupérons le *HASH* :

```bash
john-the-ripper.zip2john fichier2.zip > empreinte2.txt
```

![image](Ressources/empreinte_fichier2.zip.png)


- Et maintenant on envoi la commande de l'attaque de *John*

```bash
john-the-ripper empreinte2.txt
```

![image](Ressources/mdp_fichier2.zip.png)


Et voilà le Mot de Passe de *fichier2.zip* était **demo**


# 2. Utilisation avancée
<span id="utilisation-avancee"></span>
- On peut aussi faire avec des options comme avec une liste de mdp spécifique :

```bash
john-the-ripper -wordlist=/home/wilder/Documents/000webhost.txt empreinte1.txt
```

Où avec la liste *rockyou* que l'on a vu dans la partie **INSTALL**

```bash
john-the-ripper -wordlist=/home/wilder/Documents/rockyou.txt empreinte1.txt
```

Pour affiché les options de *John-the-ripper* :

```bash
john the ripper --help
```

# 3. FAQ
<span id="faq"></span>
## 3.1 Questions générales

**Qu'est-ce que John the Ripper ?** John the Ripper est un logiciel open source de récupération et d'audit de mots de passe. Il permet de tester la robustesse des mots de passe en utilisant diverses techniques de craquage comme les attaques par dictionnaire, par force brute ou par règles de mutation.

**Quelles sont les principales utilisations de John the Ripper ?** Il sert principalement à l'audit de sécurité des mots de passe, à la récupération de mots de passe oubliés sur des systèmes légitimes, et à l'évaluation de la politique de sécurité d'une organisation.

**Quels types de hashs John the Ripper peut-il craquer ?** John supporte de nombreux formats : Unix crypt, MD5, SHA, NTLM, LM, des hashs d'applications (ZIP, RAR, PDF), de bases de données (MySQL, PostgreSQL), et bien d'autres selon la version.

## 3.2 Dépannage

**John ne détecte pas mes hashs, pourquoi ?** Vérifiez le format du fichier. Chaque ligne doit contenir un hash valide. Essayez de spécifier manuellement le format avec `--format`. Vérifiez que la version supporte ce type de hash.

**L'attaque est très lente, que faire ?** Commencez par un dictionnaire de mots courants, évitez le mode incrémental sur de longs mots de passe, testez d'abord sur un échantillon réduit, et vérifiez si le format de hash est naturellement lent (bcrypt, scrypt).

##  3.3 Sécurité et légalité

**Est-ce légal d'utiliser John the Ripper ?** Oui, si vous avez l'autorisation du propriétaire du système. Utiliser John sur des systèmes sans autorisation est illégal et constitue une infraction pénale dans la plupart des pays.

**À quoi sert l'audit de mots de passe ?** Il permet d'identifier les mots de passe faibles, de sensibiliser les utilisateurs, de vérifier la conformité avec les politiques de sécurité, et d'améliorer la posture de sécurité globale.

**Quelles sont les bonnes pratiques ?** Testez uniquement sur vos propres systèmes ou avec autorisation écrite, utilisez des environnements isolés, documentez vos tests, et proposez des recommandations constructives pour améliorer la sécurité.


mise a jour 
mise a jour 2