# Objectif

Lors de la normalisation d’indicateurs de nature différente, il peut être nécessaire de représenter la progression d’une valeur entre un minimum $x_{\min}$ et un maximum $x_{\max}$, mais avec des comportements visuels différents :

* **linéaire**, lorsque chaque unité a le même poids,
* **logarithmique**, lorsqu’une progression initiale doit être fortement valorisée,
* **exponentielle**, lorsqu’on souhaite au contraire amplifier les valeurs élevées.

Le but est donc **d’obtenir une seule équation** pouvant représenter ces trois comportements selon un paramètre ajustable, tout en garantissant que :

$$
y(x_{\min}) = 0,\qquad y(x_{\max}) = 1.
$$

---

# Normalisation préalable

Nous définissons d’abord :

$$
t = \frac{x - x_{\min}}{x_{\max} - x_{\min}},
$$

avec :

$$
t \in [0,1].
$$

Cette normalisation permet d’exprimer toutes les fonctions dans un même espace unifié, indépendamment des unités ou de l’échelle de départ.

---

# Conditions de forme : analyse par les dérivées

Pour piloter la forme de la courbe, plutôt que de simplement choisir une fonction arbitraire, nous regardons **le comportement de la dérivée aux bornes**, qui caractérise visuellement la croissance au début et à la fin de l’intervalle.

## 1. Forme linéaire

Une progression strictement régulière impose :

* pente constante sur tout l’intervalle,
* donc :

$$
y = t.
$$

Dans ce cas :

$$
y'(0) = y'(1) = 1.
$$

## 2. Forme logarithmique (concave)

Nous voulons un comportement typique de fonction logarithmique :

* forte progression initiale,
* amortissement progressif à l’approche du maximum.

Cela se traduit par :

$$
y'(x_{\min}) > y'(x_{\max}),
$$

et plus précisément :

$$
y'(x_{\max}) = 0,
\qquad
y'(x_{\min}) > \frac{1}{x_{\max} - x_{\min}}.
$$

## 3. Forme exponentielle (convexe)

À l’inverse, si l’on veut :

* une progression initiale faible,
* puis une forte accélération en fin de domaine,

alors on impose :

$$
y'(x_{\min}) = 0,
\qquad
y'(x_{\max}) > \frac{1}{x_{\max}-x_{\min}}.
$$

---

# Vers une équation unifiée

Nous recherchons une fonction unique capable de satisfaire :

* les mêmes bornes $y(0)=0$ et $y(1)=1$,
* des dérivées aux bornes pouvant varier continûment entre les trois cas ci-dessus.

La famille exponentielle suivante répond à toutes ces exigences :

$$
y(t) = \frac{e^{k t}-1}{e^k - 1}
$$

où $k$ est un **paramètre contrôlant la forme** :

* $k = 0$ : limite linéaire,
* $k < 0$ : dérivée forte au début et faible à la fin → forme « logarithmique »,
* $k > 0$ : dérivée faible au début et forte ensuite → forme « exponentielle ».

La dérivée est :

$$
y'(t) = \frac{k e^{k t}}{e^k - 1}.
$$

Ce terme montre immédiatement que :

* si $k>0$, $y'(t)$ augmente avec $t$, ce qui correspond à une accélération (exponentielle),
* si $k<0$, $y'(t)$ diminue avec $t$, reproduisant l’effet logarithmique,
* si $k=0$, la fonction devient linéaire.

Ainsi, **le paramètre $k$ permet d’obtenir de façon continue les trois comportements en une seule équation**.

---

# Résultat final

$$
\boxed{
y(x)=\frac{e^{k\left(\tfrac{x-x_{\min}}{x_{\max}-x_{\min}}\right)} - 1}{e^k - 1}
}
$$

Avec :

* $k=0$ : comportement linéaire pur,
* $k<0$ : comportement logarithmique (forte montée au début),
* $k>0$ : comportement exponentiel (montée accélérée en fin de course).


<!-- Interactive curve widget : coller tel quel dans la page Markdown -->
<div id="exp-normalizer" style="max-width:820px;margin:1.2rem auto;padding:1rem;border:1px solid var(--md-default-foreground,#e0e0e0);border-radius:8px;background:var(--md-surface,#fff);">
  <h3 style="margin:0 0 .5rem 0;">Visualisation interactive — paramètre <code>k</code></h3>

  <div style="display:flex;gap:1rem;flex-wrap:wrap;align-items:center;margin-bottom:.6rem;">
    <label style="font-size:.95rem;">k = <output id="kVal">0.0</output></label>
    <input id="kSlider" type="range" min="-12" max="12" step="0.1" value="0" style="flex:1;">
    <label style="font-size:.95rem;">xmin <input id="xmin" type="number" value="0" step="0.1" style="width:6rem;margin-left:.3rem"></label>
    <label style="font-size:.95rem;">xmax <input id="xmax" type="number" value="1" step="0.1" style="width:6rem;margin-left:.3rem"></label>
    <button id="resetBtn" style="margin-left:auto;padding:.3rem .6rem;border-radius:6px;border:1px solid #bbb;background:transparent;cursor:pointer">Reset</button>
  </div>

  <canvas id="curveCanvas" style="width:100%;height:320px;border-radius:6px;background:linear-gradient(180deg, rgba(0,0,0,0.01), rgba(0,0,0,0.005));"></canvas>

  <div style="display:flex;gap:1rem;flex-wrap:wrap;margin-top:.6rem;font-size:.9rem;">
    <div>y(xmin) = <strong id="ymin">0</strong></div>
    <div>y(xmax) = <strong id="ymax">1</strong></div>
    <div>y'(xmin) = <strong id="dLeft">—</strong></div>
    <div>y'(xmax) = <strong id="dRight">—</strong></div>
    <div style="margin-left:auto">Exemple : x = <input id="xSample" type="number" value="0.25" step="0.01" style="width:6rem;margin-left:.3rem"> → y = <strong id="ySample">—</strong></div>
  </div>
</div>

<script>
(function(){
  // DOM
  const canvas = document.getElementById('curveCanvas');
  const kSlider = document.getElementById('kSlider');
  const kVal = document.getElementById('kVal');
  const xminInput = document.getElementById('xmin');
  const xmaxInput = document.getElementById('xmax');
  const dLeftEl = document.getElementById('dLeft');
  const dRightEl = document.getElementById('dRight');
  const yminEl = document.getElementById('ymin');
  const ymaxEl = document.getElementById('ymax');
  const xSample = document.getElementById('xSample');
  const ySample = document.getElementById('ySample');
  const resetBtn = document.getElementById('resetBtn');

  // HiDPI setup
  function resizeCanvas() {
    const dpr = window.devicePixelRatio || 1;
    const rect = canvas.getBoundingClientRect();
    canvas.width = Math.max(300, Math.floor(rect.width * dpr));
    canvas.height = Math.max(200, Math.floor(rect.height * dpr));
    ctx.setTransform(dpr,0,0,dpr,0,0);
    draw();
  }

  const ctx = canvas.getContext('2d');

  // Utility: safe expm1 and fallback
  function expm1(x){
    if (Math.expm1) return Math.expm1(x);
    return Math.exp(x) - 1;
  }

  // The normalized function y(t)
  function y_of_t(k,t){
    // Handle k ~ 0 with limit = identity
    if (Math.abs(k) < 1e-6) return t;
    const num = Math.exp(k*t) - 1;
    const den = Math.exp(k) - 1;
    return num / den;
  }

  // Derivative wrt x: y'(x) = (k e^{k t} / (e^k - 1)) * (1/(xmax-xmin))
  function dy_dx(k, t, dx){
    if (Math.abs(k) < 1e-8) return 1 / dx; // derivative of linear t w.r.t x
    const den = Math.exp(k) - 1;
    return (k * Math.exp(k * t) / den) / dx;
  }

  // Drawing
  function draw(){
    const rect = canvas.getBoundingClientRect();
    const W = rect.width;
    const H = rect.height;
    ctx.clearRect(0,0,W,H);

    // Read inputs
    const k = parseFloat(kSlider.value);
    const xmin = parseFloat(xminInput.value);
    const xmax = parseFloat(xmaxInput.value);
    const dx = xmax - xmin || 1;

    // Update displays
    kVal.textContent = parseFloat(k).toFixed(2);
    yminEl.textContent = formatNumber(y_of_t(k,0));
    ymaxEl.textContent = formatNumber(y_of_t(k,1));
    dLeftEl.textContent = formatNumber(dy_dx(k,0,dx));
    dRightEl.textContent = formatNumber(dy_dx(k,1,dx));

    // sample
    const xs = parseFloat(xSample.value);
    const ts = (xs - xmin) / dx;
    const yS = y_of_t(k, ts);
    ySample.textContent = formatNumber(yS);

    // draw axes and grid (simple)
    ctx.save();
    ctx.lineWidth = 1;
    ctx.strokeStyle = 'rgba(0,0,0,0.08)';
    // horizontal grid
    for (let i=0;i<=4;i++){
      const yy = 10 + (H-20) * (i/4);
      ctx.beginPath(); ctx.moveTo(10,yy); ctx.lineTo(W-10,yy); ctx.stroke();
    }
    // axes
    ctx.strokeStyle = 'rgba(0,0,0,0.35)';
    ctx.beginPath(); ctx.moveTo(40,H-30); ctx.lineTo(W-10,H-30); // x axis
    ctx.moveTo(40,H-30); ctx.lineTo(40,10); // y axis
    ctx.stroke();

    // labels
    ctx.fillStyle = 'rgba(0,0,0,0.6)';
    ctx.font = '12px system-ui, sans-serif';
    ctx.fillText('x', W-20, H-12);
    ctx.fillText('y', 18, 18);

    // plot curve
    const plotX0 = 40;
    const plotY0 = 10;
    const plotW = W - 60;
    const plotH = H - 40;

    ctx.beginPath();
    const steps = Math.max(120, Math.floor(plotW));
    for (let i=0;i<=steps;i++){
      const u = i / steps;
      const xVal = xmin + u * (xmax - xmin);
      const t = (xVal - xmin) / dx;
      const y = y_of_t(k, t);
      const px = plotX0 + u * plotW;
      const py = plotY0 + (1 - y) * plotH;
      if (i===0) ctx.moveTo(px,py); else ctx.lineTo(px,py);
    }
    ctx.lineWidth = 2.5;
    ctx.strokeStyle = 'rgba(40, 120, 220, 0.95)';
    ctx.stroke();

    // mark sample point
    const uSample = Math.max(0, Math.min(1, (xs - xmin) / dx));
    const pxS = plotX0 + uSample * plotW;
    const pyS = plotY0 + (1 - yS) * plotH;
    ctx.fillStyle = 'rgba(220,80,80,0.95)';
    ctx.beginPath(); ctx.arc(pxS,pyS,4,0,Math.PI*2); ctx.fill();

    // ticks on x for xmin and xmax
    ctx.fillStyle = 'rgba(0,0,0,0.7)';
    ctx.font = '11px system-ui, sans-serif';
    ctx.fillText(String(xmin), plotX0-4, H-12);
    ctx.fillText(String(xmax), plotX0 + plotW - 18, H-12);

    ctx.restore();
  }

  function formatNumber(n){
    if (!isFinite(n)) return '∞';
    const a = Math.abs(n);
    if (a >= 1e6) return n.toExponential(3);
    if (a < 0.0001 && a !== 0) return n.toExponential(3);
    return parseFloat(n.toFixed(4)).toString();
  }

  // Events
  function scheduleDraw(){ window.requestAnimationFrame(draw); }

  kSlider.addEventListener('input', scheduleDraw);
  xminInput.addEventListener('input', scheduleDraw);
  xmaxInput.addEventListener('input', scheduleDraw);
  xSample.addEventListener('input', scheduleDraw);
  resetBtn.addEventListener('click', function(){
    kSlider.value = 0; xminInput.value = 0; xmaxInput.value = 1; xSample.value = 0.25;
    scheduleDraw();
  });

  window.addEventListener('resize', resizeCanvas);

  // initial setup
  resizeCanvas();
})();
</script>

---

Cette équation permet donc de :

* normaliser n’importe quelle mesure dans l’intervalle $[0,1]$,
* choisir le « style » de progression avec un seul paramètre,
* justifier mathématiquement le comportement de la transformation par l’analyse de la dérivée aux bornes.
