# Module 06 - Workflows IA

## Definition

Un workflow IA est une sequence d'etapes automatisees impliquant un ou plusieurs modeles IA, des outils, et des donnees, pour accomplir une tache complexe de bout en bout.

Difference cle :
- Workflow simple : sequence lineaire predeterminee
- Workflow agentique : sequence dynamique ou le LLM decide des etapes

---

## Types de Workflows

### 1. Workflow Lineaire (Pipeline)
Chaque etape passe son output a l'etape suivante.
```
Input -> Etape 1 -> Etape 2 -> Etape 3 -> Output
```
Ideal pour : traitement de documents, transformation de donnees, batch processing.

### 2. Workflow Conditionnel (Branching)
Le flux change en fonction de conditions.
```
       +--> Branche A (si condition X)
Input -|
       +--> Branche B (si condition Y)
```
Ideal pour : routing, triage, qualification de leads.

### 3. Workflow Parallele
Plusieurs etapes executees simultanement.
```
       +--> Tache A --+
Input -+--> Tache B --+--> Agregation -> Output
       +--> Tache C --+
```
Ideal pour : recherche multi-sources, analyse comparative.

### 4. Workflow Agentique (Agentic Loop)
Boucle dynamique ou l'agent planifie ses propres etapes.
```
Objectif -> [Planifier -> Agir -> Observer -> Corriger] -> Resultat
```
Ideal pour : taches complexes, recherche autonome, code generation.

### 5. Workflow Multi-Agent
Plusieurs agents specialises collaborent.
```
Superviseur -> delegue a Agent 1 (specialiste)
            -> delegue a Agent 2 (specialiste)
            -> agregation -> resultat final
```

---

## Patterns de Workflows Courants

### RAG (Retrieval-Augmented Generation)
```
Question utilisateur
  -> Embedding de la question
  -> Recherche dans Vector DB (trouver les docs pertinents)
  -> Injection des docs dans le contexte
  -> Generation de reponse par LLM
  -> Reponse enrichie
```

### ReAct (Reason + Act)
```
Objectif
  -> LLM Reflechit (Thought)
  -> LLM choisit une Action (outil a utiliser)
  -> Execution de l'outil
  -> Observation du resultat
  -> [Boucle] Retour au Thought si l'objectif n'est pas atteint
  -> Reponse finale
```

### Map-Reduce pour LLMs
```
Document long
  -> Decoupage en chunks (Map)
  -> Traitement parallele de chaque chunk par LLM
  -> Agregation des resultats (Reduce)
  -> Synthese finale
```
Ideal pour : resume de longs documents, analyse de corpus.

### Chain of Verification
```
Question -> Reponse initiale -> Generation de questions de verification
         -> Reponse aux questions de verification
         -> Verification de la coherence
         -> Reponse finale corrigee
```

---

## Outils de Workflow IA

### n8n (No-Code / Low-Code)
- Interface visuelle drag & drop
- +400 integrations natives
- Self-hostable (open-source)
- Noeuds Claude/OpenAI integres
- Ideal pour : automatisation d'entreprise, integrations API
- URL: https://n8n.io

### LangGraph
- Extension de LangChain pour workflows complexes
- Modelisation en graphe d'etats
- Persistance d'etat entre les etapes
- Ideal pour : agents avec cycles, workflows conditionnels
- URL: https://langchain-ai.github.io/langgraph/

### LangChain
- Framework Python/JS pour chains et agents
- Abstraction des LLMs, tools, memory
- Grand ecosysteme de composants
- URL: https://python.langchain.com

### Make (ex-Integromat)
- Alternative n8n, focus sur integrations
- Interface visuelle
- SaaS (pas self-hostable gratuit)

### Zapier
- Plateforme d'automatisation grand public
- Zaps = workflows declencheurs -> actions
- Integrations IA natives

### CrewAI
- Orchestration d'equipes d'agents IA
- Definition de roles, objectifs, outils par agent
- Communication inter-agents
- URL: https://docs.crewai.com

### Prefect / Airflow
- Orchestrateurs de workflows de donnees
- Scheduling, monitoring, retry logic
- Integrations IA possibles

---

## MCP dans les Workflows

MCP joue un role central dans les workflows agentiques modernes.

### Pattern Workflow + MCP
```
Workflow Engine (n8n / LangGraph)
  |
  +--> Noeud Agent LLM (Claude)
         |
         +--> MCP Client -> MCP Server (Filesystem)
         +--> MCP Client -> MCP Server (Database)
         +--> MCP Client -> MCP Server (GitHub)
         +--> MCP Client -> MCP Server (Slack)
```

Avantages :
- Les outils MCP sont standardises et reutilisables
- Un workflow peut appeler N outils via MCP sans custom code
- Separation claire entre la logique workflow et les integrations

### Exemple : Workflow d'analyse de code avec MCP
```
1. Trigger : nouveau commit GitHub
2. Agent Claude via MCP GitHub Server -> recupere le diff
3. Agent Claude analyse le diff -> identifie les problemes
4. Agent Claude via MCP Sentry -> verifie les erreurs recentes liees
5. Agent Claude via MCP Slack -> poste un rapport dans le channel dev
6. Si erreur critique : MCP GitHub -> ouvre une issue automatiquement
```

---

## Bonnes Pratiques Workflows IA

### Conception
- Toujours commencer simple (lineaire) avant d'ajouter de la complexite
- Definir clairement les criteres d'arret pour les boucles agentiques
- Prevoir des fallbacks en cas d'echec d'un outil
- Humain dans la boucle pour les actions irreversibles

### Performance
- Paralleliser quand les etapes sont independantes
- Cacher les resultats intermediaires couteux
- Chunker les documents longs avant traitement
- Monitorer les couts LLM (tokens)

### Fiabilite
- Implementer des retries avec backoff exponentiel
- Logger chaque etape pour le debugging
- Valider les inputs/outputs entre les etapes
- Tests unitaires sur chaque noeud du workflow

### Securite
- Ne jamais passer de secrets en clair dans les prompts
- Valider les outputs avant de les utiliser comme inputs
- Limiter les permissions des outils au strict necessaire
- Audit trail complet des actions executees

---

## Metriques de Workflow

- Latence totale (temps d'execution end-to-end)
- Cout en tokens LLM
- Taux de succes / echec
- Nombre d'iterations de la boucle agentique
- Cout par execution

---

*Module cree: Juin 2026 | Focus MCP + Workflows*
