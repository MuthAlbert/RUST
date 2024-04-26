# Cargo

Cargo est le système de compilation et de gestion de paquets de Rust. La plupart des Rustacés utilisent cet outil pour gérer les projets Rust, car Cargo s'occupe de nombreuses tâches pour vous, comme compiler votre code, télécharger les bibliothèques dont votre code dépend, et compiler ces bibliothèques. (On appelle dépendance une bibliothèque nécessaire pour votre code.)

Des programmes Rust très simples, comme le petit que nous avons écrit précédemment, n'ont pas de dépendance. Donc si nous avions compilé le projet “Hello, world!” avec Cargo, cela n'aurait fait appel qu'à la fonctionnalité de Cargo qui s'occupe de la compilation de votre code. Quand vous écrirez des programmes Rust plus complexes, vous ajouterez des dépendances, et si vous créez un projet en utilisant Cargo, l'ajout des dépendances sera plus facile à faire.

## utilisation cargo

exemple:
````bash
$ cargo new hello_cargo
$ cd hello_cargo
````
Rendez-vous dans le dossier hello_cargo et afficher la liste des fichiers. Vous constaterez que Cargo a généré deux fichiers et un dossier pour nous : un fichier Cargo.toml et un dossier src avec un fichier main.rs à l'intérieur.

Contenu de Cargo.toml généré par cargo new.
Ce fichier est au format TOML (Tom’s Obvious, Minimal Language), qui est le format de configuration de Cargo.

````toml
[package]
name = "hello_cargo"
version = "0.1.0"
edition = "2021"

[dependencies]
````

La première ligne, [package], est un en-tête de section qui indique que les instructions suivantes configurent un paquet. Au fur et à mesure que nous ajouterons plus de détails à ce fichier, nous ajouterons des sections supplémentaires.

Les trois lignes suivantes définissent les informations de configuration dont Cargo a besoin pour compiler votre programme : le nom, la version, et l'édition de Rust à utiliser. Nous aborderons la clé edition dans l'Annexe E.

La dernière ligne, [dependencies], est le début d'une section qui vous permet de lister les dépendances de votre projet. Dans Rust, les paquets de code sont désignés sous le nom de crates. Nous n'allons pas utiliser de crate pour ce projet, mais nous le ferons pour le premier projet au chapitre 2 ; nous utiliserons alors cette section à ce moment-là.

## Compiler et exécuter un projet Cargo

````bash
$ cargo build
   Compiling hello_cargo v0.1.0 (file:///projects/hello_cargo)
    Finished dev [unoptimized + debuginfo] target(s) in 2.85 secs
````
Cette commande crée un fichier exécutable dans target/debug/hello_cargo (ou target\debug\hello_cargo.exe sous Windows) plutôt que de le déposer dans votre dossier courant. Vous pouvez lancer l'exécutable avec cette commande :
````bash
$ ./target/debug/hello_cargo # ou .\target\debug\hello_cargo.exe sous Windows
Hello, world!
````

Mais cette commande "cargo run" fait les deux en une seule commande :
````bash
$ cargo run
    Finished dev [unoptimized + debuginfo] target(s) in 0.0 secs
     Running `target/debug/hello_cargo`
Hello, world!
````
Cargo fournit aussi une commande appelée "cargo check". Elle vérifie rapidement votre code pour s'assurer qu'il est compilable, mais ne produit pas d'exécutable.

Dans quel cas n'aurions-nous pas besoin d'un exécutable ? Parfois, cargo check est bien plus rapide que cargo build, car il saute l'étape de création de l'exécutable. Si vous vérifiez votre travail continuellement pendant que vous écrivez votre code, utiliser cargo check accélèrera le processus ! C'est pourquoi de nombreux Rustacés utilisent périodiquement cargo check quand ils écrivent leur programme afin de s'assurer qu'il compile. Ensuite, ils lancent cargo build quand ils sont prêts à utiliser l'exécutable.

# Resumer
- Nous pouvons créer un projet en utilisant cargo new.
- Nous pouvons compiler un projet en utilisant cargo build.
- Nous pouvons compiler puis exécuter un projet en une seule fois en utilisant cargo run.
- Nous pouvons compiler un projet sans produire de binaire afin de vérifier l'existance d'erreurs en utilisant cargo check.
- Au lieu d'enregistrer le résultat de la compilation dans le même dossier que votre code, Cargo l'enregistre dans le dossier target/debug.

## Compiler pour diffuser

Quand votre projet est finalement prêt à être diffusé, vous pouvez utiliser "cargo build --release" pour le compiler en l'optimisant. Cette commande va créer un exécutable dans target/release au lieu de target/debug. Ces optimisations rendent votre code Rust plus rapide à exécuter, mais l'utiliser rallonge le temps de compilation de votre programme. C'est pourquoi il y a deux différents profils : un pour le développement, quand vous voulez recompiler rapidement et souvent, et un autre pour compiler le programme final qui sera livré à un utilisateur, qui n'aura pas besoin d'être recompilé à plusieurs reprises et qui s'exécutera aussi vite que possible. Si vous évaluez le temps d'exécution de votre code, assurez-vous de lancer "cargo build --release" et d'utiliser l'exécutable dans target/release pour vos bancs de test.