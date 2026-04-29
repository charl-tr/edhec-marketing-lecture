# CLAUDE.md — Instructions persistantes pour ce projet

## Contexte
Projet de fiches de révision pour l'examen **Marketing Research Methods** (EDHEC Business School, Semestre 2 2026, examen 30 avril 2026, 90 min, Respondus lockdown browser).

**Source** : 5 PDFs officiels du cours (S1, S2, S3, S4, S6) totalisant 275 pages.

## Repo GitHub
**https://github.com/charl-tr/edhec-marketing-lecture**

Le code de la web app vit sur ce repo. Commits propres à faire à chaque jalon (fin de chaque session extraite, fin de chaque phase).

## Objectif
Web app statique (un seul `index.html` autonome) avec fiches cutting-edge, flashcards, quiz, glossaire, recherche full-text. Doit pouvoir être ouvert en local OU déployé (Netlify) et utilisé hors-ligne.

## Méthode de travail (NON-NÉGOCIABLE)

### Principe : Structure d'abord, UI ensuite
1. **Capturer toute l'info de manière structurée** dans `content/sX.md` AVANT de toucher à l'UI
2. Pour les visuels non-textuels (tableaux complexes, schémas, captures SPSS, courbes) → **extraire l'image en PNG** dans `content/screens/sX_NN.png` et la référencer dans le fichier markdown plutôt que de la retaper avec risque d'erreur
3. **Vérifiabilité** : chaque fait dans les fiches doit être traçable à un slide précis (ex : `[S2 slide 47]`)

### Lecture des PDFs
- Limite : 20 pages par appel `Read`
- Séquencer en chunks et marquer dans `STATE.md` quels chunks sont traités
- Si une slide est ambiguë ou illisible → **pinguer l'utilisateur**, ne pas inventer

### Gestion des erreurs
- Pas d'invention. Si non sûr → marquer `⚠️ À VÉRIFIER` dans le markdown et demander
- Cross-checker chiffres/seuils/dates contre la source

## Branding EDHEC — Calqué sur edhec.edu/fr

**Référence officielle** : https://www.edhec.edu/fr — l'identité visuelle de la web app DOIT s'aligner sur celle du site institutionnel EDHEC.

**Direction artistique** : institutionnel premium, éditorial, sobre. Pas cheap, pas Duolingo, pas startup. La gamification existe (flashcards, quiz, progression) mais reste contenue dans une grammaire visuelle EDHEC stricte : géométrie nette, angles francs, typographie en capitales pour les titres.

### Spécifications relevées sur edhec.edu/fr (source de vérité)
- **Police** : `Montserrat`, sans-serif (à charger via Google Fonts)
- **Couleur primaire** : `rgb(95, 25, 55)` = `#5E1937` ✓ (confirmé par inspection)
- **Body / Nav links** : Montserrat **Bold**, 16px, line-height 24px
- **Titres hero** : Montserrat **Bold**, 56px, line-height 53.2px (line-height < font-size = très tight, éditorial)
- **Titres** : EN MAJUSCULES (uppercase, letter-spacing léger)
- **Border-radius** : **0** sur les composants (pas d'arrondis !) — rectangulaire, géométrique, institutionnel
- **Layout** : grilles strictes, beaucoup d'espace blanc, photos pleine largeur

### Couleurs (utilisation stricte)
- **Burgundy `#5E1937`** : couleur identitaire EDHEC, headers principaux, boutons primaires
- **Burgundy foncé `#3F0F23`** : hover, états actifs, accents profonds
- **Burgundy clair `#7A2447`** : gradients subtils burgundy → burgundy-light
- **Off-white `#FAFAF7`** : background principal (jamais blanc pur, plus warm/premium)
- **Crème `#EFEAE0`** : surfaces secondaires, badges
- **Ink `#1A1A1A`** : texte principal
- **Muted `#6B6B6B`** : texte secondaire
- **Border `#E8E2D8`** : bordures subtiles

**Couleurs d'accent (gamification)** :
- **Surlignage texte** : `rgba(94,25,55,0.10)` (bordeaux EDHEC transparent) — JAMAIS de jaune stabilo (cheap). Le surlignage ressort le texte sans crier.
- **Vert `#00B894`** : UNIQUEMENT feedback positif (bonne réponse, progression validée), petites pastilles, jamais en aplat
- **Rouge tamisé `#C0392B`** : UNIQUEMENT feedback négatif (mauvaise réponse), uniquement quand nécessaire
- **Jaune `#F7C642`** : RÉSERVÉ aux éléments décoratifs géométriques de l'identité EDHEC (petits rectangles dans les coins de slides), pas de surlignage texte

**Règles** :
- Burgundy = couleur dominante (60–70% de la surface colorée)
- Jaune et vert = accents ponctuels (5–10%), JAMAIS de grands aplats
- Pas de gradients criards. Gradients subtils OK : burgundy → burgundy-light, off-white → cream
- Ombres douces et profondes (pas de shadows agressives)

### Typographie (Montserrat partout)
- **Tous les textes** : `Montserrat`, sans-serif, chargée via Google Fonts (`@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@400;500;600;700;800&display=swap')`)
- **Headlines (H1, H2)** : Montserrat Bold (700), **UPPERCASE**, letter-spacing 0.02em–0.05em, tight line-height
- **H3** : Montserrat Bold, UPPERCASE, taille réduite (~14–16px), letter-spacing 0.1em (style "kicker" éditorial)
- **Body** : Montserrat Regular (400) ou Medium (500), 16px, line-height 1.5
- **Strong** : Montserrat Bold (700), pas de couleur différente (juste le poids)
- **Mono** (chiffres stats, code) : `JetBrains Mono` ou `Menlo`
- Pas d'emojis dans les fiches officielles (OK dans nav et encarts pédagogiques typés)

### Géométrie & formes
- **Border-radius : 0** sur tous les composants (cards, boutons, inputs, badges)
- Angles francs, rectangulaires
- Bordures fines 1px en `#E8E2D8` ou en burgundy
- Lignes horizontales pour séparer les sections (style éditorial)
- Beaucoup d'espace blanc, layout aéré

### Composants visuels (gamification premium)

**Progress bars** : barres fines burgundy, animation au remplissage, % visible

**Badges/achievements** :
- Pastilles rondes 24–32px, burgundy avec icône blanche
- "Streak" de révision (jours consécutifs)
- "Mastery" par session (% de quiz réussis)

**Cards** :
- `border-radius: 0` (rectangulaire strict, EDHEC institutionnel)
- Bordure 1px `#E8E2D8` OU bordure-left 4px burgundy pour les cards d'accent
- Shadow subtile : `box-shadow: 0 1px 2px rgba(0,0,0,.03)` au repos
- Hover : `translateY(-2px)` + shadow `0 4px 16px rgba(94,25,55,.08)`, transition 200ms

**Boutons** :
- `border-radius: 0` (rectangulaire)
- Primaire : burgundy plein, texte blanc UPPERCASE Montserrat Bold, padding 14px 28px, letter-spacing 0.05em
- Secondaire : transparent + bordure 1px burgundy, texte burgundy UPPERCASE, hover : remplissage burgundy
- Tertiaire : link burgundy avec underline, hover : underline plus épais
- Microinteraction : opacité 0.85 au hover, pas de scale

**Flashcards** :
- Animation flip 3D fluide (600ms cubic-bezier)
- Rectangulaires (border-radius 0)
- Recto : burgundy plein, texte blanc UPPERCASE en titre + question en regular
- Verso : off-white, bordure 1px burgundy, contenu structuré

**Quiz** :
- Options : rectangles (border-radius 0), bordure 1px `#E8E2D8`, hover bordure burgundy
- Bonne réponse : bordure 2px verte `#00B894` + checkmark inline
- Mauvaise : bordure 2px rouge tamisée `#C0392B` + shake animation léger
- Score animé qui s'incrémente

**Progression** :
- Dashboard d'accueil avec :
  - Anneau de progression (style Apple Watch) burgundy par session
  - Streak counter
  - "Next up" recommandation
- Stats de mastery par session

**Microinteractions** :
- Confetti subtil burgundy/jaune sur quiz parfait (canvas-confetti light)
- Hover lift sur les cards
- Smooth scroll partout
- Tab switch avec underline animé qui glisse

### Identité visuelle
- Logo EDHEC : SVG officiel si fourni, sinon "E" stylisé en burgundy
- Tagline : "UNLEASH TOMORROW" (présente discrètement en footer ou splash)
- Footer : "EDHEC Business School · Marketing Research Methods · S2 2026"

### Anti-patterns (à éviter absolument)
- ❌ Backgrounds jaunes ou verts en aplat
- ❌ Gradients arc-en-ciel ou criards
- ❌ Shadows agressives ou neon glows
- ❌ Border-radius extrêmes (ni 0, ni 50px)
- ❌ Trop de couleurs simultanées (max 3 couleurs visibles à l'écran)
- ❌ Emojis décoratifs partout
- ❌ Polices fantaisie ou serif décoratives
- ❌ Animations excessives qui distraient de la lecture

## Conventions de code

- **Un seul `index.html`** autonome (pas de build, pas de framework)
- HTML/CSS/JS vanilla
- Contenu chargé en JS depuis des constantes (pas d'AJAX → marche en file://)
- CSS variables pour les couleurs
- Responsive (mobile = examen révisable dans le métro)
- Mode print propre (pour version papier)

## Conventions de contenu

### Format des fiches
- Hiérarchie : `h2` (session) → `h3` (section principale) → `h4` (sous-section)
- Tableaux pour comparaisons (quali vs quanti, types d'interviews, etc.)
- Citations textuelles entre guillemets avec auteur+année
- Références complètes en bas de chaque session
- Bullets concis, pas de paragraphes verbeux

### Format des flashcards
- Recto = question courte
- Verso = réponse structurée, mémorisable

### Format des quiz
- QCM 4 options
- Une seule bonne réponse
- Explication systématique avec référence au slide

## Pédagogie (principe directeur)

L'objectif n'est pas de re-coller les slides en plus joli. C'est que l'étudiant **comprenne et retienne**.

### Règles pédagogiques
1. **Vulgariser systématiquement** : chaque concept abstrait doit avoir une explication "comme si on parlait à un ami qui débute"
2. **Exemple concret AVANT la définition** : on accroche avec un cas (ex : "Imagine que tu testes 2 pubs Instagram") puis on formalise
3. **Analogies & intuitions** : ANOVA = "tester si les groupes sont vraiment différents ou si c'est du hasard"
4. **Pourquoi avant comment** : à quoi sert ce concept ? Quel problème il résout ? Avant la mécanique
5. **Pas de blocs imbuvables** : si une idée tient en 3 lignes, ne pas la noyer dans 15
6. **Boucles de feedback rapides** : flashcards courtes, mini-quiz inline, "test toi" toutes les 2-3 sections
7. **Progression** : du simple au complexe, jamais l'inverse
8. **Anti-jargon** : si on doit utiliser un terme technique, le définir dans la phrase qui suit

### Format type d'une section
```
[Hook concret] → "Imagine que tu veux savoir si une pub fait acheter plus..."
[Idée intuitive] → "L'expérience, c'est juste ça : tester deux versions et comparer."
[Définition formelle] → Définition académique courte
[Exemple] → Cas Matrix ou WWF
[Piège classique] → Erreur fréquente à éviter
[Mini-test] → "Test toi : si tu changes 2 choses entre les groupes..."
```

### Hiérarchie visuelle pour la pédagogie
- **Encarts "💡 Intuition"** pour la vulgarisation
- **Encarts "🎯 Exemple"** pour les cas concrets
- **Encarts "⚠️ Piège"** pour les erreurs classiques
- **Encarts "✅ Test toi"** pour les boucles de feedback inline

(Les emojis de typage sont OK dans ces encarts car ils servent la lisibilité — différent des emojis décoratifs interdits.)

## Don'ts
- ❌ Inventer du contenu pour combler les trous
- ❌ Utiliser le jaune ou le vert en background
- ❌ Mettre des emojis partout dans les fiches
- ❌ Toucher à l'UI avant que `content/` soit complet et validé
- ❌ Oublier de référencer le slide source

## Workflow par session
Pour chaque session (S1, S2, S3, S4, S6) :
1. Lire les pages exhaustivement (chunks de 20)
2. Extraire les screens nécessaires en PNG dans `content/screens/`
3. Rédiger `content/sX.md` avec structure complète + références slides
4. Mettre à jour `STATE.md`
5. Pinger l'utilisateur pour validation avant la session suivante
