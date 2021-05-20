<template>
  <div id="app">
    <h5 style="text-align:center">Question {{numeroQuestion}} / {{ nombreQuestions }}</h5>
    <afficheQuestion
        :enonce="questionnaire[numeroQuestion-1].enonce"
        :reponses="questionnaire[numeroQuestion-1].reponses"
        :feedbacks="questionnaire[numeroQuestion-1].feedbacks"
        :explication="questionnaire[numeroQuestion-1].explication"
        :aide="questionnaire[numeroQuestion-1].aide"
    />
    <selectionQuestion @suivant="questionSuivante" @precedent="questionPrecedente" />
    <hr />
  </div>
</template>

<script>
import selectionQuestion from "@/components/selectionQuestion";
import afficheQuestion from "@/components/afficheQuestion";

export default {
  name: 'App',
  components: {
    selectionQuestion,
    afficheQuestion
  },
  data: function() {
    return {
      numeroQuestion: 1,
      nombreQuestions: 0,
      questionnaire: []
    }
  },
  created() {
    this.questionnaire = [
      {"id":31,"enonce":"<p>Donnez la réponse la plus précise possible.</p><p>La suite $u$ définie pour tout entier $n$ par $u_n = (-1)^n$ est:</p>","explication":"<p>Cette suite est&nbsp;majorée part tout nombre supérieur ou égal à $1$ et&nbsp;minorée par tout nombre inférieur ou égal à $-1$. Elle est donc bornée.</p>","bonneReponse":3,"reponses":["majorée","minorée","bornée","aucun des trois"],"feedbacks":["<p>oui tout à fait mais elle est aussi minorée par tout nombre inférieur ou égal à $-1$</p>","<p>oui tout à fait mais elle est aussi majorée part tout nombre supérieur ou égal à $1$</p>","","<p>On peut commencer par remarquer que $\\forall n\\in\\mathbb{N},~u_n \\leq 1$, autrement dit $u_n$ est au moins majorée...</p>"],"aide":"<p>Je vous proposer de représenter graphiquement les 10 premiers termes de cette suite.</p>"},
      {"id":6,"enonce":"<p>En physique, on relie l'énergie au repose d'une particule, $E$, à sa masse $m$ par une relation de proportionalité</p><p>$$E=\\text{constante}\\times m$$</p><p>Quelle est l'unité de la constante ?</p>","explication":"<p>L'énergie s'exprime en Joule (J) et la masse en kg. Or, la constante s'écrit $\\text{constante}=E/m$, donc son unité est le J/kg ou J.kg$^{-1}$. Il se trouve que cette unité est la même que des m$^2$.s$^{-2}$, c'est-à-dire une vitesse au carré. En effet, on sait que cette constante est le carré de la vitesse de la lumière.</p>","bonneReponse":3,"reponses":["J","J.kg","J.kg$^{-1}$","sans unité","aucune des réponses précédentes n'est correcte"],"feedbacks":["<p>Le Joule (J) est une unité d'énergie.</p>","<p>Attention aux manipulations algébriques quand tu exprimes la constante en fonction de $E$ et de $m$ pour trouver sa dimension.</p>","","<p>Une constante peut avoir une dimension.</p>","<p>Attention si tu penses que l'unité est le carré d'une vitesse, donc m$^2$.s$^{-2}$, cette unité est la même qu'une des unités proposées plus haut.</p>"],"aide":""},
      {"id":23,"enonce":"<p>La loi du déplacement de Wien dit que</p><p>$$\\lambda_{\\text{max}}=\\frac{\\text{constante}}{T}$$&nbsp; </p><p><img src=\"https://jfparmentier.fr/question_pictures/3/3d8c847.png\" class=\"u-max-full-width\"></p><p>Quelle est l'unité de la constante ?</p>","explication":"<p>La constante s'écrit $\\text{constante}=\\lambda\\,T$, donc l'unité dans le système international est le mètre Kelvin, m.K.</p>","bonneReponse":2,"reponses":["m/K","m.K","K/m","Sans dimension."],"feedbacks":["<p>Commence par exprimer la constante en fonction de $\\lambda$ et $T$.</p>","","","<p>Une constante <strong>peut</strong> avoir une dimension.</p>"],"aide":"<p>Écris que l'équation doit être homogène.</p>"},
      {"id":1022,"enonce":"<p>Un moustique s'écrase sur la vitre d'un TGV. Que dire de la force exercée par la vitre sur le moustique, par rapport à la force exercée par le moustique sur la vitre ?</p>","explication":"","bonneReponse":2,"reponses":["la force exercée par la vitre est plus grande","elles sont égales en norme","la force exercée par le moustique est plus grande"],"feedbacks":["","",""],"aide":""},
      {"id":953,"enonce":"<p>Une grandeur $a$ est reliée à une grandeur $b$ par la relation&nbsp;</p><p>$$a(x)=\\int_{0}^{x}b(x)\\text{d}&nbsp;x$$</p><p>où $x$ représente une longueur. Que dire des dimensions de $a$ et $b$?</p>","explication":"","bonneReponse":3,"reponses":["$[a]=[b]$","$[a]=[b]=1$","$[a]=[b]L$","$[a]=[b]L^{-1}$"],"feedbacks":["","","",""],"aide":""},
      {"id":887,"enonce":"<p>On considère la fronde de la figure ci-dessous.</p><p><img src=\"https://jfparmentier.fr/question_pictures/3/31383edc7.png\" class=\"u-max-full-width\"></p><p>Le travail de la tension de la corde est</p>","explication":"<p>Le mouvement de la masse $m$ est circulaire. La tension de la corde est radiale, donc le déplacement est perpendiculaire à la tension, le travail élémentaire est donc nul. Ainsi, le travail est toujours nul, quelque soit l'angle balayé par la masse $m$.</p>","bonneReponse":3,"reponses":["positif","nul sur un tour complet et non nul sur un demi-tour","toujours nul","négatif"],"feedbacks":["","","",""],"aide":""}
    ];
    this.nombreQuestions = this.questionnaire.length;
  },
  methods: {
    questionSuivante: function() {
      this.numeroQuestion = Math.min( this.numeroQuestion + 1, this.nombreQuestions);
      // revient en haut de la page
      window.scrollTo(0, 0);
    },
    questionPrecedente: function() {
      this.numeroQuestion = Math.max( this.numeroQuestion - 1, 1);
      // revient en haut de la page
      window.scrollTo(0, 0);
    }
  }
}
</script>

<style>
/*! normalize.css v3.0.2 | MIT License | git.io/normalize */

/**
 * 1. Set default font family to sans-serif.
 * 2. Prevent iOS text size adjust after orientation change, without disabling
 *    user zoom.
 */

html {
  font-family: sans-serif; /* 1 */
  -ms-text-size-adjust: 100%; /* 2 */
  -webkit-text-size-adjust: 100%; /* 2 */
}

/**
 * Remove default margin.
 */

body {
  margin: 0;
}

/* HTML5 display definitions
   ========================================================================== */

/**
 * Correct `block` display not defined for any HTML5 element in IE 8/9.
 * Correct `block` display not defined for `details` or `summary` in IE 10/11
 * and Firefox.
 * Correct `block` display not defined for `main` in IE 11.
 */

article,
aside,
details,
figcaption,
figure,
footer,
header,
hgroup,
main,
menu,
nav,
section,
summary {
  display: block;
}

/**
 * 1. Correct `inline-block` display not defined in IE 8/9.
 * 2. Normalize vertical alignment of `progress` in Chrome, Firefox, and Opera.
 */

audio,
canvas,
progress,
video {
  display: inline-block; /* 1 */
  vertical-align: baseline; /* 2 */
}

/**
 * Prevent modern browsers from displaying `audio` without controls.
 * Remove excess height in iOS 5 devices.
 */

audio:not([controls]) {
  display: none;
  height: 0;
}

/**
 * Address `[hidden]` styling not present in IE 8/9/10.
 * Hide the `template` element in IE 8/9/11, Safari, and Firefox < 22.
 */

[hidden],
template {
  display: none;
}

/* Links
   ========================================================================== */

/**
 * Remove the gray background color from active links in IE 10.
 */

a {
  background-color: transparent;
}

/**
 * Improve readability when focused and also mouse hovered in all browsers.
 */

a:active,
a:hover {
  outline: 0;
}

/* Text-level semantics
   ========================================================================== */

/**
 * Address styling not present in IE 8/9/10/11, Safari, and Chrome.
 */

abbr[title] {
  border-bottom: 1px dotted;
}

/**
 * Address style set to `bolder` in Firefox 4+, Safari, and Chrome.
 */

b,
strong {
  font-weight: bold;
}

/**
 * Address styling not present in Safari and Chrome.
 */

dfn {
  font-style: italic;
}

/**
 * Address variable `h1` font-size and margin within `section` and `article`
 * contexts in Firefox 4+, Safari, and Chrome.
 */

h1 {
  font-size: 2em;
  margin: 0.67em 0;
}

/**
 * Address styling not present in IE 8/9.
 */

mark {
  background: #ff0;
  color: #000;
}

/**
 * Address inconsistent and variable font size in all browsers.
 */

small {
  font-size: 80%;
}

/**
 * Prevent `sub` and `sup` affecting `line-height` in all browsers.
 */

sub,
sup {
  font-size: 75%;
  line-height: 0;
  position: relative;
  vertical-align: baseline;
}

sup {
  top: -0.5em;
}

sub {
  bottom: -0.25em;
}

/* Embedded content
   ========================================================================== */

/**
 * Remove border when inside `a` element in IE 8/9/10.
 */

img {
  border: 0;
}

/**
 * Correct overflow not hidden in IE 9/10/11.
 */

svg:not(:root) {
  overflow: hidden;
}

/* Grouping content
   ========================================================================== */

/**
 * Address margin not present in IE 8/9 and Safari.
 */

figure {
  margin: 1em 40px;
}

/**
 * Address differences between Firefox and other browsers.
 */

hr {
  -moz-box-sizing: content-box;
  box-sizing: content-box;
  height: 0;
}

/**
 * Contain overflow in all browsers.
 */

pre {
  overflow: auto;
}

/**
 * Address odd `em`-unit font size rendering in all browsers.
 */

code,
kbd,
pre,
samp {
  font-family: monospace, monospace;
  font-size: 1em;
}

/* Forms
   ========================================================================== */

/**
 * Known limitation: by default, Chrome and Safari on OS X allow very limited
 * styling of `select`, unless a `border` property is set.
 */

/**
 * 1. Correct color not being inherited.
 *    Known issue: affects color of disabled elements.
 * 2. Correct font properties not being inherited.
 * 3. Address margins set differently in Firefox 4+, Safari, and Chrome.
 */

button,
input,
optgroup,
select,
textarea {
  color: inherit; /* 1 */
  font: inherit; /* 2 */
  margin: 0; /* 3 */
}

/**
 * Address `overflow` set to `hidden` in IE 8/9/10/11.
 */

button {
  overflow: visible;
}

/**
 * Address inconsistent `text-transform` inheritance for `button` and `select`.
 * All other form control elements do not inherit `text-transform` values.
 * Correct `button` style inheritance in Firefox, IE 8/9/10/11, and Opera.
 * Correct `select` style inheritance in Firefox.
 */

button,
select {
  text-transform: none;
}

/**
 * 1. Avoid the WebKit bug in Android 4.0.* where (2) destroys native `audio`
 *    and `video` controls.
 * 2. Correct inability to style clickable `input` types in iOS.
 * 3. Improve usability and consistency of cursor style between image-type
 *    `input` and others.
 */

button,
html input[type="button"], /* 1 */
input[type="reset"],
input[type="submit"] {
  -webkit-appearance: button; /* 2 */
  cursor: pointer; /* 3 */
}

/**
 * Re-set default cursor for disabled elements.
 */

button[disabled],
html input[disabled] {
  cursor: default;
}

/**
 * Remove inner padding and border in Firefox 4+.
 */

button::-moz-focus-inner,
input::-moz-focus-inner {
  border: 0;
  padding: 0;
}

/**
 * Address Firefox 4+ setting `line-height` on `input` using `!important` in
 * the UA stylesheet.
 */

input {
  line-height: normal;
}

/**
 * It's recommended that you don't attempt to style these elements.
 * Firefox's implementation doesn't respect box-sizing, padding, or width.
 *
 * 1. Address box sizing set to `content-box` in IE 8/9/10.
 * 2. Remove excess padding in IE 8/9/10.
 */

input[type="checkbox"],
input[type="radio"] {
  box-sizing: border-box; /* 1 */
  padding: 0; /* 2 */
}

/**
 * Fix the cursor style for Chrome's increment/decrement buttons. For certain
 * `font-size` values of the `input`, it causes the cursor style of the
 * decrement button to change from `default` to `text`.
 */

input[type="number"]::-webkit-inner-spin-button,
input[type="number"]::-webkit-outer-spin-button {
  height: auto;
}

/**
 * 1. Address `appearance` set to `searchfield` in Safari and Chrome.
 * 2. Address `box-sizing` set to `border-box` in Safari and Chrome
 *    (include `-moz` to future-proof).
 */

input[type="search"] {
  -webkit-appearance: textfield; /* 1 */
  -moz-box-sizing: content-box;
  -webkit-box-sizing: content-box; /* 2 */
  box-sizing: content-box;
}

/**
 * Remove inner padding and search cancel button in Safari and Chrome on OS X.
 * Safari (but not Chrome) clips the cancel button when the search input has
 * padding (and `textfield` appearance).
 */

input[type="search"]::-webkit-search-cancel-button,
input[type="search"]::-webkit-search-decoration {
  -webkit-appearance: none;
}

/**
 * Define consistent border, margin, and padding.
 */

fieldset {
  border: 1px solid #c0c0c0;
  margin: 0 2px;
  padding: 0.35em 0.625em 0.75em;
}

/**
 * 1. Correct `color` not being inherited in IE 8/9/10/11.
 * 2. Remove padding so people aren't caught out if they zero out fieldsets.
 */

legend {
  border: 0; /* 1 */
  padding: 0; /* 2 */
}

/**
 * Remove default vertical scrollbar in IE 8/9/10/11.
 */

textarea {
  overflow: auto;
}

/**
 * Don't inherit the `font-weight` (applied by a rule above).
 * NOTE: the default cannot safely be changed in Chrome and Safari on OS X.
 */

optgroup {
  font-weight: bold;
}

/* Tables
   ========================================================================== */

/**
 * Remove most spacing between table cells.
 */

table {
  border-collapse: collapse;
  border-spacing: 0;
}

td,
th {
  padding: 0;
}

/*
* Skeleton V2.0.4
* Copyright 2014, Dave Gamache
* www.getskeleton.com
* Free to use under the MIT license.
* http://www.opensource.org/licenses/mit-license.php
* 12/29/2014
*/


/* Table of contents
––––––––––––––––––––––––––––––––––––––––––––––––––
- Grid
- Base Styles
- Typography
- Links
- Buttons
- Forms
- Lists
- Code
- Tables
- Spacing
- Utilities
- Clearing
- Media Queries
*/


/* Grid
–––––––––––––––––––––––––––––––––––––––––––––––––– */
.container {
  position: relative;
  width: 100%;
  max-width: 450px;
  margin: 0 auto;
  padding: 0 20px;
  box-sizing: border-box; }
.column,
.columns {
  width: 100%;
  float: left;
  box-sizing: border-box; }

/* For devices larger than 400px */
@media (min-width: 400px) {
  .container {
    width: 85%;
    padding: 0; }
}

/* For devices larger than 550px */
@media (min-width: 550px) {
  .container {
    width: 80%; }
  .column,
  .columns {
    margin-left: 4%; }
  .column:first-child,
  .columns:first-child {
    margin-left: 0; }

  .one.column,
  .one.columns                    { width: 4.66666666667%; }
  .two.columns                    { width: 13.3333333333%; }
  .three.columns                  { width: 22%;            }
  .four.columns                   { width: 30.6666666667%; }
  .five.columns                   { width: 39.3333333333%; }
  .six.columns                    { width: 48%;            }
  .seven.columns                  { width: 56.6666666667%; }
  .eight.columns                  { width: 65.3333333333%; }
  .nine.columns                   { width: 74.0%;          }
  .ten.columns                    { width: 82.6666666667%; }
  .eleven.columns                 { width: 91.3333333333%; }
  .twelve.columns                 { width: 100%; margin-left: 0; }

  .one-third.column               { width: 30.6666666667%; }
  .two-thirds.column              { width: 65.3333333333%; }

  .one-half.column                { width: 48%; }

  /* Offsets */
  .offset-by-one.column,
  .offset-by-one.columns          { margin-left: 8.66666666667%; }
  .offset-by-two.column,
  .offset-by-two.columns          { margin-left: 17.3333333333%; }
  .offset-by-three.column,
  .offset-by-three.columns        { margin-left: 26%;            }
  .offset-by-four.column,
  .offset-by-four.columns         { margin-left: 34.6666666667%; }
  .offset-by-five.column,
  .offset-by-five.columns         { margin-left: 43.3333333333%; }
  .offset-by-six.column,
  .offset-by-six.columns          { margin-left: 52%;            }
  .offset-by-seven.column,
  .offset-by-seven.columns        { margin-left: 60.6666666667%; }
  .offset-by-eight.column,
  .offset-by-eight.columns        { margin-left: 69.3333333333%; }
  .offset-by-nine.column,
  .offset-by-nine.columns         { margin-left: 78.0%;          }
  .offset-by-ten.column,
  .offset-by-ten.columns          { margin-left: 86.6666666667%; }
  .offset-by-eleven.column,
  .offset-by-eleven.columns       { margin-left: 95.3333333333%; }

  .offset-by-one-third.column,
  .offset-by-one-third.columns    { margin-left: 34.6666666667%; }
  .offset-by-two-thirds.column,
  .offset-by-two-thirds.columns   { margin-left: 69.3333333333%; }

  .offset-by-one-half.column,
  .offset-by-one-half.columns     { margin-left: 52%; }

}


/* Base Styles
–––––––––––––––––––––––––––––––––––––––––––––––––– */
/* NOTE
html is set to 62.5% so that all the REM measurements throughout Skeleton
are based on 10px sizing. So basically 1.5rem = 15px :) */
html {
  font-size: 62.5%; }
body {
  font-size: 1.5em; /* currently ems cause chrome bug misinterpreting rems on body element */
  line-height: 1.6;
  font-weight: 400;
  font-family: "Raleway", "HelveticaNeue", "Helvetica Neue", Helvetica, Arial, sans-serif;
  color: #222; }


/* Typography
–––––––––––––––––––––––––––––––––––––––––––––––––– */
h1, h2, h3, h4, h5, h6 {
  margin-top: 0;
  margin-bottom: 2rem;
  font-weight: 300; }
h1 { font-size: 4.0rem; line-height: 1.2;  letter-spacing: -.1rem;}
h2 { font-size: 3.6rem; line-height: 1.25; letter-spacing: -.1rem; }
h3 { font-size: 3.0rem; line-height: 1.3;  letter-spacing: -.1rem; }
h4 { font-size: 2.4rem; line-height: 1.35; letter-spacing: -.08rem; }
h5 { font-size: 1.8rem; line-height: 1.5;  letter-spacing: -.05rem; }
h6 { font-size: 1.5rem; line-height: 1.6;  letter-spacing: 0; }

/* Larger than phablet */
@media (min-width: 550px) {
  h1 { font-size: 5.0rem; }
  h2 { font-size: 4.2rem; }
  h3 { font-size: 3.6rem; }
  h4 { font-size: 3.0rem; }
  h5 { font-size: 2.4rem; }
  h6 { font-size: 1.5rem; }
}

p {
  margin-top: 0; }


/* Links
–––––––––––––––––––––––––––––––––––––––––––––––––– */
a {
  color: #1EAEDB; }
a:hover {
  color: #0FA0CE; }


/* Buttons
–––––––––––––––––––––––––––––––––––––––––––––––––– */
.button,
button,
input[type="submit"],
input[type="reset"],
input[type="button"] {
  display: inline-block;
  height: 38px;
  padding: 0 30px;
  color: #555;
  text-align: center;
  font-size: 11px;
  font-weight: 600;
  line-height: 38px;
  letter-spacing: .1rem;
  text-transform: uppercase;
  text-decoration: none;
  white-space: nowrap;
  background-color: transparent;
  border-radius: 4px;
  border: 1px solid #bbb;
  cursor: pointer;
  box-sizing: border-box; }
.button:hover,
button:hover,
input[type="submit"]:hover,
input[type="reset"]:hover,
input[type="button"]:hover,
.button:focus,
button:focus,
input[type="submit"]:focus,
input[type="reset"]:focus,
input[type="button"]:focus {
  color: #333;
  border-color: #888;
  outline: 0; }
.button.button-primary,
button.button-primary,
input[type="submit"].button-primary,
input[type="reset"].button-primary,
input[type="button"].button-primary {
  color: #FFF;
  background-color: #33C3F0;
  border-color: #33C3F0; }
.button.button-primary:hover,
button.button-primary:hover,
input[type="submit"].button-primary:hover,
input[type="reset"].button-primary:hover,
input[type="button"].button-primary:hover,
.button.button-primary:focus,
button.button-primary:focus,
input[type="submit"].button-primary:focus,
input[type="reset"].button-primary:focus,
input[type="button"].button-primary:focus {
  color: #FFF;
  background-color: #1EAEDB;
  border-color: #1EAEDB; }


/* Forms
–––––––––––––––––––––––––––––––––––––––––––––––––– */
input[type="email"],
input[type="number"],
input[type="search"],
input[type="text"],
input[type="tel"],
input[type="url"],
input[type="password"],
textarea,
select {
  height: 38px;
  padding: 6px 10px; /* The 6px vertically centers text on FF, ignored by Webkit */
  background-color: #fff;
  border: 1px solid #D1D1D1;
  border-radius: 4px;
  box-shadow: none;
  box-sizing: border-box; }
/* Removes awkward default styles on some inputs for iOS */
input[type="email"],
input[type="number"],
input[type="search"],
input[type="text"],
input[type="tel"],
input[type="url"],
input[type="password"],
textarea {
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none; }
textarea {
  min-height: 65px;
  padding-top: 6px;
  padding-bottom: 6px; }
input[type="email"]:focus,
input[type="number"]:focus,
input[type="search"]:focus,
input[type="text"]:focus,
input[type="tel"]:focus,
input[type="url"]:focus,
input[type="password"]:focus,
textarea:focus,
select:focus {
  border: 1px solid #33C3F0;
  outline: 0; }
label,
legend {
  display: block;
  margin-bottom: .5rem;
  font-weight: 600; }
fieldset {
  padding: 0;
  border-width: 0; }
input[type="checkbox"],
input[type="radio"] {
  display: inline; }
label > .label-body {
  display: inline-block;
  margin-left: .5rem;
  font-weight: normal; }


/* Lists
–––––––––––––––––––––––––––––––––––––––––––––––––– */
ul {
  list-style: circle inside; }
ol {
  list-style: decimal inside; }
ol, ul {
  padding-left: 0;
  margin-top: 0; }
ul ul,
ul ol,
ol ol,
ol ul {
  margin: 1.5rem 0 1.5rem 3rem;
  font-size: 90%; }
li {
  margin-bottom: 1rem; }


/* Code
–––––––––––––––––––––––––––––––––––––––––––––––––– */
code {
  padding: .2rem .5rem;
  margin: 0 .2rem;
  font-size: 90%;
  white-space: nowrap;
  background: #F1F1F1;
  border: 1px solid #E1E1E1;
  border-radius: 4px; }
pre > code {
  display: block;
  padding: 1rem 1.5rem;
  white-space: pre; }


/* Tables
–––––––––––––––––––––––––––––––––––––––––––––––––– */
th,
td {
  padding: 12px 15px;
  text-align: left;}
/*   border-bottom: 1px solid #E1E1E1; } */
th:first-child,
td:first-child {
  padding-left: 0; }
th:last-child,
td:last-child {
  padding-right: 0; }


/* Spacing
–––––––––––––––––––––––––––––––––––––––––––––––––– */
button,
.button {
  margin-bottom: 1rem; }
input,
textarea,
select,
fieldset {
  margin-bottom: 1.5rem; }
pre,
blockquote,
dl,
figure,
table,
p,
ul,
ol,
form {
  margin-bottom: 2.5rem; }


/* Utilities
–––––––––––––––––––––––––––––––––––––––––––––––––– */
.u-full-width {
  width: 100%;
  box-sizing: border-box; }
.u-max-full-width {
  max-width: 100%;
  box-sizing: border-box; }
.u-pull-right {
  float: right; }
.u-pull-left {
  float: left; }


/* Misc
–––––––––––––––––––––––––––––––––––––––––––––––––– */
hr {
  margin-top: 1rem;
  margin-bottom: 1rem;
  border-width: 0;
  border-top: 1px solid #E1E1E1; }


/* Clearing
–––––––––––––––––––––––––––––––––––––––––––––––––– */

/* Self Clearing Goodness */
.container:after,
.row:after,
.u-cf {
  content: "";
  display: table;
  clear: both; }


/* Media Queries
–––––––––––––––––––––––––––––––––––––––––––––––––– */
/*
Note: The best way to structure the use of media queries is to create the queries
near the relevant code. For example, if you wanted to change the styles for buttons
on small devices, paste the mobile query code up in the buttons section and style it
there.
*/


/* Larger than mobile */
@media (min-width: 400px) {}

/* Larger than phablet (also point when grid becomes active) */
@media (min-width: 550px) {}

/* Larger than tablet */
@media (min-width: 750px) {}

/* Larger than desktop */
@media (min-width: 1000px) {}

/* Larger than Desktop HD */
@media (min-width: 1200px) {}

.text-center {
  text-align: center;
}
.button-primary,
.button-primary:focus,
.button-primary:active {
  color: #fff;
  background-color: #2980b9;
  border-color: #2980b9;
}
.button-primary:hover {
  color: #fff;
  background-color: #2573a7;
  border-color: #2573a7;
}
.button-success,
.button-success:focus,
.button-success:active {
  color: #fff;
  background-color: #27ae60;
  border-color: #27ae60;
}
.button-success:hover {
  color: #fff;
  background-color: #239d56;
  border-color: #239d56;
}
.button-info,
.button-info:focus,
.button-info:active {
  color: #fff;
  background-color: #3498db;
  border-color: #3498db;
}
.button-info:hover {
  color: #fff;
  background-color: #258bcf;
  border-color: #258bcf;
}
.button-warning,
.button-warning:focus,
.button-warning:active {
  color: #fff;
  background-color: #f39c12;
  border-color: #f39c12;
}
.button-warning:hover {
  color: #fff;
  background-color: #e08e0b;
  border-color: #e08e0b;
}
.button-danger,
.button-danger:focus,
.button-danger:active {
  color: #fff;
  background-color: #c0392b;
  border-color: #c0392b;
}
.button-danger:hover {
  color: #fff;
  background-color: #ad3327;
  border-color: #ad3327;
}
.button.button-block {
  width: 100%;
}

.bouton-reponse {
  display: inline-block;
  padding: 10px 5px;
  margin-bottom: 0.6rem;
  color: #555;
  text-align: center;
  font-size: small;
  text-decoration: none;
  background-color: transparent;
  border-radius: 4px;
  border: 1px solid #bbb;
  cursor: pointer;
  box-sizing: border-box;
}

.bouton-reponse:hover,
.bouton-reponse:focus {
  color: #333;
  border-color: #888;
  outline: 0;
}

.bouton-vert {
  display: inline-block;
  padding: 10px 5px;
  margin-bottom: 0.6rem;
  color: #fff;
  text-align: center;
  font-size: small;
  text-decoration: none;
  background-color: #27ae60;
  border-color: #27ae60;
  border-radius: 4px;
  border: 1px solid #bbb;
  cursor: pointer;
  box-sizing: border-box;
}

.bouton-orange {
  display: inline-block;
  padding: 10px 5px;
  margin-bottom: 0.6rem;
  color: #fff;
  text-align: center;
  font-size: small;
  text-decoration: none;
  background-color: #f39c12;
  border-color: #f39c12;
  border-radius: 4px;
  border: 1px solid #bbb;
  cursor: pointer;
  box-sizing: border-box;
}


.bouton-rouge {
  display: inline-block;
  padding: 10px 5px;
  margin-bottom: 0.6rem;
  color: #fff;
  text-align: center;
  font-size: small;
  text-decoration: none;
  background-color: #c0392b;
  border-color: #c0392b;
  border-radius: 4px;
  border: 1px solid #bbb;
  cursor: pointer;
  box-sizing: border-box;
}
</style>
