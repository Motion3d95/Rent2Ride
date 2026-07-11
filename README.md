# Rent2Ride — Édition Premium

Site vitrine complet pour une agence de location de motos en Espagne, dans
un style premium inspiré d'Airbnb : fond blanc/crème épuré, cartes ombrées,
accent corail vif. 8 pages, multilingue FR/ES/EN, calendrier de réservation,
widget WhatsApp, galerie photo, avis clients, FAQ. Site statique (HTML / CSS
/ JavaScript), sans framework — aucune installation complexe nécessaire,
modifiable directement dans VS Code.

---

## 1. Installer et ouvrir le projet dans Visual Studio Code

### Étape 1 — Installer Visual Studio Code
Si ce n'est pas déjà fait : https://code.visualstudio.com — téléchargez la
version pour votre système et installez normalement.

### Étape 2 — Récupérer les fichiers
Téléchargez le dossier `cds-premium` (ou décompressez l'archive .zip),
placez-le où vous voulez, par exemple `Documents/cds-premium`.

### Étape 3 — Ouvrir le dossier dans VS Code
**Fichier > Ouvrir un dossier...** puis sélectionnez `cds-premium`. Vous
devez voir dans l'Explorateur :

```
cds-premium/
├── index.html          → Accueil
├── catalogue.html        → Catalogue motos
├── reservation.html       → Tarifs + réservation (calendrier)
├── galerie.html            → Galerie photos
├── avis.html                 → Avis clients
├── faq.html                    → Questions fréquentes
├── conditions.html               → Conditions de location
├── contact.html                    → Contact
├── favicon.png
├── css/
│   ├── base.css                      → Couleurs, polices, header, boutons
│   └── components.css                  → Cartes, calendrier, FAQ, galerie...
├── js/
│   ├── i18n.js                           → TOUS les textes (FR/ES/EN)
│   └── main.js                             → Calendrier, prix, FAQ, WhatsApp...
└── images/
    └── ...                                    → Photos (actuellement des
                                                   images de remplacement)
```

### Étape 4 — Installer l'extension "Live Server"
1. Icône **Extensions** dans la barre de gauche (ou `Ctrl+Shift+X`)
2. Cherchez `Live Server`, installez celle de **Ritwick Dey**
3. Ouvrez `index.html`, clic droit → **"Open with Live Server"**
4. Le site s'ouvre dans votre navigateur, avec rafraîchissement automatique
   à chaque sauvegarde (`Ctrl+S`)

---

## 2. Comment modifier le site

### 2.1 — Modifier les TEXTES (FR / ES / EN)
👉 Fichier : **`js/i18n.js`**

Tous les textes du site sont regroupés ici par "clé", traduite dans les 3
langues :

```js
hero_title: {
  fr: "Louez votre moto et explorez la Costa del Sol",
  es: "Alquile su moto y explore la Costa del Sol",
  en: "Rent your bike and explore the Costa del Sol"
},
```

Remplacez le texte entre guillemets dans chaque langue, puis enregistrez.
Ne touchez jamais à la partie avant les deux-points (`hero_title:`).

### 2.2 — Modifier les PRIX
👉 Fichier : **`js/main.js`**, tout en haut, bloc `PRICING`

```js
const PRICING = {
  mt07:     { day: 55,  week: 339,  month: 1155, deposit: 300, ... },
  mt09:     { day: 75,  week: 462,  month: 1575, deposit: 500, ... },
  ...
};
```

Changez les nombres. Le calculateur de réservation utilisera automatiquement
ces nouveaux prix. ⚠️ Pensez aussi à mettre à jour les prix affichés "en
dur" dans les pages HTML (`index.html`, `catalogue.html`, `reservation.html`)
— cherchez par exemple `55 €` avec `Ctrl+F` pour les retrouver toutes.

### 2.3 — Remplacer les PHOTOS
👉 Dossier : **`images/`**

Le site est livré avec des **images de remplacement** (fond dégradé avec le
texte "PHOTO PLACEHOLDER"). Pour les remplacer :

1. Trouvez vos photos sur un site gratuit : unsplash.com, pexels.com,
   pixabay.com
2. Téléchargez, renommez **exactement** comme le fichier à remplacer, en
   `.jpg`
3. Glissez-déposez dans `images/` en confirmant le remplacement

| Fichier | Utilisé sur | Format recommandé |
|---|---|---|
| `images/hero.jpg` | Fond d'accueil | Paysage, 1920×1080 |
| `images/mt07.jpg`, `mt09.jpg`, `tracer7.jpg`, `tracer9.jpg` | Cartes motos | Paysage, 800×600 |
| `images/route-ronda.jpg`, `route-coast.jpg`, `route-villages.jpg` | Bannières pages + section itinéraires | **Portrait**, 900×1125 |
| `images/gallery-1.jpg` à `gallery-7.jpg` | Page Galerie | Carré-ish, 800×800 |
| `images/logo-header.png` | Logo dans le menu | Déjà en place |
| `favicon.png` | Icône d'onglet | Carré, 64×64 |

⚠️ **Règle importante** : tous les chemins d'image utilisés dans le CSS
(`--hero-img`, `--bike-img`, `--route-img`, `--gal-img`) commencent par un
`/` (ex: `url('/images/hero.jpg')`). Si vous ajoutez un nouvel emplacement
photo, gardez ce `/` au début, sinon l'image ne s'affichera pas (le
navigateur cherchera au mauvais endroit).

### 2.4 — Modifier les COULEURS et POLICES
👉 Fichier : **`css/base.css`**, tout en haut (`:root { ... }`)

```css
:root{
  --c-accent: #E0383A;   /* couleur principale — corail/rouge vif */
  --c-ink: #222222;      /* texte principal */
  --c-bg-cream: #FAF8F6; /* fond crème alterné */
  ...
}
```

Changez `--c-accent` pour changer la couleur principale partout sur le site
(boutons, prix, accents).

### 2.5 — Numéro WhatsApp et lien Momoven
👉 Fichier : **`js/main.js`**, tout en haut

```js
const WHATSAPP_NUMBER = "34911459813"; // PLACEHOLDER — à remplacer
const MOMOVEN_URL = "https://www.momoven.com"; // à remplacer par votre annonce
```

**Important** : `WHATSAPP_NUMBER` doit être au format international, sans
espaces ni symboles (indicatif pays + numéro). Pour l'Espagne : `34` suivi
du numéro complet. Exemple pour le numéro espagnol 911 459 813 :
`34911459813`.

Le message pré-rempli que les visiteurs voient en cliquant est modifiable
dans `js/i18n.js`, clé `wa_default_text`.

### 2.6 — Avis clients
👉 Fichier : **`js/i18n.js`**, clés `review1_*` à `review6_*`

Chaque avis a un texte, un nom et une mention (modèle + date). Remplacez le
contenu placeholder par de vrais avis. Le score global (4.9) et le nombre
total d'avis sont à modifier directement dans `avis.html` (cherchez
`rating-score` et `rating_count_label`).

### 2.7 — FAQ
👉 Fichier : **`js/i18n.js`**, clés `faq1_q`/`faq1_a` à `faq8_q`/`faq8_a`

Pour ajouter une nouvelle question, dupliquez un bloc `.faq-item` dans
`faq.html` (et `conditions.html` si pertinent) et ajoutez les clés
correspondantes (`faq9_q`, `faq9_a`) dans les 3 langues dans `i18n.js`.

---

## 3. Le calendrier de réservation

Fonctionne comme avant : sélection de dates par clic, calcul automatique du
prix selon le modèle et la durée (remise automatique à partir de 7 et 30
jours). Voir section "5. Connecter les formulaires" ci-dessous pour recevoir
les demandes par e-mail.

Astuce : les boutons "Réserver" sur les cartes motos (page d'accueil et
catalogue) pré-sélectionnent automatiquement le bon modèle dans le
formulaire de réservation.

---

## 4. Le widget WhatsApp

Bulle verte flottante en bas à droite sur toutes les pages. Au clic, un
panneau de discussion factice s'ouvre avec un message d'accueil et un
bouton qui ouvre une vraie conversation WhatsApp (avec un message
pré-rempli) dans un nouvel onglet.

Pour que ça fonctionne réellement : remplacez `WHATSAPP_NUMBER` dans
`js/main.js` par votre vrai numéro professionnel (voir section 2.5).

---

## 5. Connecter les formulaires (réservation + contact) à un vrai e-mail

Comme pour le calendrier, les formulaires de réservation et de contact ne
font actuellement qu'afficher un message de confirmation — ils n'envoient
**pas encore** d'e-mail réel.

**Option simple — Formspree ou Getform :**
1. Créez un compte gratuit sur https://formspree.io ou https://getform.io
2. Récupérez votre URL de formulaire (`https://formspree.io/f/XXXXXXX`)
3. Dans `reservation.html` et `contact.html`, ajoutez l'attribut `action`
   sur la balise `<form>` :
   `<form class="booking-form" id="bookingForm" action="https://formspree.io/f/XXXXXXX" method="POST">`
4. Dans `js/main.js`, dans `initBookingForm()` et `initContactForm()`,
   supprimez la ligne `e.preventDefault();` pour laisser le formulaire
   s'envoyer normalement

**Option avancée — votre propre serveur :** voir le commentaire `WHERE TO
SEND THE BOOKING DATA` dans `js/main.js`, qui contient un exemple de
`fetch()` à adapter.

---

## 6. Momoven

Momoven n'offre pas d'accès technique (API) permettant une vraie connexion
entre les deux sites — c'est un simple bouton/lien vers votre annonce
Momoven (voir section 2.5 pour modifier l'URL). Si Momoven propose un jour
un partenariat technique, ce lien pourra être remplacé en conséquence.

---

## 7. SEO (référencement)

Chaque page a déjà :
- une balise `<title>` et `<meta name="description">` propres à son contenu
- des intitulés `<h1>`/`<h2>` structurés
- des images avec attribut `alt` (à compléter quand vous ajoutez vos photos
  réelles — décrivez ce que montre chaque image, ex: `alt="Yamaha MT-07
  garée sur la route de Ronda"`)

Pour aller plus loin (recommandé une fois le site en ligne) :
- Créez un compte Google Search Console et soumettez votre site
- Ajoutez un fichier `sitemap.xml` listant vos 8 pages (des générateurs
  gratuits existent en ligne, ex: xml-sitemaps.com)
- Remplacez les URLs `https://www.momoven.com` et autres liens externes
  placeholder par les vraies adresses

---

## 8. Publier le site en ligne

Le site est 100% statique. Hébergement gratuit possible via :
- **Netlify** (https://netlify.com) : glissez-déposez le dossier
  `cds-premium`
- **GitHub Pages** : poussez le dossier dans un dépôt, activez "Pages"
- **Vercel** (https://vercel.com)

---

## 9. Récapitulatif rapide

| Je veux... | J'ouvre... |
|---|---|
| Changer un texte | `js/i18n.js` |
| Changer un prix | `js/main.js` (bloc `PRICING`) + pages HTML concernées |
| Changer une photo | dossier `images/` |
| Changer une couleur | `css/base.css` (haut du fichier) |
| Changer le numéro WhatsApp | `js/main.js` (`WHATSAPP_NUMBER`) |
| Changer le lien Momoven | `js/main.js` (`MOMOVEN_URL`) |
| Ajouter/modifier un avis client | `js/i18n.js` (`reviewN_*`) |
| Ajouter/modifier une question FAQ | `js/i18n.js` + `faq.html` |
| Connecter les formulaires à un vrai e-mail | voir section 5 |
| Mettre le site en ligne | voir section 8 |

Bonne route avec Rent2Ride 🏍️
