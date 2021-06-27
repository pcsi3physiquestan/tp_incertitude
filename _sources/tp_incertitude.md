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

# Incertitudes de mesure et méthodes expérimentales.

Cette présentation théorique présente :
* les différentes parties d'une manipulation (Protocole-Observation-Exploitation)
* le concept d'incertitude. On verra de plus comment implémenter une simulation de Monte-Carlo avec Python
* quelques méthodes d'exploitation des données : l'écart normalisé, la moyenne de plusieurs résultats et la régression linéaire.

Remarque : A plusieurs reprises des éléments de code sont proposés. Vous pouvez les tester vous même en les copiant dans un fichier script que vous exécuterez. En haut à droite de chaque cellule de code, vous trouverez un petit bouton ![Bouton](./notebook/images/copie_code.png) qui vous permettra de copier le code pour le coller ensuite dans votre fichier.