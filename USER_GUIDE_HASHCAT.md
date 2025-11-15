# Sommaire

1. [Introduction](#introduction)
2. [Utilisation de base](#utilisation-de-base)
3. [Utilisation avancée](#utilisation-avancee)
4. [FAQ](#faq)

# Introduction
<span id="introduction"></span>
**Hashcat** est un outil open-source de **récupération de mots de passe**. Il exploite la puissance du CPU et surtout du **GPU (via OpenCL)** pour effectuer des calculs très rapides. Chaque hash correspond à une empreinte (MD5, SHA1, NTLM, bcrypt, etc.) que Hashcat essaie de “deviner” en testant des candidats.

---
## Concepts de base

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
## Identifier le type de hash

Avant d’utiliser Hashcat, il faut **identifier le type de hash**.  
Utilise un outil comme :

```bash
hashid <fichier_hash>        # (sudo apt install hashid)
```
### Exemples :

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
# 1. Utilisation de base
<span id="utilisation-de-base"></span>
## Attaques de base

### Commande

```bash
hashcat -m <mode_hash> -a <mode_attaque> -o <resultat.txt> <fichier_hash> <wordlist>
```
#### Exemple (MD5 + dictionnaire) :

```bash
hashcat -m 0 -a 0 -o found.txt hashes.txt /usr/share/wordlists/rockyou.txt
```

| Option       | Signification                           |
| ------------ | --------------------------------------- |
| -m 0         | Type MD5                                |
| -a 0         | Mode dictionnaire                       |
| -o found.txt | Fichier où enregistrer les résultats    |
| hashes.txt   | Fichier contenant les hachages à tester |
| rockyou.txt  | Liste de mots de passe à essayer        |

---
#### Modes d’attaque (-a)

| Mode | Nom                         | Description                              |
| ---- | --------------------------- | ---------------------------------------- |
| -a 0 | Dictionnaire                | Essaie chaque mot d’une liste            |
| -a 1 | Combinator                  | Combine deux listes de mots              |
| -a 3 | Brute-force / masque        | Génère toutes les combinaisons possibles |
| -a 6 | Hybride (wordlist + masque) | Ajoute un suffixe au mot                 |
| -a 7 | Hybride (masque + wordlist) | Ajoute un préfixe au mot                 |

---
### Dictionnaire simple

```bash
hashcat -m 0 -a 0 hashes.txt /usr/share/wordlists/rockyou.txt
```

### Brute-force ciblée

```bash
hashcat -m 0 -a 3 hashes.txt ?l?l?l?l?d?d
```
4 lettres + 2 chiffres (ex : `abcd12`)

### Hybride

```bash
hashcat -m 0 -a 6 hashes.txt rockyou.txt ?d?d
```
Chaque mot de rockyou + 2 chiffres à la fin.

---

## Résultats des attaques

- **Affichage des résultats trouvés :**
```bash
 hashcat --show -m 0 hashes.txt
```

- **Lecture du fichier résultat :**
```bash
  cat found.txt
 ```

---
# 2. Utilisation avancée
<span id="utilisation-avancee"></span>
## Attaques avancées

### Utiliser des règles

Les **rules** appliquent des transformations sur ta wordlist :

```bash
hashcat -m 0 -a 0 -r /usr/share/hashcat/rules/best64.rule hashes.txt rockyou.txt
```

### Attaque incrémentale

```bash
hashcat -m 0 -a 3 -i --increment-min=4 --increment-max=6 hashes.txt ?l?l?l?l?l?l
```

### Personnaliser les caractères

| Symbole | Signification         |
| ------- | --------------------- |
| ?l      | Lettre minuscule      |
| ?u      | Lettre majuscule      |
| ?d      | Chiffre               |
| ?s      | Symbole               |
| ?a      | Tous caractères ASCII |
| ?1      | Charset personnalisé  |

Exemple :

```bash
hashcat -m 0 -a 3 -1 ?l?d hashes.txt ?1?1?1?1
```

---
## Contrôle des performances
### Benchmark :

```bash
hashcat -b
```

### Choisir le niveau de charge

```bash
hashcat -w 1   # léger
hashcat -w 3   # par défaut
hashcat -w 4   # intensif
```

### Vérifier les périphériques OpenCL :

```bash
hashcat -I
```

---
# 3. FAQ
<span id="faq"></span>