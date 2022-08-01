---
jupytext:
  formats: ipynb,md:myst
  split_at_heading: true
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.11.1
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---

Nous avons déjà commencé à voir comment rendre compte d'une mesure unique avec son incertitude, nous allons maintenant voir comment rendre compte d'un groupe de résultat.

+++

# Rendre compte et exploiter

+++

## Résultat unique
```{margin}
Vous pouvez utiliser des puissances de 10 en facteur si c'est nécessaire.
```
````{important}
Un résultat de mesure unique avec incertitude doit s'écrire sous la forme :__

$$
G = (G_{mes} \pm u(G)) Unités
$$
Vous devez respectez les contraintes suivantes :
* L'incertitude de mesure doit avoir 2 chiffres significatifs
* La valeur mesurée doit avoir la même précision que l'incertitude ne mesure.
````

````{topic} Exemples
| Mise en forme | Correct/Incorrect |Explication|
|:-:|:-:|:-:|
|$U = 3.2 \pm 2.1 V$ | Correct | |
|$R = (3.2 \pm 2.1) \times 10^6 \Omega$ | Correct | |
|$R = 3.215 \pm 2.112 \Omega$ | Incorrect | Trop de chiffres significatifs|
|$R = 3.2 \pm 2 \Omega$ | Incorrect | Incohérence dans les précisions (mesure/incertitude)|
|$R = 1 \pm 2.1 \Omega$ | Incorrect | Incohérence dans les précisions (mesure/incertitude)|
````


+++

## Ensemble de résultats
```{margin}
Dans les premiers TP, l'utilisation des notebook vous obligera à surtout utiliser `numpy` et `matplotlib` pour manipuler un ensemble de résultat.
```
Pour rendre compte d'un ensemble de résultats, on peut utiliser plusieurs moyens techniques:
* Un tableau de valeurs. _En général en utilisant un tableur._
* Un graphique avec si elles sont calculer des _croix ou barres d'incertitude._

Se reporter au [document sur Python](https://pcsi3physiquestan.github.io/intro_python/notebook/plt_presentation.html#methode-generale) pour revoir la structure pour créer un graphique sous Python.

__On se rappellera l'utilisation de `errorbar` pour créer des croix d'incertitudes.__