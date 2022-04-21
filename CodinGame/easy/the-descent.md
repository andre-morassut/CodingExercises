# Onboarding

## Description

### Objectif
Écrivez le programme permettant de détruire les montagnes pour pouvoir attérir. Pour cela, tirez sur la montagne la plus haute.
### Règles
Au début de chaque tour de jeu, vous recevez en entrée la hauteur de chaque montagne de gauche à droite.
Avant la fin du tour de jeu, vous devez indiquer la montagne la plus haute pour tirer dessus.
Tirer sur une montagne ne fera qu'en détruire une partie. Votre vaisseau descend à chaque passe.
### Conditions de victoire
Vous gagnez si vous détruisez la montagne la plus haute à chaque tour
### Conditions de défaite
Votre vaisseau percute une montagne
Vous fournissez une sortie invalide ou votre programme ne réponds pas à temps
### Note
N'oubliez pas d'exécuter les tests depuis la fenêtre "Jeu de tests". Les tests fournis et les validateurs utilisés pour le calcul du score sont légèrement différents pour éviter les solutions codées en dur.
### Entrées du jeu
Le programme doit lire depuis l'entrée standard la hauteur des montagnes puis fournir sur la sortie standard l'indice de la montagne à détruire.
### Entrées pour un tour de jeu
8 lignes : un entier mountainH par ligne. Il représente la hauteur d'une montagne. Les hauteurs des montagnes sont données dans l'ordre de leur index (allant de 0 à 7).
### Sortie pour un tour de jeu
Une unique ligne contenant le numéro de la montagne sur laquelle tirer.
### Contraintes
0 ≤ mountainH ≤ 9
Temps de réponse pour un tour ≤ 100ms

## Code

```js
/**
 * The while loop represents the game.
 * Each iteration represents a turn of the game
 * where you are given inputs (the heights of the mountains)
 * and where you have to print an output (the index of the mountain to fire on)
 * The inputs you are given are automatically updated according to your last actions.
 **/


// game loop
while (true) {
    let maxH = -1;
    let maxIdx = 0;
    for (let i = 0; i < 8; i++) {
        const mountainH = parseInt(readline()); // represents the height of one mountain.
        if (mountainH > maxH) {
            maxH = mountainH;
            maxIdx = i;
        }
    }

    // Write an action using console.log()
    // To debug: console.error('Debug messages...');

    console.log(maxIdx);     // The index of the mountain to fire on.

}
```

