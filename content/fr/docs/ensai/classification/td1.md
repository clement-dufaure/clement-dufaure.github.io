---
title: "TD1 Classification"
description: "Méthodes géométriques"
lead: ""
# date: 2020-10-13T15:21:01+02:00
# lastmod: 2020-10-13T15:21:01+02:00
draft: true
images: []
menu:
  docs:
    parent: "classification"
weight: 100
toc: true
---


# Exercice 1 : K Means

## 1-1 Différents paramétrages

| 1 | 2 | 9 | 12 | 20 |


---

a) $K=2;μ_1=1;μ_2=7$

K nombre de classe

Dans K-means, **le nombre de classe est un paramètre**, il est défini a priori

On choisit alors au hasard autant de points que de classes (notés $µ_i$), ce sont les barycentres des classes à l'itération 0.

### Itération 1

| 1 | 2 || 9 | 12 | 20 |
|-|-|-|-|-|-|
| x |  |x|  | |  |
| $µ_1=1$ |  |$µ_2=7$|  | |  |

- Points plus proche de $µ_1$ que de $µ_2$ : 1,2

- Points plus proche de $µ_2$ que de $µ_1$ : 9,12,20

Classes à l'itération 1 : 

| 1  2 || 9  12  20 |

Barycentre de ces classes :
- Classe 1 : $(1+2)/2=1.5$
- Classe 2 : $(9+12+20)/3=13.7$

### Itération 2

| 1 || 2 | 9 | 12 || 20 |
|-|-|-|-|-|-|-|
|| x |  ||  |x |  |
|| $µ_1=1.5$ |  ||  |$µ_2=13.7$ |  |

- Points plus proche de $µ_1$ que de $µ_2$ : 1,2

- Points plus proche de $µ_2$ que de $µ_1$ : 9,12,20

Les classes sont stables : 

| 1  2 || 9  12  20 |

Fin de l'algorithme

---

b) $K=2;μ_1=1;μ_2=20$

### Itération 1

| 1 | 2 | 9 | 12 | 20 |
|-|-|-|-|-|-|-|
|x||||x ||
|$µ_1=1$||||$µ_2=20$||

- Points plus proche de $µ_1$ que de $µ_2$ : 1,2,9

- Points plus proche de $µ_2$ que de $µ_1$ : 12,30

Classes à l'itération 1 : 

| 1  2 9 || 12  20 |

Barycentre de ces classes :
- Classe 1 : $(1+2+9)/3=4$
- Classe 2 : $(12+20)/2=16$

### Itération 2

| 1 | 2 || 9 | 12 || 20 |
|-|-|-|-|-|-|-|
|||x|||x||
|||$µ_1=4$|||$µ_2=16$||

- Points plus proche de $µ_1$ que de $µ_2$ : 1,2,9

- Points plus proche de $µ_2$ que de $µ_1$ : 12,30

Les classes sont stables : 

| 1  2 9 || 12  20 |

Fin de l'algorithme

---

Remarque : pour 2 tirages, on a obtenu deux classifications différentes

=> Existance d'optimum locaux

---

c)$K= 3,μ1= 1,μ2= 12 ,μ3= 20$

### Itération 1

| 1 | 2 | 9 | 12 | 20 |
|-|-|-|-|-|
|x|||x|x ||
|$µ_1=1$|||$µ_2=12$|$µ_3=20$||

- Points plus proche de $µ_1$ : 1,2
- Points plus proche de $µ_2$ : 9,12
- Points plus proche de $µ_3$ : 20

Classes à l'itération 1 : 

| 1  2 || 9 12 || 20 |

Barycentre de ces classes :
- Classe 1 : $1.5$
- Classe 2 : $10.5$
- Classe 2 : $20$

Classes stables

---

d)$K= 4,μ1= 1,μ2= 9,μ3= 12 ,μ4= 20$

### Itération 1

| 1 | 2 | 9 | 12 | 20 |
|-|-|-|-|-|
|x||x|x|x ||
|$µ_1=1$||$µ_2=9$|$µ_3=12$|$µ_4=20$||

- Points plus proche de $µ_1$ : 1,2
- Points plus proche de $µ_2$ : 9
- Points plus proche de $µ_3$ : 12
- Points plus proche de $µ_4$ : 20


Classes stables

## 1-2 Un critère de sélection

On veut :
- Classes homogènes (= Inertie intra faible)
- Classes différentes entre elles (= Inertie inter forte)

Inertie totale = Inertie intra + Inertie inter

Pour une classe $k$, $I_{INTRA_k}=\sum_{i\in k}p_id²(x_i,G_k)$

Avec :
- $i\in k$ les éléments i de la classe k
- $G_k$ le barycentre de la classe k
- $d$ une distance à définir (paramètre de la méthode)
- $p_i$ les poids relatifs au sein de la classe ($\sum_ip_i=1$ en sommant sur les individus de la classe). En l'absence d'indications, les individus sont équipondérés.

Au total, on pondère par les effectifs des classes :

$I_{INTRA} = \sum_{k=1}^K\frac{n_k}{n}I_{INTRA_k}$

Soit pour les classifications précédentes :

a)

Classe {1 2} : Barycentre=1.5 $I_{INTRA}=1/2(0.5²+0.5²)=0.25$

Classe {9 12 20} : Barycentre=13.7 $I_{INTRA}=1/3(4.7²+1.7²+6.3²)=21.6$

Soit au total $I_{INTRA}=2/5*0.25+3/5*21.6=13.06$

b)

Classe {1 2 9} : Barycentre=4 $I_{INTRA}=1/3(3²+2²+5²)=12.67$

Classe {12 20} : Barycentre=16 $I_{INTRA}=1/2(4²+4²)=16$

Soit au total $I_{INTRA}=3/5*12.67+2/5*16=14$

Dans la classification obtenue avec b), les classes sont moins homogènes

c)

Classe {1 2} : Barycentre=0.5 $I_{INTRA}=1/2(0.5²+0.5²)=0.25$

Classe {9 12} : Barycentre=10.5 $I_{INTRA}=1/2(1.5²+1.5²)=2.25$

Classe {20} : Barycentre=20 $I_{INTRA}=0$

Soit au total $I_{INTRA}=2/5*0.25+2/5*2.25+1/5*0=1$

d)

$I_{INTRA}=0.1$

:warning: Ce critère n'a de sens que si on compare des classifications avec le même nombre de classe !!!
Avec plus de classe, on a FORCÉMENT moins d'inertie intra !
Sinon la meilleure classification est celle avec n classes singleton ($I_{INTRA}$ nulle !)

# Exercice 2 : CAH

## 2-1 Une première CAH à la main

Regrouper les individus en utilisant la *classification hiérarchique ascendante* et en prenant comme mesure de similarité *la distance euclidienne* et comme critère d’agrégation *le linkage single*.

3 paramètres
- la méthode CAH, qui implique deux paramètres
- la mesure de similarité ~ distance entre points
- le critère d'aggrégation ~ distance entre classes

Rappel : distance euclidienne entre x et y : $\sqrt{\sum_{j=1}^p(x_j-y_j)²}$ 

linkage single ? $d(Classe_1,Classe_2)=min_{x\in Classe_1,y\in Classe_2}d(x,y)$
En d'autres termes, le plus petite distance possible entre un point de chacune des classe.

algorithme de CAH ?
*classification* : ok
*hierarchique* : l'output de la méthode sera une hiérachie dans laquelle on va choisir une partition (ou classification)
*ascendante* : l'état initial de l'algorithme sera les singletons (5 classes de 1 employé)

### Itération 1

Classes : |E1|E2|E3|E4|E5|

Calcul des distances entre individus :

|Employé |E1|E2|E3|E4|E5|
|- |- |- |- |- |- |
|Ancienneté| 2| 3| 5| 6| 8|
|Salaire| 2000| 2100| 3500| 4100| 10000|



|  |E1|E2|E3|E4|E5|
|- |- |- |- |- |- |
|E1| 0|100|1500|2100|8000|
|E2|  | 0|1400|2000|7900|
|E3|  |  | 0|600|6500|
|E4|  |  |  | 0|5900|
|E5|  |  |  |  | 0|

(arrondies au centième 

Entre E1 et E2 par exemple : $d(E1,E2)=\sqrt{(2000-2100)²+(3-2)²}=\sqrt{100²+1²}=\sqrt{10001}\approx \sqrt{10000}$

Remarque : On retrouve quasiment la distance en ne considérant que la variable Salaire 

Les deux individus (classes singletons) les plus proches sont E1 et E2, on les regoupe

### Itération 2

Classes : |E1 E2|E3|E4|E5|

Disatances entre classe selon le critère du linkage single (distance minimale)

|  |E1 E2|E3|E4|E5|
|- |- |- |- |- |- |
|E1 E2| 0|1400|2000|7900|
|E3|    | 0|600|6500|
|E4|    |  | 0|5900|
|E5|    |  |  | 0|

Les deux classes les plus proches : singletons E3 et E4

### Itération 3


|  |E1 E2|E3 E4|E5|
|- |- |- |- |- |- |
|E1 E2| 0|1400|2000|7900|
|E3 E4|    | 0|5900|
|E5|    |  |  0|

Les deux classes les plus proches : {E1 E2} et  {E3 E4}

### Itération 4

|  |E1 E2 E3 E4|E5|
|- |- |- |- |- |- |
|E1 E2 E3 E4| 0|5900|
|E5|    |  0|

Forcément on regroupe les deux classes restantes et on obtient une classe avec tout le monde

 **Choisir une classification**
 
 La méthode ne donne pas une mais une succesion de classification plausible
 
Il faut savoir quand s'arrêter

Pas facile avec la méthode linkage simple, souvent on utilise le critère de Ward. La distance entre classe est alors le regroupe ment qui fait perdre le moins d'inertie intra.

Avec le critère de Ward, on peut prendre en compte la "vitesse" de gain d'inertie intra lors d'un regroupement

Remarque : sous R, en utilisant FactoMineR (qui utilise lui même agnes), on peut choisir comme méthode :
```
 method: character string defining the clustering method.  The six
          methods implemented are '"average"' ([unweighted pair-]group
          [arithMetic] average method, aka 'UPGMA'), '"single"' (single
          linkage), '"complete"' (complete linkage), '"ward"' (Ward's
          method), '"weighted"' (weighted average linkage, aka
          'WPGMA'), its generalization '"flexible"' which uses (a
          constant version of) the Lance-Williams formula and the
          'par.method' argument, and '"gaverage"' a generalized
          '"average"' aka "flexible UPGMA" method also using the
          Lance-Williams formula and 'par.method'.
```



## 2-2 2-3 *Valeurs standardisées* 

Standardiser (réduire) ? un souvenir des différences entre ACP normées ou non ?

```r
      anciennete     salaire
[1,] -1.17279094 -0.71128234
[2,] -0.75393703 -0.68088566
[3,]  0.08377078 -0.25533212
[4,]  0.50262469 -0.07295204
[5,]  1.34033251  1.72045216
```

Disparition des problèmes d'ordre de grandeur entre les variables ancienneté et salaire.
Même problématique que l'ACP normée : résoudre les problèmes d'unité, de dimension,...

- nouvelles distances

```r
     [,1] [,2] [,3] [,4] [,5]
[1,]    0 0.42 1.34 1.79 3.50
[2,]    0 0.00 0.94 1.40 3.19
[3,]    0 0.00 0.00 0.46 2.34
[4,]    0 0.00 0.00 0.00 1.98
[5,]    0 0.00 0.00 0.00 0.00
```


---
Code

```r
rm(list=ls())

anciennete=c(2,3,5,6,8)
salaire=c(2000,2100,3500,4100,10000)

data=cbind(anciennete,salaire)
data=as.data.frame(data)

# On réduit les données
dataScale=as.data.frame(scale(data))

# Calcul des distances

## A la main

distance= function(i,j,data) {
    sqrt(
    rowSums((data[i,]-data[j,])**2 )
    )
}

distances= function(data){
    a= matrix(data = rep(0, 25), nrow = 5, ncol = 5)
    for (i in 1:5) {
         for (j in i:5) {
            a[i,j]=distance(i,j,data)
        }
    }
    round(a,2)
}

distances(data)
distances(dataScale)

## Avec la fonction daisy

round(daisy(data),2)
round(daisy(dataScale),2)

# CAH

require(cluster)
cah <- agnes(data, metric = "euclidean", method="single",stand = FALSE)
plot(cah)

require(FactoMineR)
res.HCPC=HCPC(data,method="single")

res.HCPC=HCPC(dataScale,method="single")
```


---

Compléments

- ACP + CAH : on effectue une ACP, on utilise un critère de sélection d'axe, et on effectue la CAH sur les données nettoyées"
```r
# Pour ne conserver que les 3 premiers axes
res.PCA<-PCA(data,scale.unit=TRUE,graph=FALSE,ncp=3)
# CAH qui utilise uniquement les 3 premiers axes factoriels 
res.HCPC=HCPC(res.PCA)
```


- Variables qualitatives ? : on effectue une ACM (on sélectionne les axes) et la CAH se fait sur les axes factoriels
```r
# Pour ne conserver que les 3 premiers axes
res.MCA<-MCA(data,scale.unit=TRUE,graph=FALSE,ncp=3)
# CAH qui utilise uniquement les 3 premiers axes factoriels de l'ACM 
res.HCPC=HCPC(res.MCA)
```

# Exercice 3 (Kmeans et variables qualitatives)
 
On considère une enquête conduite par deux étudiants d'Agrocampus sur 135 personnes visant à avoir une vue d'ensemble de leurs différentes prises de position concernant les OGM (fichier ogm.csv). Il leur a été posé un ensemble de 21 questions fermées que nous avons réparties en deux groupes.
Un premier groupe composé de seize questions en lien direct avec le rapport aux OGM qu'ont les per-
sonnes interrogées :
- Vous sentez-vous concerné par la polémique sur les OGM.
- Quelle est votre position quand à la culture d'OGM en France.
- Quelle est votre position quant à l'incorporation de matrière première OGM dans les produits alimentaires destinés à l'alimentation humaine.
- Quelle est votre position quant à l'incorporation de matrière première OGM dans les produits alimentaires destinés à l'alimentation animale.
- Avez-vous déjà participé à une manifestation contre les OGM.
- Estimez-vous que les médias communiquent suffisamment sur le sujet.
- Faîtes-vous vous-même la démarche de vous informer sur le sujet.
- Pensez-vous que les OGM puissent permettre la réduction d'usage de fongicides.
- Pensez-vous que les OGM puissent permettre la réduction des problèmes de famine dans le monde.
- Pensez-vous que les OGM puissent permettre l'amélioration des conditions de vie des agriculteurs.
- Pensez-vous que les OGM puissent permettre de futurs progrès scientifiques.
- Pensez-vous que les OGM représentent un éventuel danger pour notre santé.
- Pensez-vous que les OGM représentent une menace pour l'environnement.
- Pensez-vous que les OGM représentent un risque économique pour les agriculteurs.
- Pensez-vous que les OGM représentent un procédé scientifique inutile.
- Pensez vous que nos grands-parents avaient une alimentation plus saine.

Un second groupe composé de cinq variables de signalétique au sens large :
- Sexe
- Catégorie soci-professionnelle
- Tranche d'âge
- Exercez vous des études ou un métier en rapport avec l'agriculture, l'agroalimentaire ou la pharmaceutique
- A quel parti politique vous identifiez vous le plus

Problématique. À travers ce questionnaire, on cherche à obtenir une typologie des personnes interrogées en fonction de leur rapport aux OGM; à voir si cette typologie n'est pas sans lien avec les variables de signalétique d'autre part.
- Quels sont les éléments actifs et les élements supplémentaires?
- Quelle analyse factorielle faut-il effectuer pour étudier les dépendances entre les variables?
- On souhaite effectuer une classiffication non supervisée afin de déterminer des groupes d'opinion relatifs aux OGM. Pour cela, on souhaite utiliser la méthode des K-means. À partir des sorties logicielles, répondre aux questions suivantes
    - Quelle distance a été utilisée ?
    - Combien de classes faudrait-il considérer ? Cela est-il pertinent avec les sorties de la méthode factorielle ?
    - Interpréter les différentes classes.
    - Il y a-t-il un lien significatif entre la position vis à vis des OGM et le genre ?
    - Il y a-t-il un lien significatif entre la position vis à vis des OGM et la sensibilité politique ?

```r
rm(list=ls())
require(FactoMineR)
ogm <- read.table("./Classification/data/ogm.csv",header = TRUE,sep=";")
dim(ogm)

# Traitement des modalités rares (regroupements de Très favorable et Favorable)
plot(ogm$Position.Al.H)
prop.table(table(ogm$Position.Al.H))
levels(ogm$Position.Al.H)[4] <- levels(ogm$Position.Al.H)[1]

plot(ogm$Position.Culture)
prop.table(table(ogm$Position.Culture))
levels(ogm$Position.Culture) <- c("Favorable", "Pas Favorable du Tout", "Plutot Defavorable", "Favorable")

# On ne fait la classification que sur les variables sur les avis sur les OGM
dataActif <- ogm[,1:16]
dataToCluster <- tab.disjonctif(dataActif)

# Comparaison de k-means sur plusieurs nombre de classes
Kmax <- 10
results <- list()
criterion <- rep(NA, Kmax)
for (k in 1:Kmax){
results[[k]] <- kmeans(dataToCluster, k)
criterion[k] <- results[[k]]$tot.withinss
}
plot(1:Kmax, criterion, xlab="Number of clusters", ylab="Criterion")

# Sélection de 3 classes avec "critère du coude"
Kselec <- 3
by(ogm[,1:16], results[[Kselec]]$cluster, summary)

# Analyse fine d'une variable "active" = utilisée dans la classification
contingence = table(ogm$Position.Al.H,results[[Kselec]]$cluster)
contingence = addmargins(contingence,2)
prop.table(contingence,2)

# Analyse fine d'une variable "supplémentaire" = non utilisée dans la classification
contingence = table(ogm$Parti.Politique,results[[Kselec]]$cluster)
contingence = addmargins(contingence,2)
prop.table(contingence,2)

# Comparaison avec ACM
res <- MCA(ogm, ncp = 5, quali.sup = 17:21, graph = FALSE)
plot(res$ind$coord[,1], res$ind$coord[,2], col=results[[Kselec]]$cluster, pch=results[[Kselec]]$cluster)


by(ogm[,17:21], results[[Kselec]]$cluster, summary)

# Comparaison lien Sexe/OGM et Politique/OGM

chisq.test(results[[Kselec]]$cluster, ogm$Sexe)

contingence = table(ogm$Sexe,results[[Kselec]]$cluster)
contingence = addmargins(contingence,2)
contingence
prop.table(contingence,2)

chisq.test(results[[Kselec]]$cluster, ogm$Parti.Politique)

contingence = table(ogm$Parti.Politique,results[[Kselec]]$cluster)
contingence = addmargins(contingence)
contingence
prop.table(contingence,2)

```
