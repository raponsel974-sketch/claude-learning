# Module 05 - MCP : Model Context Protocol

## Definition

MCP (Model Context Protocol) est un standard open-source cree par Anthropic pour connecter les applications IA a des systemes externes.
Pense a MCP comme un "port USB-C pour les IA" : une interface universelle standardisee.

Source officielle: https://modelcontextprotocol.io
Spec: https://modelcontextprotocol.io/docs/learn/architecture

---

## Pourquoi MCP ?

### Avant MCP
Chaque integration IA necessitait une implementation sur mesure :
- IA <-> Google Drive : code custom
- IA <-> GitHub : code custom
- IA <-> Base de donnees : code custom
Resultat : fragmentation, duplication, maintenance complexe.

### Avec MCP
Un seul protocole standard :
- Developper un MCP Server = compatible avec tous les clients MCP
- Developper un MCP Client = acces a tous les serveurs MCP disponibles
Resultat : ecosysteme unifie, interoperabilite, reutilisation.

---

## Architecture MCP

### Les participants

#### MCP Host
L'application IA qui orchestre les connexions.
Exemples : Claude Desktop, Claude Code, VS Code, Cursor, ChatGPT

#### MCP Client
Composant cree par le Host pour chaque serveur. Maintient une connexion dediee.
Chaque serveur = 1 client dedie.

#### MCP Server
Programme qui expose des capacites (tools, resources, prompts) aux clients.
Peut tourner localement ou a distance.

```
MCP Host (Claude Desktop)
  |-- MCP Client 1 ---> MCP Server A (Filesystem local)
  |-- MCP Client 2 ---> MCP Server B (Database locale)
  |-- MCP Client 3 ---> MCP Server C (Sentry remote)
```

### Les couches

#### Data Layer
Protocole base sur JSON-RPC 2.0. Definit :
- Lifecycle management (initialisation, negociation)
- Les primitives (tools, resources, prompts)
- Sampling, Elicitation, Logging

#### Transport Layer
Mecanismes de communication :
- STDIO : stdin/stdout pour les serveurs locaux (performance maximale)
- Streamable HTTP : HTTP POST + Server-Sent Events pour les serveurs distants

---

## Les 3 Primitives Fondamentales

### 1. Tools (Outils)
Fonctions executables que le LLM peut invoquer pour agir dans le monde.
Controle : Model-controlled (le LLM decide quand les utiliser)

Exemples :
- searchFlights(origin, destination, date)
- createCalendarEvent(title, start, end)
- queryDatabase(sql)
- sendEmail(to, subject, body)
- executeCode(language, code)

Schema JSON pour definir un tool :
```
{
  name: "get_weather",
  description: "Get current weather for a location",
  inputSchema: {
    type: "object",
    properties: {
      location: { type: "string" }
    },
    required: ["location"]
  }
}
```

Flux d'execution :
1. Client envoie tools/list -> decouvre les outils disponibles
2. LLM decide d'utiliser un outil
3. Client envoie tools/call avec les arguments
4. Serveur execute et retourne le resultat

### 2. Resources (Ressources)
Sources de donnees en lecture seule que l'app peut recuperer pour contextualiser le LLM.
Controle : Application-controlled (l'app decide quand les inclure)

Chaque resource a un URI unique. Deux types :
- Direct Resources : URI fixes (ex: file:///path/to/doc.md)
- Resource Templates : URI dynamiques (ex: weather://forecast/{city}/{date})

Exemples :
- calendar://events/2024 (agenda)
- file:///Documents/rapport.pdf (fichier)
- db://schema/users (schema base de donnees)
- trips://history/paris-2023 (historique)

### 3. Prompts (Templates)
Templates reutilisables qui guident le LLM dans des workflows specifiques.
Controle : User-controlled (l'utilisateur choisit explicitement)

Exemples :
- /plan-vacation (destination, budget, duree, interets)
- /summarize-meeting (fichier audio/texte)
- /code-review (repository, langage)
- /draft-email (context, tone, recipient)

---

## Lifecycle MCP

1. Initialisation : Client envoie initialize avec sa version et ses capabilities
2. Negociation : Serveur repond avec ses capabilities (tools, resources, prompts)
3. Ready : Client envoie notifications/initialized
4. Usage : Echanges de requetes/reponses JSON-RPC
5. Notifications : Serveur informe le client des changements (ex: nouveaux tools)

---

## Ecosysteme MCP

### Clients MCP existants
- Claude Desktop / Claude Code (Anthropic)
- VS Code (GitHub Copilot)
- Cursor
- ChatGPT (OpenAI)
- Continue (IDE plugin)

### Serveurs MCP officiels (reference)
- Filesystem : acces aux fichiers locaux
- GitHub : gestion de repositories
- Google Drive : acces aux documents
- Slack : communication equipe
- PostgreSQL : requetes SQL
- Brave Search : recherche web
- Puppeteer : automatisation navigateur
- Sentry : monitoring erreurs
- Notion : gestion de contenu

### SDKs disponibles
- Python SDK : https://github.com/modelcontextprotocol/python-sdk
- TypeScript SDK : https://github.com/modelcontextprotocol/typescript-sdk
- Java SDK
- C# SDK
- Kotlin SDK

---

## MCP vs Tool Calling classique

| Critere | Tool Calling classique | MCP |
|---------|----------------------|-----|
| Standardisation | Non (specifique a chaque LLM) | Oui (protocole universel) |
| Reutilisabilite | Faible | Haute |
| Ecosysteme | Fragmente | Unifie |
| Transport | Direct | STDIO / HTTP |
| Persistance | Non | Oui (stateful) |
| Multi-client | Non | Oui |

---

## Securite MCP

- Les serveurs DOIVENT valider tous les inputs
- Un humain doit TOUJOURS pouvoir approuver/refuser les tool executions
- Les clients DOIVENT afficher clairement quels outils sont utilises
- Eviter la prompt injection via les outputs de serveurs
- Rate limiting sur les appels d'outils

---

Sources:
- https://modelcontextprotocol.io/introduction
- https://modelcontextprotocol.io/docs/learn/architecture
- https://modelcontextprotocol.io/docs/learn/server-concepts

*Module cree: Juin 2026 | Specialisation MCP*
