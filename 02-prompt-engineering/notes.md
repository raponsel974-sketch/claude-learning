# Module 02 - Prompt Engineering

## Definition

Le Prompt Engineering est l'art de formuler des instructions pour un LLM afin d'obtenir des reponses precises, pertinentes et de haute qualite.

---

## Structure d'un prompt efficace

### Les 6 composants cles

1. Role : Definir qui est l'IA dans ce contexte
   - "Tu es un expert en cybersecurite"
   - "Tu es un copywriter senior specialise en SaaS"

2. Contexte : Fournir les informations de fond necessaires

3. Tache : La mission precise a accomplir (verbe d'action clair)

4. Format : Comment structurer la reponse (liste, tableau, JSON, code...)

5. Exemples : Montrer ce qu'on attend (few-shot prompting)

6. Contraintes : Ce qu'il faut eviter

---

## Techniques avancees

### Chain of Thought (CoT)
Demander a l'IA de raisonner etape par etape avant de conclure.
Trigger: "Reflechis etape par etape" ou "Montre ton raisonnement"

### Zero-shot CoT
Ajouter "Let's think step by step" pour activer le raisonnement sans exemples.

### Few-shot Prompting
Fournir des exemples input/output pour guider le format et le style.

### Self-Consistency
Generer plusieurs reponses et choisir la plus coherente.

### Prompt Chaining
Decomposer une tache complexe en plusieurs prompts en sequence.
La sortie du prompt N devient l'entree du prompt N+1.

### System Prompt
Instructions de haut niveau definissant le comportement global.
Utilise dans les Projects Claude et via l'API.

---

## Le Prompt Generator de Claude

Outil integre dans claude.ai (menu > Prompt Generator).
Permet de decrire en langage naturel et obtenir un prompt optimise automatiquement.

---

## Template de prompt universel

ROLE: Tu es [expertise].
CONTEXTE: [Situation, projet, audience cible].
TACHE: [Verbe d'action + objectif precis].
FORMAT: [Structure, longueur, langue, style].
CONTRAINTES: [Ce qu'il faut eviter ou respecter].
EXEMPLE (optionnel): [Input: ... / Output: ...]

---

## Erreurs courantes

- Prompt trop vague sans precision
- Plusieurs taches non structurees dans un seul prompt
- Ne pas specifier le format de sortie
- Oublier le contexte important

---

*Module cree: Juin 2026 | En cours d'enrichissement*
