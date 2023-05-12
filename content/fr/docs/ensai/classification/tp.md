---
title: "TP Classification"
description: ""
lead: ""
# date: 2020-10-13T15:21:01+02:00
# lastmod: 2020-10-13T15:21:01+02:00
draft: false
images: []
menu:
  docs:
    parent: "classification"
weight: 120
toc: true
---


TP2 exo2

```r
rm(list = ls())
install.packages("mclust")
require(cluster)
require(pgmm)
require(FactoMineR)
require(explor)
require(VarSelLCM)
require(mclust)
data("coffee")

?coffee

summary(coffee)

coffee$Variety <- as.factor(coffee$Variety)
out.pca <- PCA(coffee, quali.sup = 1:2, graph = F)
explor(out.pca)
plot(out.pca$ind$coord[,1], out.pca$ind$coord[,2], col=coffee[,1])

?VarSelCluster
res.diago.bic <- VarSelCluster(coffee[, -c(1, 2)], 1:8, vbleSelec = F)
summary(res.diago.bic)
res.diago.icl <- VarSelCluster(coffee[, -c(1, 2)], 1:8, vbleSelec = F,
     crit.varsel = "ICL")
summary(res.diago.icl)

res.diago.bic@partitions

table(coffee[, 1], res.diago.bic@partitions@zMAP)
table(coffee[, 2], res.diago.bic@partitions@zMAP)
par(mfrow=c(1,1))
plot(out.pca$ind$coord[, 1], out.pca$ind$coord[, 2],
    col = res.diago.bic@partitions@zMAP)

sil <- silhouette(res.diago.bic@partitions@zMAP, daisy(coffee[, -c(1, 2)]))
sil <- silhouette(res.diago.icl@partitions@zMAP, daisy(coffee[, -c(1, 2)]))
plot(sil)
summary(sil)

data.with.partitions <- cbind(coffee, factor(res.diago.bic@partitions@zMAP))
?catdes
catdes(data.with.partitions, ncol(data.with.partitions))

by(coffee, res.diago.icl@partitions@zMAP, summary)
res.diago.icl@criteria@discrim

cor(coffee[res.diago.bic@partitions@zMAP == 1, -c(1, 2)])
cor(coffee[res.diago.bic@partitions@zMAP == 2, -c(1, 2)])


?Mclust
mclust.options("emModelNames")
resfull <- Mclust(coffee[, -c(1, 2)], 1:8)
summary(resfull)
resfull$parameters
table(resfull$classification, res.diago.bic@partitions@zMAP)
```



TP2 exo1

```r
##############################################################################################################
# Mélange de distributions de poissons
##############################################################################################################
rm(list = ls())

rdata <- function(n, prop, lambda) {
  g <- length(prop)
  z <- sample(1:g, n, replace = TRUE, prob = prop)
  x <- rpois(n, lambda[z])
  list(z = z, x = x)
}

oneEM <- function(x, g, tol) {
  # Init
  prop <- runif(g)
  prop <- prop / sum(prop)
  lambda <- sample(x, g)
  # Calcul loglike
  masse.cond <- sapply(1:g, function(k) dpois(x, lambda[k]) * prop[k])
  loglike <- sum(log(rowSums(masse.cond)))
  prec <- -Inf
  while ((loglike - prec) > tol) {
    # Estep
    tik <- masse.cond / rowSums(masse.cond)
    # Mstep
    prop <- colSums(tik) / sum(tik)
    lambda <- as.numeric(t(tik) %*% x) / colSums(tik)
    # Calcul loglike
    masse.cond <- sapply(1:g, function(k) dpois(x, lambda[k]) * prop[k])
    prec <- loglike
    loglike <- sum(log(rowSums(masse.cond)))
  }
  list(
    prop = prop,
    lambda = lambda,
    loglike = loglike,
    tik = tik,
    check = loglike > prec,
    masse.cond = masse.cond
  )
}

multi.EM <- function(x, g, nbinit = 20, tol = 0.01) {
  res <- replicate(nbinit, oneEM(x, g, tol), simplify = FALSE)
  res <- res[[which.max(sapply(res, function(u) u$loglike))]]
  res
}

MAPassign <- function(prob) {
  as.factor(apply(prob, 1, which.max))
}

estim.mixture <- function(x, gmax, criterion = "BIC", nbinit = 20, tol = 0.01) {
  results <- lapply(1:gmax, multi.EM, x = x, nbinit = nbinit, tol = tol)
  for (g in 1:gmax) {
    results[[g]]$partition <- MAPassign(results[[g]]$tik)
    results[[g]]$BIC <- results[[g]]$loglike - (2 * g - 1) * 0.5 * log(length(x))
    results[[g]]$ICL <- sum(log(apply(results[[g]]$masse.cond, 1, max))) - (2 * g - 1) * 0.5 * log(length(x))
  }
  if (criterion == "BIC") {
    results <- results[[which.max(sapply(results, function(u) u$BIC))]]
  } else if (criterion == "ICL") {
    results <- results[[which.max(sapply(results, function(u) u$ICL))]]
  }
  results
}

set.seed(123)
ech <- rdata(100, c(1 / 2, 1 / 2), c(5, 20))
solution <- estim.mixture(ech$x, 8)
solution$prop
solution$lambda
table(solution$partition, ech$z)


```


TP2 exo3
```r

##############################################################################################################
# Sélection de variable et gestion de données manquantes
##############################################################################################################
rm(list = ls())
require(VarSelLCM)
require(missMDA)
generdata <- function(n, r, d, epsilon) {
  z <- sample(1:2, n, replace = TRUE)
  x <- matrix(rnorm(n * r), n, r)
  x[which(z == 1), ] <- x[which(z == 1), ] + epsilon
  x[which(z == 2), ] <- x[which(z == 2), ] - epsilon
  x <- cbind(x, matrix(rnorm(n * (d - r), sd = sqrt(2)), n, d - r))
  list(z = z, x = x)
}

giveARI <- function(ech) {
  res.with <- VarSelCluster(ech$x, 2, vbleSelec = TRUE, crit.varsel = "BIC")
  res.without <- VarSelCluster(ech$x, 2, vbleSelec = FALSE)
  c(ARI(ech$z, res.with@partitions@zMAP), ARI(ech$z, res.without@partitions@zMAP))
}

set.seed(123)
all.ech <- replicate(20, generdata(100, 3, 20, 1), simplify = FALSE)
res <- sapply(all.ech, giveARI)
summary(t(res))

generdata2 <- function(n, r, d, epsilon, tau) {
  z <- sample(1:2, n, replace = TRUE)
  x <- matrix(rnorm(n * r), n, r)
  x[which(z == 1), ] <- x[which(z == 1), ] + epsilon
  x[which(z == 2), ] <- x[which(z == 2), ] - epsilon
  x <- cbind(x, matrix(rnorm(n * (d - r), sd = sqrt(2)), n, d - r))
  x.notna <- x
  for (j in 1:ncol(x)) {
    naloc <- which(runif(n) < tau)
    if (length(naloc) > 0) {
      x[naloc, j] <- NA
    }
  }
  list(z = z, x = x, x.notna = x.notna)
}

giveARI.na <- function(ech) {
  x.impute <- imputePCA(ech$x, scale = FALSE)$completeObs
  ari.geo <- ARI(ech$z, kmeans(x.impute, 2)$cluster)
  ari.mixture <- ARI(ech$z, VarSelCluster(ech$x, 2, vbleSelec = TRUE)@partitions@zMAP)
  c(ari.geo, ari.mixture)
}

set.seed(123)
all.ech <- replicate(20, generdata2(101, 3, 6, 1, .2), simplify = FALSE)
res <- sapply(all.ech, giveARI.na)
summary(t(res))



generdata3 <- function(n, r, d, epsilon, tau) {
  z <- sample(1:2, n, replace = TRUE)
  x <- matrix(rnorm(n * r), n, r)
  x[which(z == 1), ] <- x[which(z == 1), ] + epsilon
  x[which(z == 2), ] <- x[which(z == 2), ] - epsilon
  x <- cbind(x, matrix(rnorm(n * (d - r), sd = sqrt(2)), n, d - r))
  x.notna <- x
  for (j in 1:ncol(x)) {
    naloc <- which(x[, j] < tau)
    if (length(naloc) > 0) {
      x[naloc, j] <- NA
    }
  }
  list(z = z, x = x, x.notna = x.notna)
}

set.seed(123)
all.ech <- replicate(20, generdata3(101, 3, 6, 1, 1), simplify = FALSE)
res <- sapply(all.ech, giveARI.na)
summary(t(res))


```