# Lex Duana plugin

[English](#english) · [Français](#français)

## English

Lex Duana brings African customs law into your AI tool: national and community customs codes, common external tariffs, the Harmonized System and the WCO customs valuation instruments. This plugin bundles two things:

- a **connector** to the Lex Duana server (read-only `lex_*` tools);
- a **skill**: instructions that teach your assistant where to look, how to quote an article with its version, and how to answer in your language with few tool calls.

The texts are served as published in Lex Duana. The tools do not give legal advice, do not compute duties and do not decide a tariff classification.

### Install

Pick the form your AI tool accepts.

1. **Full plugin** (connector and skill), for tools that read the `.claude-plugin` format:

   ```
   claude plugin install lex-duana --marketplace Smart-DUANA/lex-duana-ai
   ```

2. **Skill only**, as an archive to upload or unzip into your tool's skills folder: [lex-duana-skill-1.1.0.zip](https://github.com/Smart-DUANA/lex-duana-ai/releases/download/v1.1.0/lex-duana-skill-1.1.0.zip). Then add the server address below as a connector.

3. **Server address only**, for tools that accept a remote MCP server but no skill:

   ```
   https://api.lexduana.com/mcp
   ```

### Sign in

The server requires a Lex Duana account; a free account is enough. On first use your AI tool opens a sign-in page in your browser. The daily limits depend on your plan and are shown in the Lex Duana app, under "Connected AI tools", where you can also disconnect a tool.

Step-by-step guides: <https://lexduana.com/en/outils-ia/> · [Privacy policy](https://lexduana.com/fr/confidentialite/) (in French)

### What is inside

| Path | Purpose |
|---|---|
| `.claude-plugin/plugin.json` | Plugin manifest |
| `.mcp.json` | Connector: server `lex-duana`, no key inside |
| `skills/lex-duana/SKILL.md` | The skill |
| `skills/lex-duana/references/` | Details loaded on demand: tools and fields, workflows, citation rules, errors and limits, glossary |
| `skills/lex-duana/agents/openai.yaml` | Skill metadata for tools that read this file |
| `assets/icon.svg` | Lex Duana icon |

### AI tools

No AI tool is listed here yet: a tool is named only once its connection to Lex Duana has been tried. Any tool that supports remote MCP servers with sign-in can use the server address.

### License

MIT, see [LICENSE](LICENSE). The license covers this plugin (connector settings and skill), not the legal texts served by Lex Duana. Source: <https://github.com/Smart-DUANA/lex-duana-ai>

## Français

Lex Duana met le droit douanier africain dans votre outil IA : codes des douanes nationaux et communautaires, tarifs extérieurs communs, Système harmonisé et instruments d'évaluation en douane de l'OMD. Ce plugin réunit deux choses :

- un **connecteur** vers le serveur Lex Duana (outils `lex_*`, en lecture seule) ;
- un **skill** : des consignes qui apprennent à votre assistant à chercher au bon endroit, à citer l'article et sa version, et à répondre dans votre langue en peu d'appels.

Les textes sont servis tels que publiés dans Lex Duana. Les outils ne donnent pas de conseil juridique, ne calculent pas de droits et ne décident pas d'un classement tarifaire.

### Installer

Choisissez la forme que votre outil IA accepte.

1. **Plugin complet** (connecteur et skill), pour les outils qui lisent le format `.claude-plugin` :

   ```
   claude plugin install lex-duana --marketplace Smart-DUANA/lex-duana-ai
   ```

2. **Skill seul**, en archive à téléverser ou à décompresser dans le dossier des skills de votre outil : [lex-duana-skill-1.1.0.zip](https://github.com/Smart-DUANA/lex-duana-ai/releases/download/v1.1.0/lex-duana-skill-1.1.0.zip). Ajoutez ensuite l'adresse du serveur ci-dessous comme connecteur.

3. **Adresse du serveur seule**, pour les outils qui acceptent un serveur MCP distant mais pas de skill :

   ```
   https://api.lexduana.com/mcp
   ```

### Se connecter

Le serveur exige un compte Lex Duana ; un compte gratuit suffit. Au premier usage, votre outil IA ouvre une page de connexion dans votre navigateur. Les limites quotidiennes dépendent de votre offre et s'affichent dans l'application Lex Duana, écran « Outils IA connectés », où vous pouvez aussi déconnecter un outil.

Guides pas à pas : <https://lexduana.com/fr/outils-ia/> · [Politique de confidentialité](https://lexduana.com/fr/confidentialite/)

### Contenu

| Chemin | Rôle |
|---|---|
| `.claude-plugin/plugin.json` | Manifeste du plugin |
| `.mcp.json` | Connecteur : serveur `lex-duana`, sans aucune clé |
| `skills/lex-duana/SKILL.md` | Le skill |
| `skills/lex-duana/references/` | Détails chargés à la demande : outils et champs, parcours, règles de citation, erreurs et limites, glossaire |
| `skills/lex-duana/agents/openai.yaml` | Métadonnées du skill pour les outils qui lisent ce fichier |
| `assets/icon.svg` | Icône Lex Duana |

### Outils IA

Aucun outil IA n'est encore cité ici : un outil n'est nommé qu'une fois sa connexion à Lex Duana essayée. Tout outil qui accepte un serveur MCP distant avec connexion par compte peut utiliser l'adresse du serveur.

### Licence

MIT, voir [LICENSE](LICENSE). La licence couvre ce plugin (réglages du connecteur et skill), pas les textes juridiques servis par Lex Duana. Source : <https://github.com/Smart-DUANA/lex-duana-ai>
