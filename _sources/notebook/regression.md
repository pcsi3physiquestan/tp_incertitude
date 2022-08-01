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

Comme évoqué précédement, on est souvent dans la situation où l'on ne connait pas tous les paramètres d'une loi physique à vérifier. On doit donc déterminer, à partir des données expérimentales, les paramètres inconnues de la loi de sorte que la loi obtenus soit "la plus cohérente" avec les résultats expérimentaux. On parle __d'ajustement ou de régression.__

+++

# Ajustement d'un modèle affine

```{important}
On peut réaliser l'ajustement d'un modèle quelconque a priori. Mais dans le cadre du programme, on se limitera à des méthodes d'ajustement de modèle affine (appelé par abus de langage modèle linéaire) : $Y = aX + b$.
```

+++

## Méthode générale

Avant de rentrer dans la méthodes d'ajustment du modèle, __il convient d'être méthodique__. On suppose qu'on a un ensemble de mesures qui amène à construire deux mesurandes $Y$ et $X$ dont le modèle théorique les reliant est de la forme:

$$
Y = aX + b
$$

où $a$ et $b$ ne sont pas connus. On a alors réalisé une série de mesure amenant au calcul des couples $(x_i, y_i)$ (on considèrera qu'il y a k mesures en tout : $i \in \{1, 2, \ldots, k\}$ avec leurs incertitudes.

On doit alors :
1. Tracer les croix d'incertitude autour des points $(x_i, y_i)$ et vérifier qu'on peut espérer faire passer une droite par les croix d'incertitude (__vérification qualitative__).
2. Estimer au moins les paramètres $a$ et $b$ compatibles avec les points de mesures et si nécessaire l'incertitude sur les paramètres $a$ et $b$.
3. Tracer les points de mesures ET le modèle pour vérifier que le modèle passe par les croix d'incertitude (__vérification semi-qualitative__).
4. _Si ce n'est pas le cas_, on calculera les __écarts normalisés__ pour voir s'il y a effectivement incompatibilité.

```{margin}
Dans les premiers TPs, les écarts normalisés seront systématiquement tracés pour s'entraîner à les calculs (sous Python notamment) et à les analyser.
```

Seul le point 2. n'a pas encore été développés. On va voir comment on s'y prend.

+++

## Régression linéaire : Méthode des moindres carrés.

Pour déterminer $a$, $b$, on va utiliser une méthode particulière appelée __méthode des moindres carrés__, cette méthode est démontrées comme étant l'une meilleures estimations de $a$ et $b$ dans de nombreux cas. Leurs incertitudes $u(a)$ et $u(b)$ seront déterminées par une méthode de Monte-Carlo (en répétant donc la méthode des moindres carrés avec des échantillons tirés aléatoirement à partir des distributions statistiques).

````{important}
En pratique, on utilisera des logiciels pour appliquer la méthode des moindres carrés:
* la fonction `numpy.polyfit` sous [Python](https://pcsi3physiquestan.github.io/intro_python/notebook/np_polyfit.html#numpy-polyfit)
* la fonction `DROITEREG` sous LibreOffice ou Excel. Son utilisation sera expliqué en temps voulu.
````
+++

### Explication de la méthode.

Cf. [explications ici](https://pcsi3physiquestan.github.io/intro_python/notebook/np_polyfit.html)


```{attention}
La méthode des moindres carrés proposées ci-dessus n'est optimale que si les incertitudes sur les abscisses sont faibles voire nulles. On veillera donc __toujours à placer en abscisses les grandeurs les moins incertaines__, quitte à inverser $X$ et $Y$.
```
