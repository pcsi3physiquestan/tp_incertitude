---
jupytext:
  encoding: '# -*- coding: utf-8 -*-'
  formats: ipynb,md:myst,py:percent
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

Obtenir une mesure n'est en général pas suffisant, il est important d'exploiter les résultats obtenus en vue de répondre à la problématique fixée. Vous aller apprendre ici à comparer un résultat expérimental à un résultat attendu (théorique, valeur constructeur...)

+++

# Comparer un résultat expérimental avec un résultat théorique.

+++

## Comparaison qualitative.

Une première étude peut-être réalisée en comparant les intervalles associées au couple \{résultat de mesurage + incertitude de mesure\} à la valeur théorique attendue. Si la barre d'incertitude comprend la valeur théorique, on peut considérer que la théorie et l'expérience sont compatibles.

````{topic} Limites
Cette comparaison a ses limites car l'intervalle défini par l'écart-type autour du résultat de mesurage exclut des valeurs qui ont une probabilité encore importante d'être réalisée.
> Dans le cas d'une distribution gaussienne, un valeur lors d'un tirage n'a que 63% de chance de se trouver dans l'intervalle à un écart-type. On ne tient pas compte d'un tiers des valeurs en raisonnant de cette façon.
````

## Ecart-normalisé

```{margin}
Le choix d'une valeur de 2 est arbitraire mais régulièrement choisie en laboratoire ou dans l'industrie. On pourrait néanmoins choisir uine autre valeur (on choisit une valeur de 5 en physique des particules par exemple,le risque d'erreur en cas de rejet étant alors beaucoup plus faible).
```
```{important} Ecart normalisé

Pour tester la compatibilité entre une valeur attendue $g_{att}$ d'incertitude $u(g_{att})$ et un résultat de mesurage $g_{mes}$ d'incertitude $u(g_{mes})$, on calcule __l'écart normalisé__:

$$
\eta = \frac{g_{mes} - g_{att}}{\sqrt{u^2(g_{mes}) + u^2(g_{att})}}
$$

* Si l'écart normalisé est inférieur à 2, on considérera que valeur attendue et expérience sont compatibles.
* Si l'écart normalisé est supérieur à 2, on considérera que valeur attendue et expérience ne sont pas compatibles.
```

### Explication du raisonnement. (en ligne)

````{topic} Explications
On considère :
* qu'on étudie une grandeur G possèdant une valeur attendue $G_{att}$ dont la valeur est $g_{att}$ avec une incertitude $u(G_{att})$. _On supposera que la distribution suivie est une distribution gaussienne._
* on a réalise le mesurage de la grandeur G (appelé $G_{mes}$) dont le résultat de mesurage est $g_{mes}$ avec une incertitude $u(G_{mes})$. _On supposera aussi que la distribution est gaussienne._

__On veut savoir si la valeur mesurée et la valeur attendue sont cohérentes.__ On __espère__ avoir un écart nul $g_{mes} - g_{att} = 0$ mais il est évident que ce n'est pas possible car les __deux grandeurs sont soumises à une incertitude (variabilité ou manque d'information).__

Par contre, la grandeur $\Delta G = G_{mes} - G_{att}$ est aussi un mesurande qu'on peut _voir comme_ une variable aléatoire. Et si valeur attendue et expérience sont cohérentes, alors on __attend__ l'espérance de cette distribution soit 0 (_distribution centrée_).

De plus, $G_{mes}$ et $G_{att}$ étant indépendante, on peut connaître la variance de leur différence grâce aux théorèmes mathématiques sur la variance : $v_{\Delta G} = v_{G_{mes}} + v_{G_{att}}$ soit pour les écart-type:

$$
    \sigma_{\Delta G} = \sqrt{\sigma^2_{G_{mes}} + \sigma^2_{G_{att}}}
$$

En divisant $\Delta G$ par $\sigma_{\Delta G}$, on aura donc une variable aléatoire $\eta_G$ qui aura un écart-type égal à 1 (_distribution réduite_). Donc:
> Si l'expérience et les attentes (théoriques ou constructeur) sont compatibles, on attend donc que la variable aléatoire associée au mesurande ;
>
> $$
\eta_G = \frac{G_{mes} - G_{att}}{\sqrt{\sigma^2(G_{mes}) + \sigma^2(G_{att})}}
$$
> soit __une distribution centrée réduite.__

On s'est donc ramené à l'idée que pour tester la compatibilité valeur attendue-expérience, il ne faut pas attendre un écart nul mais des données compatibles avec une estimation de $\eta_G$. On rappelle qu'on ne possède pas l'allure de $\eta_G$ mais uniquement $g_{mes}, u(G_{mes}), g_{att}, u(G_{att})$, on ne peut donc qu'estimer $\eta_G$ par:

$$
\eta = \frac{g_{mes} - g_{att}}{\sqrt{u^2(G_{mes}) + u^2(G_{att})}}
$$

__Il faut donc un critère sur la valeur de $\eta$ pour savoir s'il y a compatibilité ou non.__

Il existe des tests en statistique permettant à partir d'une estimation de décider si l'hypothèse d'une distribution centrée réduite est acceptable ou non. Ces tests ne sont pas au programme, on admet que cela revient à fixer une valeur seuil pour $\eta$ et considérer que si la valeur seuil est dépassée, il n'y a pas compatibilité. Si  $\eta$ est inférieure à cette valeur seuil, il y a compatibilité.

Dans le cadre des classes préparatoires, le choix de cette valeur seuil est fixé à 2. Cela revient, dans l'hypothèse d'une distribution gaussienne, à rejeter une compatibilité avec un risque d'erreur de 5%.
````

## Exemples d'utilisation (en ligne)

```{code-cell} ipython3
:tags: [remove-cell]

from myst_nb import glue
import numpy as np
R1 = 373.1
uR1 = 3.5
R2 = 398.5
uR2 = 6.1
Rth = 370
uRth = 4

eta1 = (R1 - Rth) / np.sqrt(uR1**2 + uRth**2)
eta2 = (R2 - Rth) / np.sqrt(uR2**2 + uRth**2)
glue('eta1', eta1, display=False)
glue('eta2', eta2, display=False)
```
````{topic}  Résultat unique
On va reprendre l'exemple de l'étude d'une résistance électrique. Cela sera aussi l'occasion de comprendre graphiquement la notion d'écart normalisé. On ne refait pas toute l'étude. On supposera :
1. Cas 1 : 
    * qu'on a mesuré une valeur de résistance $R = 373,1 \pm 3,5 \Omega$
    * que le constructeur donne une valeur de résistance : $R = 370 \pm 4 \Omega$
2. Cas 2 :
    * qu'on a mesuré une valeur de résistance $R = 398,5 \pm 6,1 \Omega$
    * que le constructeur donne une valeur de résistance : $R = 370 \pm 4 \Omega$

On obtient :
* Cas 1 : $\eta =${glue:text}`eta1:.1f`
    * On peut donc conclure que la valeur constructeur et l'expérience réalisée sont compatibles.
* Cas 2 : $\eta =${glue:text}`eta2:.1f`
    * On doit considérer que la valeur constructeur et l'expérience réalisée ne sont pas compatibles.
    * __Il ne faut pas en rester là et chercher les causes de cette incompatibilité.__
````

````{topic} Analyse graphique
Puisqu'on possède les valeurs mesurées et les incertitudes, on va pouvoir faire une simulation de Monte-Carlo des grandeurs. On a réalisé N=1000000 simulations.

On représente [ci-dessous](feta_fig) (chaque ligne correspond à un cas) :
1. Les barres d'incertitudes pour la valeur expérimentales puis pour la valeur constructeur.
2. Les histogrammes des deux distributions (valeur expérimentale et valeur constructeur)

```{glue:figure} feta
:name: feta_fig
:align: center
```
````

```{code-cell} ipython3
:tags: [remove-cell]

import matplotlib.pyplot as plt
import numpy.random as rd

N = 1000000
R1_sim = rd.normal(R1, uR1, N)
R2_sim = rd.normal(R2, uR2, N)
Rt_sim = rd.normal(Rth, uRth, N)

f, ax = plt.subplots(2, 2, figsize=(9, 6), dpi=100)
f.suptitle("Vision graphique de l'écart normalisé")
ax[0][0].errorbar([1, 2], [R1, Rth], yerr=[uR1, uRth], capsize=5, capthick=1, linestyle='', marker='+', label="EN : {:.2f}".format(eta1))
xtickspos = [0, 1, 2, 3]
xtickslab = ["", "Cas 1", "Constr", ""]
ax[0][0].set_xticks(xtickspos)
ax[0][0].set_xticklabels(xtickslab)
ax[0][0].legend()

ax[1][0].errorbar([1, 2], [R2, Rth], yerr=[uR2, uRth], capsize=5, capthick=1, linestyle='', marker='+', label="EN : {:.2f}".format(eta2))
xtickspos = [0, 1, 2, 3]
xtickslab = ["", "Cas 2", "Constr", ""]
ax[1][0].set_xticks(xtickspos)
ax[1][0].set_xticklabels(xtickslab)
ax[1][0].legend()

ax[0][1].hist([R1_sim, Rt_sim], bins='rice')
ax[1][1].hist([R2_sim, Rt_sim], bins='rice')

glue("feta", f, display=False)
```

+++

### Multiples résultats
* On peut se servir de l'écart normalisé pour tester la compatibilité d'un ensemble de mesures entre elles. _On se limite en général à calculer l'écart normalisé entre la moyenne et chaque résultat._
* On peut aussi tester les écarts à un modèle (théorique ou calculé) sur plusieurs valeurs grâce à l'écart normalisé.
<!-- ```{glue:figure} focales
:name: focale_tbl
:align: center
```

On va se servir de l'écart normalisé pour comparer les différents échantillons à la valeur moyenne obtenue et voir si certaines valeurs ne sont pas problématiques. La [figure ci-après](focen_fig) montre les barre d'incertitude et les écart normalisés.

La valeur de focale ainsi mesurée est :

$f' =$ ({glue:text}`fs:.2f` $\pm$ {glue:text}`ufs:.2f`) cm

```{glue:figure} foc_en
:name: focen_fig
:align: center
```

En pratique, il faudrait analyser les résultats précédents et si certains sont incompatibles, il faudrait en chercher les causes. A défaut de chercher les causes d'incompatibilité (on ne sait pas d'où viennent ces valeurs), on pourra déjà d'exercer à repérer les échantillons problématiques.


```{code-cell} ipython3
:tags: [remove-cell]
import pandas as pd

N = 10
fs = 10 + rd.uniform(-1, 1, N)
ufs = rd.uniform(0.2, 0.5, N)

foc_tab = pd.DataFrame({
      "f' (cm)": ["{:.2f}".format(val) for val in fs],
      "u(f') (cm)": ["{:.2f}".format(val) for val in ufs]
  })

glue('focales', foc_tab, display="False")

fsm = np.mean(fs)
ufsm = np.sqrt(np.var(fs, ddof=1) / N)
glue('fs', fsm)
glue('ufs', ufsm)

en = (fs - fsm) / np.sqrt(ufs**2 + ufsm**2)

f, ax = plt.subplots(1, 2, figsize=(9, 6), dpi=100)
f.suptitle("Analyse des données des focales")

echs = np.arange(10) + 1
ax[0].set_title("Echantillons")
ax[0].errorbar(echs, fs, yerr=ufs, capsize=5, capthick=1, linestyle='', marker='+', color="black")
ax[0].plot([0, 11], [fsm, fsm], color="red")
ax[0].plot([0, 11], [fsm - ufsm, fsm - ufsm], color="red", linestyle="--")
ax[0].plot([0, 11], [fsm + ufsm, fsm + ufsm], color="red", linestyle="--")
ax[0].set_ylabel("f'(cm)")

ax[1].set_title("Ecarts normalisés")
ax[1].plot(echs, en, color="black", linestyle='', marker='+')
ax[1].set_ylabel("f'(cm)")

glue('foc_en', f, display=False)
```

```{attention}
L'utilisation de l'écart normalisé ne doit pas devenir une application d'une formule sans réflexion. Vous devez toujours vérifier que la manipulation a été réalisée correctement, même si l'écart normalisé est inférieur à 2.
``` -->