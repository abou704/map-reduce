## Aboubakiri
## DIAW
---


# Introduction

Ce rapport est une application du cours sur Hadoop. Il comprend 2 parties et une reponse à la question sur le fichier ventes:


## Partie 1
La première partie de ce rendu consiste à écrire un script map-reduce qui détecte les mots ayant EXACTEMENT les mêmes lettres (mais dans un ordre différent). 

* Code map

Je vous présente ci-dessous le **code map** écrit en python:


```` PYTHON
import sys
wordList = dict()
# input comes from STDIN (standard input)
for line in sys.stdin:
    # remove leading and trailing whitespace
    line = line.strip()
    # split the line into words
    words = line.split()

    # increase counters
    for word in words:

        wordList[word]="".join(sorted(word))  #cree list[cle,valeur]
        print (wordList[word], '\t', word)# affichage cle valeur   

````

*Code Reduce

Je vous présente ci-dessous le **code reduce** écrit en python:

```` PYTHON
import sys
current_key = None
current_word = list()
key = None
# input comes from STDIN
for line in sys.stdin:
    # remove leading and trailing whitespace
    line = line.strip()

    # parse the input we got from mapper.py
    key, word = line.split('\t', 1)

    if current_key == key:

        current_word.append(word)  #ajoute le mot dans la list de meme cle
        if len(current_word)>1:

            print (current_word)

    else :

        if current_key :
             # write result to STDOUT
            del current_word[:]
        current_key = key  # passe a la cle suivante
        current_word.append(word) # ajoute la la list la valeur de la cle suivant

if current_key == key and len(current_word) > 1:
    print (current_word)
    
````

#### Résultat de l'algorithme sous environnement **Hadoop**
A partir s'etre connecté au hadoop-master, j'ai lancé les daemon **Hadoop**. Apres, je lance le job que j'ai prévu dans mes fichiers map.py et reduce.py. J'obtiens en sorti le résultat suivant:


![img](/alpha.PNG)





## Partie 2

La deuxième partie consiste à proposer une requête originale et complexe sur le fichier de données
Dans cette base ma requête consiste à afficher les noms des 100 auteurs morts au XIXeme siècle rangés par ordre décroissante des années.

### Description de la requête


### reponse à la question 2 sur le fichier ventes
A partir s'etre connecté au hadoop-master, j'ai lancé les daemon **Hadoop**. Apres, je lance le job que j'ai prévu dans mes fichiers map.py et reduce.py. J'obtiens en sorti le résultat suivant:

![img](/ventes2.PNG)
