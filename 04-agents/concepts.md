# Module 04 - Agents IA : Concepts Fondamentaux

## Qu'est-ce qu'un Agent IA ?

Un agent IA est un systeme capable de percevoir son environnement, de prendre des decisions et d'executer des actions de maniere autonome pour atteindre un objectif donne.

Contrairement a un simple modele de langage (LLM) qui repond a une requete, un agent peut :
- Planifier une sequence d'actions
- Utiliser des outils (recherche web, code, API, fichiers)
- Memoriser et utiliser un contexte sur le long terme
- S'auto-corriger en cas d'erreur
- Deleguer a d'autres agents

---

## Les composants d'un agent

### 1. Le Cerveau (LLM)
Le modele de langage qui raisonne, planifie et decide. Ex: Claude, GPT-4, Gemini.

### 2. La Memoire
- Memoire court terme : contexte de la conversation en cours
- Memoire long terme : base de donnees, fichiers, vector stores
- Memoire de travail : resultats intermediaires

### 3. Les Outils (Tools / Skills)
Capacites que l'agent peut appeler pour agir dans le monde :
- Recherche web
- Execution de code
- Lecture/ecriture de fichiers
- Appels API
- Navigation web
- Envoi d'emails

### 4. Le Planificateur
Strategie de decomposition des taches complexes en etapes simples.
Patterns communs :
- ReAct (Reason + Act)
- Chain of Thought (CoT)
- Tree of Thoughts (ToT)
- MRKL (Modular Reasoning, Knowledge and Language)

### 5. L'Orchestrateur
Module qui coordonne l'execution : quel outil appeler, dans quel ordre, comment gerer les erreurs.

---

## Types d'architectures agents

### Agent Simple (Single Agent)
Un seul agent avec acces a plusieurs outils. Simple mais limite en complexite.

### Multi-Agent
Plusieurs agents specialises qui collaborent. Ex: un agent Planificateur + un agent Executeur + un agent Verificateur.

### Agent Hierarchique
Un agent superviseur qui delegue a des sous-agents. Permet de paralleliser les taches.

### Agent en Pipeline
Chaine d'agents ou la sortie de l'un est l'entree du suivant.

---

## Concepts cles a maitriser

- **Tool Calling** : mecanisme par lequel le LLM decide d'appeler un outil
- **Function Calling** : implementation technique du tool calling (JSON schema)
- **RAG** (Retrieval-Augmented Generation) : enrichir le contexte avec des docs externes
- **Vector Database** : stocker et retrouver des informations semantiquement proches
- **Embedding** : representation vectorielle du texte pour la recherche semantique
- **Agentic Loop** : boucle perception -> reflexion -> action -> observation

---

## Frameworks et outils (a approfondir)

- **LangChain** : framework Python pour construire des agents LLM
- **LangGraph** : extension LangChain pour agents avec graphe d'etat
- **AutoGen** : framework Microsoft pour agents multi-LLM
- **n8n** : automatisation no-code/low-code avec agents IA
- **CrewAI** : orchestration d'equipes d'agents IA
- **Claude Computer Use** : agent qui controle un ordinateur

---

## Defis et limites actuels

- Hallucinations et erreurs de raisonnement
- Gestion du contexte long
- Cout et latence des appels LLM
- Securite et contenu injecte (prompt injection)
- Evaluation de la performance

---

*Module cree: Juin 2026 | En cours d'enrichissement*
