# BLUEPRINT — Architecture & Roadmap

## Vision produit
Une web app de révision **cutting-edge**, sobre, à l'identité EDHEC, qui permet à un étudiant de :
1. **Lire** des fiches de synthèse complètes par session
2. **Mémoriser activement** via flashcards et quiz
3. **Chercher** rapidement n'importe quel concept
4. **Imprimer** une version papier propre

Cible utilisateur : étudiant EDHEC en révision active la veille de l'examen.

## Stack technique
- **HTML/CSS/JS vanilla** — un seul fichier `index.html`
- Pas de build, pas de dépendances, pas de backend
- Contenu hardcodé en JS (chargé depuis `content/*.md` au moment du build via script Node ou copié manuellement — choix à faire)
- Hébergeable sur Netlify, GitHub Pages, ou simplement `file://`

## Architecture de fichiers

```
mkt-val/
├── CLAUDE.md            # Instructions persistantes pour l'agent
├── BLUEPRINT.md         # Ce fichier
├── STATE.md             # Tableau de bord d'avancement
├── *.pdf                # Sources officielles (5 PDFs)
├── index.html           # Application finale (un seul fichier)
├── content/
│   ├── s1.md            # Fiche structurée Session 1
│   ├── s2.md            # Session 2
│   ├── s3.md            # Session 3
│   ├── s4.md            # Session 4
│   ├── s6.md            # Session 6
│   ├── glossary.md      # Glossaire transversal
│   ├── flashcards.md    # Banque de flashcards
│   ├── quiz.md          # Banque de questions QCM
│   └── screens/
│       ├── s1_29.png    # Screen extrait du slide 29 de S1
│       ├── s2_47.png    # ...
│       └── ...
└── build.sh             # (optionnel) Script pour injecter content/* dans index.html
```

## Format des fichiers content/sX.md

```markdown
# S2 · Quantitative Methods Guidelines

> **Source** : S2_Quantitative_Methods_Guidelines_v2_IG_clean.pdf (64 pages)
> **Pages couvertes** : 1–64 ✅
> **Statut** : Complet / Partiel / À vérifier

## Section 1 — Titre [slide 5–8]

### 1.1. Sous-section [slide 5]

Texte de la fiche.

> Citation exacte du slide entre blockquote.

**Référence** : Auteur (Année), Journal.

![Description du screen](screens/s2_05.png)

---

## ⚠️ À vérifier
- Slide 23 : ambiguïté sur la valeur de X — clarifier avec l'utilisateur
```

## Composants UI cibles

### Navigation
- Header sticky avec recherche full-text
- Tabs horizontales : Accueil | S1 | S2 | S3 | S4 | S6 | Glossaire | Flashcards | Quiz

### Vues
1. **Accueil** : table des matières, stratégie de révision, points clés transversaux
2. **Session X** : fiche complète, ancrée par slide source
3. **Glossaire** : ~60 entrées alphabétiques
4. **Flashcards** : carte recto/verso avec animation flip
5. **Quiz** : 25+ QCM auto-corrigés, score sticky
6. **Recherche** : résultats agrégés avec snippets surlignés

### Mode print
- Cacher nav, search, boutons interactifs
- Toutes les sessions affichées en séquence
- Saut de page propre entre sections

## Roadmap d'exécution

### Phase 0 — Gouvernance ✅
- [x] CLAUDE.md
- [x] BLUEPRINT.md
- [x] STATE.md
- [x] Structure dossiers

### Phase 1 — Extraction structurée
- [ ] S3 (9p) — le plus court, pour rodage
- [ ] S1 (83p) — extraction + screens
- [ ] S2 (64p) — extraction + screens
- [ ] S4 (43p) — extraction + screens
- [ ] S6 (76p) — extraction + screens (le plus dense, SPSS captures)

### Phase 2 — Construction transversale
- [ ] Glossaire consolidé
- [ ] Banque de flashcards (~30 cartes)
- [ ] Banque de quiz (~30 questions)

### Phase 3 — UI re-build
- [ ] Refonte index.html avec branding strict (burgundy + surlignages uniquement)
- [ ] Intégration des screens
- [ ] Mode print
- [ ] Test responsive

### Phase 4 — Polish
- [ ] Logo EDHEC officiel (si fourni par l'utilisateur)
- [ ] Mode examen blanc avec timer 90 min
- [ ] Export PDF
- [ ] Déploiement Netlify (optionnel)

## Décisions techniques à confirmer
1. **Comment injecter `content/*.md` dans `index.html` ?**
   - Option A : copier-coller manuel dans des constantes JS (simple, mais désynchro possible)
   - Option B : script `build.sh` qui parse les MD et génère le HTML (propre, mais ajoute complexité)
   - **Recommandation** : Option A pour la V1 (deadline serrée), Option B en Phase 4 si temps

2. **Logo EDHEC** : utilisateur fournit-il un SVG officiel ?

3. **Hébergement** : local file:// suffit, ou besoin Netlify ?
