# Objectif

Lors de la normalisation d’indicateurs de nature différente, il peut être nécessaire de représenter la progression d’une valeur entre un minimum (x_{\min}) et un maximum (x_{\max}), mais avec des comportements visuels différents :

* **linéaire**, lorsque chaque unité a le même poids,
* **logarithmique**, lorsqu’une progression initiale doit être fortement valorisée,
* **exponentielle**, lorsqu’on souhaite au contraire amplifier les valeurs élevées.

Le but est donc **d’obtenir une seule équation** pouvant représenter ces trois comportements selon un paramètre ajustable, tout en garantissant que :

[
y(x_{\min}) = 0,\qquad y(x_{\max}) = 1.
]

---

# Normalisation préalable

Nous définissons d’abord :

[
t = \frac{x - x_{\min}}{x_{\max} - x_{\min}},
]

avec :

[
t\in[0,1].
]

Cette normalisation permet d’exprimer toutes les fonctions dans un même espace unifié, indépendamment des unités ou de l’échelle de départ.

---

# Conditions de forme : analyse par les dérivées

Pour piloter la forme de la courbe, plutôt que de simplement choisir une fonction arbitraire, nous regardons **le comportement de la dérivée aux bornes**, qui caractérise visuellement la croissance au début et à la fin de l’intervalle.

## 1. Forme linéaire

Une progression strictement régulière impose :

* pente constante sur tout l’intervalle,
* donc :

[
y = t.
]

Dans ce cas :

[
y'(0) = y'(1) = 1.
]

## 2. Forme logarithmique (concave)

Nous voulons un comportement typique de fonction logarithmique :

* forte progression initiale,
* amortissement progressif à l’approche du maximum.

Cela se traduit par :

[
y'(x_{\min}) > y'(x_{\max}),
]

et plus précisément :

[
y'(x_{\max}) = 0,
\qquad
y'(x_{\min}) > \frac{1}{x_{\max} - x_{\min}}.
]

## 3. Forme exponentielle (convexe)

À l’inverse, si l’on veut :

* une progression initiale faible,
* puis une forte accélération en fin de domaine,

alors on impose :

[
y'(x_{\min}) = 0,
\qquad
y'(x_{\max}) > \frac{1}{x_{\max}-x_{\min}}.
]

---

# Vers une équation unifiée

Nous recherchons une fonction unique capable de satisfaire :

* les mêmes bornes (y(0)=0) et (y(1)=1),
* des dérivées aux bornes pouvant varier continûment entre les trois cas ci-dessus.

La famille exponentielle suivante répond à toutes ces exigences :

[
y(t) = \frac{e^{k t}-1}{e^k - 1}
]

où (k) est un **paramètre contrôlant la forme** :

* (k = 0) : limite linéaire,
* (k < 0) : dérivée forte au début et faible à la fin → forme « logarithmique »,
* (k > 0) : dérivée faible au début et forte ensuite → forme « exponentielle ».

La dérivée est :

[
y'(t) = \frac{k e^{k t}}{e^k - 1}.
]

Ce terme montre immédiatement que :

* si (k>0), (y'(t)) augmente avec (t), ce qui correspond à une accélération (exponentielle),
* si (k<0), (y'(t)) diminue avec (t), reproduisant l’effet logarithmique,
* si (k=0), la fonction devient linéaire.

Ainsi, **le paramètre (k) permet d’obtenir de façon continue les trois comportements en une seule équation**.

---

# Résultat final

[
\boxed{
y(x)=\frac{e^{k\left(\tfrac{x-x_{\min}}{x_{\max}-x_{\min}}\right)} - 1}{e^k - 1}
}
]

Avec :

* (k=0) : comportement linéaire pur,
* (k<0) : comportement logarithmique (forte montée au début),
* (k>0) : comportement exponentiel (montée accélérée en fin de course).

Cette équation permet donc de :

* normaliser n’importe quelle mesure dans l’intervalle ([0,1]),
* choisir le « style » de progression avec un seul paramètre,
* justifier mathématiquement le comportement de la transformation par l’analyse de la dérivée aux bornes.
