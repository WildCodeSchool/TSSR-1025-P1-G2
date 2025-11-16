## Sommaire

1. [Introduction](#introduction)
2. [Utilisation de base](#utilisation-de-base)
3. [Utilisation avancée](#utilisation-avancee)
4. [FAQ](#faq)

## Introduction
<span id="introduction"></span>
**Hashcat** est un outil open-source de **récupération de mots de passe**. Il exploite la puissance du CPU et surtout du **GPU (via OpenCL)** pour effectuer des calculs très rapides.
Chaque hash correspond à une empreinte (MD5, SHA1, NTLM, bcrypt, etc.) que Hashcat essaie de décoder en testant des candidats.

**Concepts de base**

| Élément                 | Description                                                                    |
| ----------------------- | ------------------------------------------------------------------------------ |
| **Hash**                | Empreinte chiffrée du mot de passe (ex : MD5, SHA1, NTLM...)                   |
| **Mode (-m)**           | Définit le type de hash                                                        |
| **Mode d’attaque (-a)** | Définit la stratégie utilisée (dictionnaire, brute-force...)                   |
| **Wordlist**            | Liste de mots à tester (ex : rockyou.txt)                                      |
| **Rules**               | Transformations appliquées à la wordlist (ajout de chiffres, majuscules, etc.) |
| **Masques**             | Modèles de brute-force ciblée (ex : ?l?l?l?d?d)                                |
| **Potfile**             | Fichier où Hashcat stocke les mots trouvés (~/.hashcat/hashcat.potfile)        |

---

## 1. Utilisation de base
<span id="utilisation-de-base"></span>
### 1.1 - Identifier le type de hash

Avant d’utiliser Hashcat,  **identifier le type de hash** .  

```bash
7z l -slt fichier2.zip
```

##### Exemples :

| Type de hash   | Mode Hashcat |
| -------------- | ------------ |
| MD5            | -m 0         |
| SHA1           | -m 100       |
| SHA256         | -m 1400      |
| NTLM (Windows) | -m 1000      |
| 7-Zip          | -m 11600     |
| ZIP WinZip AES | -m 13600     |
| bcrypt         | -m 3200      |
| WPA/WPA2 PMKID | -m 22000     |

---

### 1.2 - Extraire le hash

**Pour extraire le hash, utiliser l'outil zip2hashcat :**

```bash
zip2hashcat fichier2.zip > hash2.txt
```

**Utiliser la commande cat :**

```bash
cat hash2.txt
```

---

### 1.3 - Attaques de base

#### 1.3.1 - Commande

```bash
hashcat -m <mode_hash> -a <mode_attaque> <hash2.txt>
```

---
#### 1.3.2 - Modes d’attaque (-a)

| Mode | Nom                         | Description                              |
| ---- | --------------------------- | ---------------------------------------- |
| -a 0 | Dictionnaire                | Essaie chaque mot d’une liste            |
| -a 1 | Combinator                  | Combine deux listes de mots              |
| -a 3 | Brute-force / masque        | Génère toutes les combinaisons possibles |
| -a 6 | Hybride (wordlist + masque) | Ajoute un suffixe au mot                 |
| -a 7 | Hybride (masque + wordlist) | Ajoute un préfixe au mot                 |

---

**Dictionnaire simple (-a 0) - Dictionnaire**

```bash
hashcat -m 13600 -a 0 hash2.txt /usr/share/wordlists/rockyou.txt
```

---

**Masque (-a 3) - Brute Force ciblée** 

```bash
hashcat -m 0 -a 3 hash2.txt
```

---

**Hybride (-a 6) - Wordlist + Masque**

```bash
hashcat -m 0 -a 6 hash2.txt rockyou.txt ?d?d
```

Chaque mot de **rockyou.txt** + 2 chiffres à la fin.

---

**Hybride (-a 6) - Masque + Wordlist**

```bash
hashcat -m 0 -a 6 hash2.txt ?d?d rockyou.txt
```

Chaque mot de **rockyou.txt** + 2 chiffres à la fin.

---
### 1.4 - Résultats des attaques

- **Affichage des résultats trouvés :**

```bash
hashcat -m 13600 hash2.txt --show
```

- **Lecture du fichier résultat :**

```bash
cat found.txt
```

---

## 2. Utilisation avancée
<span id="utilisation-avancee"></span>
### 2.1 - Attaques avancées

**Utiliser des règles**

Les **rules** appliquent des transformations sur ta wordlist :

```bash
hashcat -m 0 -a 0 -r /usr/share/hashcat/rules/best64.rule hashes.txt rockyou.txt
```

---

**Personnaliser les caractères des attaques par masque**

| Symbole | Signification         |
| ------- | --------------------- |
| ?l      | Lettre minuscule      |
| ?u      | Lettre majuscule      |
| ?d      | Chiffre               |
| ?s      | Symbole               |
| ?a      | Tous caractères ASCII |
| ?1      | Charset personnalisé  |

**Exemple :**

```bash
hashcat -m 0 -a 3 -1 ?l?d hashes.txt ?1?d?u?a
```

---

### 2.2 - Contrôle des performances

**Benchmark :**

```bash
hashcat -b
```

**Choisir le niveau de charge**

```bash
hashcat -w 1   # léger
hashcat -w 3   # par défaut
hashcat -w 4   # intensif
```

**Vérifier les périphériques OpenCL :**

```bash
hashcat -I
```

---

## 3. FAQ
<span id="faq"></span>

**Q : Quelle est la différence entre John et Hashcat ?**

John the Ripper : orienté CPU, flexible, supporte de nombreux formats.  
Hashcat : orienté GPU, très performant, idéal pour de gros volumes.

---

**Q : Comment convertir un ZIP en hachage pour Hashcat ?**

```bash
zip2hashcat fichier.zip > hash.txt
````

---

**Q : Comment tester si ma carte graphique est reconnue ?**

```bash
hashcat -I
```

---

**Q : Où sont stockés les résultats ?**

**Par défaut dans**

```bash
~/.hashcat/hashcat.potfile
```

---

**Q : Hashcat dit "No devices found" - que faire ?**

**Vérifier les drivers GPU (NVIDIA/AMD) :**

```bash
sudo apt install ocl-icd-libopencl1
```

**et OpenCL :**

```bash
sudo apt install nvidia-driver
```

---

**Q : Comment reprendre une session interrompue ?**

```bash
hashcat --session=ma_session -m 13600 hash.txt rockyou.txt
```

**Pour reprendre :**

```bash
hashcat --restore --session=ma_session
```

---

