---
jupytext:
  encoding: '# -*- coding: utf-8 -*-'
  formats: ipynb,md:myst
  split_at_heading: true
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.10.3
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---

# Points à retenir
Cette partie résume les méthodes à connaître. Les explications sont données dans les chapitres suivants.

## Concepts
* __Mesurande__ : Grandeur que l'on veut mesurer. Le _résultat de mesure_ est soumis à une variabilité dû aux conditions expérimentales, à la méthode, à l'opérateur. Cette variabilité est quantifité par une __incertitude__ de mesure.
* __Incertitude-Type__ : Estimation de l'incertitude comme l'écart-type de la distribution des résultats de mesurage possibles.

## Distribution
### Distribuion uniforme
* Loi de probabilité : $p(x) = \frac{1}{b-a}$
* Espérance de la distribution : $\mu = \frac{a+b}{2}$
* Ecart-type de la distribution : $\sigma = \frac{b-a}{\sqrt{12}}$
* _PYTHON_ (bibliothèque `numpy.random`) - Vecteur de N tirages :`uniform(a, b, N)`

### Distribution gaussienne
* Loi de probabilité : $p(x) = \frac{1}{\sigma \sqrt{2\pi}}\exp^{- {1 \over 2} {\left(\frac{x - \mu}{\sigma}\right)}^2}$
* Espérance de la distribution : $\mu$
* Ecart-type de la distribution : $\sigma$
* _PYTHON_ (bibliothèque `numpy.random`) - Vecteur de N tirages :`normal(a, b, N)`

## Méthode de Monte-Carlo
Pour un mesurande $Y = f(X_i)$.
1. Pour chaque mesurande directe $X_i$
    1. Pour chaque source d'incertitude estimée $u_i$ : Simulation de N tirages suivant la distribution estimée (__autour de 0__).
    2. Somme des composantes
2. Calcul des N simulations de Y.
3. Calcul de la moyenne (`mean(V)`) des N valeurs (__résultat de mesurage__) et de l'écart-type (`std(V, ddof=1)`) (__incertitude-type__).

## Rendre-compte
### Résultat unique
$$
G = (G_{mes} \pm u(G)) Unités
$$

Vous devez respectez les contraintes suivantes :
* L'incertitude de mesure doit avoir 2 chiffres significatifs
* La valeur mesure doit avoir la même précision que l'incertitude ne mesure.

### Représentation graphique
* __Avec les incertitudes de mesure.__
* _PYTHON_ (bibliothèque `matplotlib.pyplot`) - Croix d'incertitude : `errorbar(x, y, xerr=ux, yerr=uy, marker='+', linestyle='', label='Légende')`
* _PYTHON_ (bibliothèque `matplotlib.pyplot`) - Croix d'incertitude : `hist(v, bins='rice')`

## Exploitation
### Ecart normalisé :

$$\eta = \frac{g_{mes} - g_{att}}{\sqrt{u^2(g_{mes}) + u^2(g_{att})}}$$

* Si l'écart normalisé est inférieur à 2, on considérera que valeur attendue et expérience sont compatibles.
* Si l'écart normalisé est supérieur à 2, on considérera que valeur attendue et expérience ne sont pas compatibles.

__On peut utiliser l'écart normalisé sur une série de données pour vérifier leur compatibilité entre elles.__

### Régression linéaire
1. Tester l'alignement visuellement.
2. Faire la régression linéaire N fois : boucle + `polyfit(x, y, 1)` (bibliothèque `numpy`)
3. Moyenne et écart-type sur la pente et l'ordonnée à l'origine
4. Vérification graphique de la droite modèle avec les croix d'incertitude
5. Vérification par les carts normalisées entre le modèle et les mesures

