# Projet Rainbow Table

Ce projet implémente l'utilisation de **tables arc-en-ciel** pour le cassage de mots de passe hachés, permettant une alternative plus rapide aux attaques par force brute. Les tables arc-en-ciel exploitent des valeurs de hachage pré-calculées pour retrouver plus efficacement les mots de passe à partir de leurs hachages.

## Fonctionnalités

- **Génération de tables arc-en-ciel** à l'aide de plusieurs algorithmes de hachage.
- **Cassage de mots de passe hachés** à partir de tables arc-en-ciel générées.
- Prise en charge de plusieurs algorithmes de hachage comme MD5, SHA-256, SHA-512, etc.
- Utilisation flexible de différents jeux de caractères, tailles de mots de passe, et fonctions de réduction.

## Table des matières
1. [Prérequis](#prérequis)
2. [Compilation](#compilation)
3. [Utilisation du script Bash](#utilisation-du-script-bash)
4. [Exemples d'exécution](#exemples-dexécution)
5. [Détails des paramètres](#détails-des-paramètres)
6. [Remarques](#remarques)

---

## Prérequis

Avant de commencer, assurez-vous d'avoir :
- **Java** installé sur votre système (version 8 ou supérieure).
- Un terminal Unix/Linux ou macOS pour exécuter le script Bash.
- Le répertoire `build/` où seront stockés les fichiers compilés.

## Compilation

Avant de pouvoir exécuter le projet, il est nécessaire de compiler les fichiers Java. Pour cela, exécutez la commande suivante dans le terminal à partir de la racine du projet :

```bash
javac -d ../build rainbow/model/demo/*.java rainbow/model/pwdgen/*.java rainbow/model/utils/*.java rainbow/model/hashing/*.java rainbow/model/table/*.java rainbow/model/reduction/*.java
```

Cette commande compile tous les fichiers Java nécessaires et les place dans le dossier `build`.

## Utilisation du script Bash

Le script Bash `rainBowScript.bash` situé dans le répertoire `src` facilite l'utilisation du projet. Il permet de générer des tables arc-en-ciel ou de casser des mots de passe via une interface en ligne de commande interactive.

### Étapes pour utiliser le script

1. **Accéder au répertoire contenant le script** :
   ```bash
   cd src
   ```

2. **Rendre le script exécutable** (si ce n'est pas déjà fait) :
   ```bash
   chmod +x rainBowScript.bash
   ```

3. **Lancer le script** :
   ```bash
   ./rainBowScript.bash
   ```

4. **Sélectionner une option** :
   Le script vous demandera de choisir entre deux options :
   - **1** pour **générer une table arc-en-ciel**.
   - **2** pour **casser des mots de passe** à l'aide d'une table arc-en-ciel préexistante.

5. **Suivre les instructions** :
   - Sélectionnez l'algorithme de hachage à utiliser (MD5, SHA-256, etc.).
   - Saisissez le jeu de caractères utilisé pour les mots de passe (par exemple, `abc123`).
   - Définissez la longueur des mots de passe, le nombre de réductions, etc.

### Exemple d'utilisation

1. **Génération d'une table arc-en-ciel** :
   Lorsque vous choisissez l'option "1", le script vous demandera les informations suivantes :
   - Algorithme de hachage (exemple : MD5).
   - Jeu de caractères pour les mots de passe (exemple : `abc123`).
   - Nombre de réductions et taille de la table arc-en-ciel.

   Après avoir fourni ces informations, la commande suivante sera automatiquement exécutée :
   ```bash
   java -cp ../build rainbow.model.demo.Main generator <algo> <charset> <reduce_number> <table_size> <pw_number> <pw_size>
   ```

2. **Cassage de mots de passe** :
   Si vous sélectionnez l'option "2", le script tentera de casser des mots de passe hachés en utilisant une table arc-en-ciel existante :
   ```bash
   java -cp ../build rainbow.model.demo.Main crack <algo> <charset> <reduce_number> ./DataBase/RainBowTable.txt ./DataBase/passWordToCrack.txt <pw_size>
   ```

---

## Exemples d'exécution

### 1. Générer une table arc-en-ciel

Supposons que vous souhaitez générer une table arc-en-ciel avec l'algorithme **MD5**, le jeu de caractères **abc123**, 2 réductions, 10 mots de passe et une longueur de 6 caractères :

```bash
./rainBowScript.bash
# Sélectionnez 1 pour générer
# Choisissez "MD5" comme algorithme, "abc123" comme charset, 2 réductions, 10 mots de passe, et longueur 6
```

Cela générera une table arc-en-ciel avec les paramètres spécifiés.

### 2. Casser des mots de passe

Supposons que vous avez déjà généré une table arc-en-ciel et que vous souhaitez casser des mots de passe hachés dans un fichier :

```bash
./rainBowScript.bash
# Sélectionnez 2 pour casser
# Choisissez "MD5" comme algorithme, "abc123" comme charset, et longueur 6
```

Le script utilisera alors la table arc-en-ciel et les hachages dans `passWordToCrack.txt` pour tenter de retrouver les mots de passe originaux.

---

## Détails des paramètres

### Paramètres d'entrée
- **algo** : Algorithme de hachage à utiliser (ex : `MD5`, `SHA-256`).
- **charset** : Jeu de caractères pour les mots de passe (ex : `abc123`).
- **reduce_number** : Nombre de réductions appliquées aux hachages.
- **table_size** : Taille de la table arc-en-ciel (nombre de chaînes dans la table).
- **pw_number** : Nombre de mots de passe à générer ou casser.
- **pw_size** : Longueur des mots de passe.

### Mode générateur
- Permet de générer une table arc-en-ciel avec les paramètres spécifiés.

### Mode cassage
- Utilise une table arc-en-ciel pour retrouver les mots de passe à partir de leurs hachages.

---

## Remarques

- **Efficacité des tables arc-en-ciel** : Les tables arc-en-ciel sont particulièrement efficaces pour casser des mots de passe non salés. Il est fortement recommandé d'utiliser des hachages salés dans les systèmes réels pour se protéger contre ce type d'attaque.
- **Taille de la table** : Une plus grande taille de table améliore les chances de casser des mots de passe, mais nécessite plus d'espace de stockage et de temps de pré-calcul.
- **Utilisation de hachages sécurisés** : Les hachages sécurisés avec sel rendent les attaques par table arc-en-ciel beaucoup plus difficiles.



