---
title: "Séances de suivi"
description: ""
lead: ""
# date: 2020-10-13T15:21:01+02:00
# lastmod: 2020-10-13T15:21:01+02:00
draft: false
images: []
menu:
  docs:
    parent: "projet-ensai"
weight: 100
toc: true
---

## La note bibliographique

**Remarques**

- En rester à des publications statistiques, notemment des analyses sociologiques (un bon article de presse va s'appuyer sur une publication)

**A quoi ça servira ?**

- Il faut au maximum se baser sur des références bibliographiques (éviter le "on sait que...")
- Avoir des éléments "métier" sur le sujet (Introduction, cadrage, plan, ...)
- Ce qui se sait déjà => le rapport pourra confirmer ou infirmer
- Des éléments sur ce que ne couvre pas vos données => ouverture


## La problématique

**Remarques**

- Définir une problématique, ce n'est pas "juste" trouver une jolie question
- C'est toute la démarche de réflexions autour essentiellement de la bibliographie pour affiner les pistes de recherche
- Taille adapté :
  - trop restreint, vous aurez vite fait le tour
  - trop large, vous ne pourrez pas y répondre correctement dans les temps et nombre de pages impartis
  - La problématique pourra être élargie si nécessaire au second semestre
- **Attention** : vous ne pourrez pas détecter de causalité. C'est un projet de statistique descriptives, on peut "juste" trouver les variables qui fonctionnent ensemble => reflexion et bibliographie

**A quoi ça sert ?**

- "Angle d'attaque"
- => choix de variable, méthodes statistiques, plan, ...

## Le choix de variables

**Remarques**

- **Ne pas négliger le temps de construction de votre table de données**
- Sélectionner dès maintenant toute variable pouvant avoir un rapport plus ou moins éloignée avec votre sujet
- Pour le premier semestre, réeffectuer une sélection plus fine ne conservant que des variables en lien direct : les méthodes uni/bivariées ne vous permettrons que de gérer un nombre limité de variables
- Au second semestre vous aurez vu des méthodes multivariées qui sont conçues pour gérer beaucoup de variables
- Il faudra parfois construire des variables à partir des variables "brutes"
- **En cas de changement de logiciel, il est possible d'effectuer un export/import et pas forcément une recréation de zéro**

**A quoi ça sert/servira ?**
- Une connaissance du stock de variables peut aider à orienter correctement votre problématique (éviter de se focaliser sur un élément dont on a aucune mesure)
- La définition de la problématique (et des "sous problématiques") guide le choix final des variables
- La problématique pourra être élargie si nécessaire au second semestre

### Le choix de la ou des population.s, du ou des millésime.s

Question systématiques avant chaque traitemement de variables :
  - Quel est l'**individu statistique** ?
  - Quelle est la **population** ?

Spoiler : la réponse ne sera jamais ici un ménage, les ménages de France, mais plutôt les communes de plus de 10000 habitants de France métropolitaine.

- En priorité lors de croisements essayer d'utiliser les mêmes tables (exemple : "Communes 2020")
- Possibilité d'associer deux millésimes "proches" si on ne peut faire autrement
- En cas de tables différentes vérifier les jointures (par exemple pour les communes, chaque années il y a des petits changements)
- Penser à récupérer la source en même temps que la donnée : Institut, Administration, Entreprise dont est issu la donnée et nom de l'enquete, de la base, etc  (Insee RP, ...)

**A quoi ça sert/servira ?**
- Ne pas interpréter à côté, avoir une problématique cohérente
- titre, champ, source


## Le plan

- Garant de la cohérence de votre rapport
- Nous validerons ensemble un **plan**, pas des **titres** !!


## L'analyse uni/bi variée

- Des statistiques univariées pour connaitre la composition de la population
- Sélectionner en fonction de votre bibliographie par exemple des croisements a priori pertinents pour l'analyse
- Rester concis sur les résultats
  - Ne pas oublier les indicateurs de base (moyenne, variance, médiane, mode, etc.) sur vos variables d'intêret
  - Résultats "complexe" : Choix d'un tableau ou d'un graphique **avec son titre, champ, source, note de lecture**
  - Préciser ce qui est à remarquer dans le résultats statistique en faisant attention à ne pas surinterpréter

**On ne vous reprochera pas de ne pas avoir de réultats sensationnels s'il n'y en a pas à trouver, on vous reprochera des résultats issus de surinterprétation**


### L'outil cartographique intégré au site

- Outils de visualisation des données sous forme de carte
- Possibilité d'importer des variables calculées par vos soins
- Pertinent pour un sujet sur les territoires

MAIS

- NE PAS se forcer à avoir une carte pour avoir une carte
- NE PAS surutiliser l'outil
- une carte doit être lisible et doit porter une information

Une carte sur une variable brute équivaut techniquement à imprimer un tableau de donnée de brute (donc pas un statistique à proprement parler), la plus value, c'est quand on veut s'en serivir pour repérer un zone géographique pas forcément évidente à identifier avec un variable (le nord, la diagonale du vide, les alentours de grandes villes, les frontières, ...)

2 variables liées peuvent être détectées en observant que les cartes des deux variables "se ressemblent", mais il utiliser des outils plus précis pour le montrer (coefficient de correlation, tableau de contingence, ...)

