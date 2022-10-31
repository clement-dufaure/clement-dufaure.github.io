---
title: "Autres remarques"
description: ""
lead: ""
# date: 2020-10-13T15:21:01+02:00
# lastmod: 2020-10-13T15:21:01+02:00
draft: true
images: []
menu:
  docs:
    parent: "projet-ensai"
weight: 200
toc: true
---

## Ne pas oublier les variables synthétiques
En bivarié :
- Corrélation entre 2 quanti 
- Rapport de corrélation (η²) entre quanti/quali
- χ2 ou V de cramer pour quali/quali :
À surtout utiliser à titre de comparaison entre plusieurs croisements de variables
- Coefficient de détermination (R²) pour une régression

## Tableau de contingence
- Se concentrer sur profil ligne ou colonne
- Mettre impérativement la marge associée (absence tolérée si c'est des quantiles)
- Essayer de conserver le "même sens" si plusieurs croisement avec la même variable
- Se focaliser sur sur/sous représentation ou comparaison entre profils

## Être précis sur le choix des variables
- Problématique (raisonnement) => **DES** question**S** => choix de variables
- Détailler les variables, leur modalités
- Attention particulière sur les variables créées ou modifiées : pourquoi ? comment ?

## Rédaction
- Un minimum d'effort sur les titres...
- Problèmatique -> Pourquoi une statistique -> La statistique -> Résultat/Interprétation
- Attention aux parties "Catalogue"

## Attention à la surinterprétation !!
- Éviter les hypothèses "personnelles"
- Utiliser la bibliographie

## Choix des graphiques
- Un graphique doit être lisible, apporter de l'information (ou illustrer un résultat)
- Camenbert : à réserver pour les fréquences de variables quali nominales
- Diagramme en baton : pour les quali ordinales
<!-- - Donnée manquante : plutôt à traiter hors graphique, ou alors être très clair (par exemple pour le cas des batons, c'est délicat de placer à une extrémité ou l'autre) -->

## Forme
- Bibliographie : tout élément doit être cité, en latex utilisez les références
- Toute annexe doit être citée. Une annexe illisible ne sert à rien (par exemple attention aux représentations graphiques des analyses factorielles).
<!--- Le code doit quand même être un minimum lisible (en latex utiliser un environnement `verbatim`)-->
- Tableaux / graphiques : éviter les sorties brutes des logiciels (moche). Ne batailler pas des heures avec les paramétrages de la PROC TABULATE ou assimilé. Prenez des résultats butes et faites votre propre tableau directement dans latex/word/... ou faites vos graphiques dans excel/libreoffice/... 

## Forme
- Éviter tout codage de variable dans le corps du rapport
- Annoncez les méthodes utilisées !

## Forme
- ATTENTION aux termes corrélation et sous/sur représentés
- Sur/sous représentés : parfois utilisé pour "modalité rare"

## Forme : Notations usuelles
- R² : coefficient de détermination d'une régression
- η² : rapport de corrélation (quali/quanti)

## Forme
Pour un graphique/tableau : 
- Source
- Champ (échelon géographique)
- Note de lecture si nécessaire (n'est pas une interprétation)
- **Doit se démarquer du corps de texte**

## Individus atypiques
- Varibles quanti : possibilité de supprimer les valeurs "anormalement" élevées (2nd semestre : mettre en supplémentaire)
- Variables quali : regrouper les modalités rares (décomposer la variance sur une classe trop petite donne de mauvais résultats)

## Attention : petite population
- Seulement 13 régions : "risque" de décrire tout le tableau
- Ce n'est pas faux, mais il ne faut pas oublier les stats de bases
- Lire un tableau de données brutes n'est pas un travail statistique complet
- Illutratif, voire contrôle de la méthode stat

## Variable "effectif" ou "nombre de"
- Attention à leur utilisation en particulier dans les croisements !
- Plus cohérent en rapportant à la population
- Variable "intermédiaire" population

## Individu statistique
Vous allez étudiez des villes, des départements, des zones d'emploi ... **Pas des personnes physiques**
- Pensez-y dans la lecture et l'interprétation de vos résultat !
- "Les villes avec plus de cadres sont plus riches" et non "Les cadres sont plus riches"

## Graphique et tableaux
- Attention aux source et champs
- La source n'est pas "Observatoire des territoires" !
- L'obesrvatoire des territoires propose une compilation de plusieurs sources
- Un tableau/graphique peut avoir plusieurs sources
- Champs : peut changer d'un tableau/graphique à un autre !
    - Communes de France métropolitaine
    - Régions
    - ...

## Gérer des donées temporelles ?
- Vous n'avez pas les outils pour analyser finement une série temporelle
- Si vous voulez analyser une évolution
   - Calcul (par commune par exemple) d'un taux d'évolution : l'évolution devient une variable "comme les autres" (moyenne, variance, croisement avec un autre variable, ... , intégration dans une analyse factorielle)
   - Se limiter à étudier les disparités dune évolution entre deux millésimes, risque de compliquer le raisonnement en croisant plusieurs évolutions.

## Modalités rares
Attention, risque de fausses interprétations !
- Revenu moyen selon age moyen dans les villes
- [0 - 45] : 2000
- [45 - 70] : 2100
- [70 - 100] : 3500
Le revenue augmente nettement avec l'age moyen ?

## Modalités rares
- Répartition des villes
    - [0 - 45] : 54 %
    - [45 - 70] : 45 %
    - [70 - 100] : 1 %
- 3e classe atypique, perturbe l'analyse, équivalent d'une valeur extrème pour les quanti
Rq : données purement imaginées !

## Données manquantes
- Globalement très peu de données manquantes
- On ne vous demande pas de savoir les gérer
- Attention sur quelques variables, données manquantes potentiellement massives et contitionnées
- exemple : taux de logement social calculé uniquement sur les communes de plus de N habitants

## Second semestre
- Maintien de la mise en problématique, données, démarche, choix de variables, etc
- Les stats univariées restent nécessaires pour du cadrage (notemment recherche de modalité rares), potentiellement quelques éléments de bivarié
- Idée générale : remplacer la partie bivariée un peu lourde par du multivarié plus synthétique
- Utiliser une méthode de classification dans le même esprit (le cours arrive bientôt)

## Second semestre
Analyse factorielle 
- Pensez au déroulé de la méthode : choix de la méthode, paramétrage, actives/supplémentaires
- Représentations graphiques en analse factorielle : dessin de l'axe et de se qui s'oppose suffit
- Les représentations des plans factoriels s'adaptent mal à un résultat d'étude généralement (illisibles et parfois trompeurs)

## Second semestre
Classification
- Choix de la méthode, paramétrage,... Rester cohérent avec les choix de l'analyse factoriel ou justifier
- Si CAH, utiliser les résultats de l'analyse factorielle
- Ce qui est surtout attendu : analyse de la partition retenue
- La classification crée une nouvelle variable qualitative (appartenance à la classe C)
- Les résultats se basent essentiellement sur des statistiques bivariée (tableaux et graphiques de la statistique bivariée peuvent alors être utilisés)


## Catégoriser une quanti
- Dans un environnement avec que des quali (ou presque) c'est souvent un bon choix
- Les tableaux de contingence sont souvent plus lisibles et plus exploitables

## Gérer des donées temporelles ?
- Alternative en analyse factorielle
- DISCLAIMER : risque de ne rien donner
- possibilité d'intégrer le même jeu de variables disponible sur plusieurs millésimes. Idée : voir si des années se ressemble du point de vue de certaines variables, se distinguent sur une autre.

## Analyse factorielle :  quelles variables acives retenir ?

- Vu en cours/TD : CTR>CTR moyenne, n premières les plus contributives, ...
- Se baser sur ces critères (et annoncer comment vous avez choisi) pour filtrer mais rester souple. On peut par exemple conserver une variable avec une CTR plus faible si elle est juste en dessous de la moyenne et que l'on conserve un variable juste au dessus.

## Analyse factorielle :  quelles variables supplémentaires retenir ?

- En général on se base sur la qualité de représentation
- Mais attention en ACM, elle est mécaniquement très faible
- Il faut *impérativement* utiliser la valeur test (VT, p-value) et conserver par exemple les VT, |VT|>2
 
## Les données manquantes ?
- Dans tous les cas une première analyse sans aucun traitement : on peut à ce moment détecter des comportements de non réponse (par exemple les non réponds ont l'air d'être associé à un revenu élevé)

## Les données manquantes ?
- Lorsque la non réponse est une modalité rare (*et seulement si*), elle va perturber l'analyse, il faut alors regrouper la non réponse avec les autres modalités :
   - en utilisant la première analyse et l'affecter "au plus proche voisin"
   - en utilisant la ventilation aléatoire (level.ventil de FactomineR) : le comportement est parfois surprenant, on peut le faire à la main de façon plus sûre et le fixer pour les analyses suivantes.
   - en utilisant les fonctions d'imputation de FactomineR : MissMDA
   - (remarque : il existe une méthode, COREM, permettant de mettre en supplémentaire des modalités. Le TDC est alors à marge non constante)
   
- Attention, on ne peut pas mettre en supplémentaire les individus avec de la non réponse ! (zero frequencies)
- On peut aussi éliminer toute observation avec au moins une donnée manquante, mais c'est un peu dommage...-->

## Les modalités rares ?

- Dans tous les cas une première analyse sans aucun traitement : on peut à ce moment remarque que la modalité rare X se comporte comme la modalité Y
- On effectue alors un regroupement :
   - par le sens : deux modalités nominales proches (niveau d'études école ou collège) ou deux modalités ordinales successives (3 enfants et 4 enfants ou plus devient 3 enfants ou plus)
   - en utilisant la première analyse et l'affecter "au plus proche voisin"
   - en utilisant la ventilation aléatoire (level.ventil de FactomineR) : le comportement est parfois surprenant, on peut le faire à la main de façon plus sûre et le fixer pour les analyses suivantes.
   - (remarque : il existe une méthode, COREM, permettant de mettre en supplémentaire des modalités. Le TDC est alors à marge non constante)

- Attention, on ne peut pas mettre en supplémentaire les individus avec la modalité rare ! (zero frequencies)

## Le eta2 dans les listings de classification

- Pour l'analyse de variables *quantitatives* sur les classes, il permet de dire si la variable permet de bien décrire la partition (équivalent du chi2 pour une variable qualitative). C'est la statistique du test de fisher, elle vaut (Vinter/n-k)/(Vintra/k-1) et suit une loi de fisher (k-1,n-k) avec n le nombre d'individu, k le nombre de classes.

## Rappel démarche d'une classification
- Statistiques descriptives (nbr obs, type de données, nbr variables...)
- Choix des éléments actifs (obs et vbles)
- Choix de la métrique et des critères d'agrégation (si CAH)
- Choix du nombre de groupes et de la méthode de clustering sélectionnée (si plusieurs méthodes utilisées)
- Interprétation des classes pour la méthode sélectionnée à partir des paramètres (centres des classes...)

<!-- ## Mais pourquoi fait-on une classification ? Ca ne sert à rien les individus sont anonymes.
- ...-->

## La classification
- Il ne s'agit pas juste de trouver de bonnes classes, il faut aussi (et surtout) bien analyser les classes !
- (Donc aura du sens aussi sur les communes)
- Profils-types
- Adapté à la vulgarisation
