# Module 03 - Skill Avance : Les Artifacts

## Qu'est-ce qu'un Artifact ?

Les Artifacts sont des sorties structurees et autonomes generees par Claude, affichees dans un panneau dedie separement de la conversation.

Source officielle: https://support.anthropic.com/fr/articles/9487310-que-sont-les-artefacts-et-comment-les-utiliser

---

## Types d'Artifacts

### Code
Generation de code dans n'importe quel langage.
Exemple d'usage: script Python, fonction JavaScript, requete SQL...

### HTML/CSS/JS interactif
Pages web completes rendues directement dans le panneau.
Ideal pour: landing pages, formulaires, interfaces simples, demos.

### SVG
Graphiques vectoriels generes et rendus visuellement.
Ideal pour: diagrammes, icones, illustrations simples.

### Markdown
Documentation structuree, README, rapports...

### React Components
Composants React interactifs avec JSX.
Ideal pour: tableaux de bord, interfaces dynamiques.

### Jeux et applications
Applications interactives completes.
Exemples testes: Snake, Tetris, calculatrices, quiz...

---

## Comment utiliser les Artifacts

1. Activer les Artifacts dans les parametres Claude (si pas deja actif)
2. Faire une demande qui necessite une sortie structuree
3. L'Artifact s'ouvre automatiquement dans le panneau droit
4. Possibilite de modifier, copier, telecharger l'Artifact
5. Iteration : demander des modifications directement en conversation

---

## Cas d'usage avances

- Generer un dashboard interactif depuis des donnees CSV
- Creer un jeu complet en une seule requete
- Construire un prototype d'interface utilisateur rapidement
- Generer des rapports HTML auto-formates
- Creer des visualisations de donnees interactives (D3.js, Chart.js)

---

## Limites

- Pas d'acces au reseau (pas de fetch/API calls)
- Pas de persistance des donnees entre sessions
- Taille limitee par la fenetre de contexte
- Certains frameworks complexes ne sont pas supportes

---

*Module cree: Juin 2026 | Source: Ressource #1 Elliott Pierret*
