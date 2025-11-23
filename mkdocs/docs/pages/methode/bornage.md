# Objectif

On souhaite transformer une variable d'un indicateur territorial (x), définie dans un intervalle ([x_{\min}, x_{\max}]), vers une valeur normalisée (y(x)) dans un intervalle ([0, 1]).

Cette transformation doit pouvoir reproduire trois types de profils :

* **linéaire**
* **logarithmique (concave)**
* **exponentiel (convexe)**

De plus, les contraintes suivantes doivent être respectées :

[
y(x_{\min}) = 0,\qquad y(x_{\max}) = 1
]

et selon la forme choisie, on contrôle la pente aux bords.

---

# ➤ Normalisation de la variable

On définit d’abord une version réduite de (x) :

[
t = \frac{x - x_{\min}}{x_{\max} - x_{\min}}
]

Ainsi :

[
t \in [0, 1],\quad t=0 \text{ quand } x=x_{\min},\quad t=1 \text{ quand } x=x_{\max}
]

Toutes les formes seront donc exprimées à partir de cette variable réduite.

---

# ➤ Fonction générale

La famille de courbes retenue est :

[
\boxed{
y(t)=\frac{e^{k t} - 1}{e^{k}-1}
}
]

où (k) est un paramètre réel permettant de contrôler la forme de la courbe.

Cette fonction présente plusieurs propriétés clés :

* Elle est strictement croissante pour tout (k).
* Elle vérifie automatiquement les conditions de bornes :

[
y(0)=0,\qquad y(1)=1
]

* Elle contient les profils linéaire, logarithmique et exponentiel comme cas particuliers.

---

# ➤ Dérivée

La pente locale est donnée par :

[
y'(t) = \frac{k, e^{k t}}{e^k - 1}
]

Ce qui permet d’analyser la forme de la courbe selon le signe de (k).

---

# ➤ Cas linéaire – (k = 0)

Lorsque (k=0), on utilise le développement de Taylor :

[
\lim_{k\to 0} \frac{e^{k t}-1}{e^k-1} = t
]

Ce qui donne simplement :

[
y(t) = t = \frac{x - x_{\min}}{x_{\max} - x_{\min}}
]

✔ Profil rectiligne
✔ Pente constante sur tout l’intervalle

---

# ➤ Cas exponentiel (convexe) – (k > 0)

Lorsque (k) est positif :

* la courbe démarre lentement,
* puis s’accélère en fin d’intervalle.

On obtient :

[
y'(0) = \frac{k}{e^k - 1} \cdot \frac{1}{x_{\max}-x_{\min}} \to 0 \quad\text{quand } k\to\infty
]

[
y'(1) = \frac{k e^k}{e^k - 1} \cdot \frac{1}{x_{\max}-x_{\min}} > \frac{1}{x_{\max}-x_{\min}}
]

Ce qui correspond exactement au comportement souhaité :

* la pente à gauche devient quasi nulle (courbe très aplatie),
* la pente à droite devient très élevée.

✔ C’est le comportement typique d’une croissance exponentielle.

---

# ➤ Cas logarithmique (concave) – (k < 0)

Lorsque (k) est négatif :

* la courbe monte vite au début,
* puis s’aplatit progressivement vers la droite.

En effet :

[
y'(0)=\frac{k}{e^k - 1} \cdot \frac{1}{x_{\max}-x_{\min}} > \frac{1}{x_{\max}-x_{\min}}
]

[
y'(1)=\frac{k e^k}{e^k - 1} \cdot \frac{1}{x_{\max}-x_{\min}} \to 0 \quad\text{quand } k\to -\infty
]

Donc :

* pente forte en début d’intervalle,
* pente faible en fin d’intervalle.

✔ Comportement typique d’une fonction de type logarithmique.

---

# ➤ Avantages de cette approche

Cette formulation unique :

* fournit un **bornage garanti entre 0 et 1** ;
* s’adapte à de nombreux comportements via un seul paramètre (k) ;
* est continue, monotone et dérivable partout ;
* permet un réglage quantitatif simple du « caractère » de la transformation.

Elle constitue donc une base rigoureuse et généralisable pour :

* normaliser des indicateurs hétérogènes ;
* indexer des valeurs dans une échelle commune ([0,1]) ;
* ajuster la sensibilité à l’évolution selon le contexte métier.

---

# ➤ Résumé

[
\boxed{
y(x)=\frac{e^{k\left(\tfrac{x-x_{\min}}{x_{\max}-x_{\min}}\right)} - 1}{e^k - 1}
}
]

* (k=0) → normalisation linéaire
* (k>0) → forme exponentielle (faible au début, forte à la fin)
* (k<0) → forme logarithmique (forte au début, faible à la fin)

---

Si tu veux, je peux maintenant :

* te générer une version Markdown prête à coller dans MkDocs,
* produire des graphes de comparaison pour différentes valeurs de (k),
* ou rajouter une section sur les dérivées aux bornes pour une justification officielle.
