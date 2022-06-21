---
jupytext:
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

Une autre exploitation possible de résultats expérimentaux fréquentes consiste à la vérification d'une loi physique, c'est-à-dire __d'une relation $Y=f(X)$ entre deux grandeurs physiques Y et X__.

+++

# Vérifier une loi physique

+++

## Principe général

````{note}
Par la suite, on considère qu'on a mesurée plusieurs couples $(x_i, y_i)$ avec leurs incertitudes $u(X_i), u(Y_i)$. On dispose d'un modèle théorique de l'expérience qui prévoit une relation du type $Y=f(X)$ entre les deux grandeurs.

```{margin}
On ne vérifie pas une loi physique avec un seul couple $Y, X$. Cela n'a pas de sens.
```
````

Suivant la fonction $f$, il existe des méthodes plus ou moins complexes de validation. On se limitera à trois méthodes, qu'on utilisera généralement conjointement :
1. Méthode qualitative "à l'oeil" sans le modèle (__uniquement pour une relation affine__).
2. Méthode semi-quantitative "à l'oeil" avec le modèle
3. Méthode quantitative avec les résidus et les écarts normalisés.

+++

## Vérification qualitative.

+++

### Méthode

Avant de se lancer dans des méthodes numériques et calculs plus ou moins complexes, il est important de vérifier __à l'oeil__ que l'ensemble des mesures _semblent_ compatibles avec la loi proposée. MAIS, __le seul lien mathématique appréciable à l'oeil entre deux grandeurs est la droite.__

```{important}
Pour déterminer à l'oeil si deux grandeurs sont reliées entre elles, il faud nécessairement se ramener à une relation $Y'=g(X')$ où g est l'équation d'une droite. On peut alors représenter les points $(x_i, y_i)$ avec leurs croix d'incertitudes et décider s'il est possible à l'oeil de faire passer une droite par les croix d'incertitudes.

Si c'est le cas, on peut espérer avec une relation du type $Y' = aX' + b$ et procéder à une vérification plus précise, voire (cf. suite) à une détermination de $a$ et $b$ si on ne les connait pas.

Si ce n'est pas le cas, il faut soit revoir le modèle, soit revoir les mesures.
```

_La vérification "à l'oeil" est surtout utile quand on ne connait pas tous les paramètres du modèle (la pente a par exemple) car on ne peut alors tracer un modèle et le comparer. En général, elle est suivie d'une méthode pour déterminer les paramètres inconnus._

+++

### Exemples (en ligne)

````{topic} Exemples
> * On veut mesurer la résistance $R$ d'une résistance électrique en utilisant des valeur de $U$ et $I$. Mais avant de mesurer $R$, on veut vérifier que les couples $(i_k, u_k)$ vérifient bien la loi d'Ohm $U=RI$ (sinon, son utilisation est remise en question !). On a donc tracer les couples $(i_k, u_k)$ __avec leur croix d'incertitude__.  
> Comme on ne peut tracer de droite modèle (on ne connait pas R, on le cherche !), on va simplement vérifier que les points semblent alignés, c'est-à-dire _qu'on peut tracer une droite qui passe par toutes les croix d'incertitude._
> * On veut déterminer l'indice de réfraction $n_v$ d'un verre. Pour cela on envoie un faisceau Laser dans l'air ($n_{air} = 1,000$) à la rencontre du dioptre air-verre avec un angle $i_1$ qu'on mesure et on mesure l'angle de réfraction $i_2$ ainsi que les incertitudes sur les angles. On ne peut pas :
>    * simplement tracer $i_2$ en fonction de $i_1$ et le comparer à un tracé modèle puisqu'on ne connait pas $n_v$
>    * simplement tracer $i_2$ en fonction de $i_1$ et vérifier qualitativement si la relation entre les deux est respectées car la relation $n_{air} \sin i_1 = n_v \sin i_2$ n'est pas représentée par une droite.
>
>On va alors tracer $\sin i_2$ en fonction de $\sin i_2$. Le modèle théorique prévoit alors une droite qu'on pourrait cette fois appréciser à l'oeil.
````

+++

## Comparaison semi-quantitative.

```{important}
On va tracer le nuage de points __avec les croix d'incertitude__ ET le modèle théorique (ou semi-théorique). Si le modèle passe par les croix d'incertitude, alors on peut considérer que les résultats expérimentaux sont compatibles avec le modèle théorique.
```

````{margin}
_Le modèle de comparaison n'est pas toujours complètement théorique. On peut par exemple avoir déterminé expérimentalement certaines paramètres du modèle ($R$ et $n_v$ pour les exemples précédents) puis on tracer le modèle ainsi obtenus pour __vérifier qu'il est effectivement compatible ave les résultats__ ._
````

+++

## Ecarts normalisés.
Les écarts normalisés ont déjà été présentés [précédemment](comparaison.ipynb). L'idée reste la même :
1. On calcule les écarts normalisés pour chaque ensemble $(y_{i, exp}(x_i), y_{i, th}(x_i), u(y_{i, exp}(x_i)), u(y_{i, th}(x_i))$.
2. On représente les écarts normalisés en fonction des $x_i$ et on repère les points dans l'écart normalisé est supérieur à 2 : ce sont les points problématiques qui peuvent remettre en cause la cohérence théorie-expérience.