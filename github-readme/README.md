<div align="center">

<img src="docs/banner.png" alt="MS Solar — Mainframe de tes bots Discord" width="100%">

<br>

![version](https://img.shields.io/badge/version-1.3-E84246?style=for-the-badge&labelColor=090B0F)
![node](https://img.shields.io/badge/node-%E2%89%A518-5EF0F6?style=for-the-badge&labelColor=090B0F)
![windows](https://img.shields.io/badge/Windows-pr%C3%A9vu%20pour-F4D646?style=for-the-badge&labelColor=090B0F)
![licence](https://img.shields.io/badge/usage-non%20commercial-928C9A?style=for-the-badge&labelColor=090B0F)

**Héberge, surveille et répare tous tes bots Discord depuis un seul panel, sans MCSManager.**<br>
*Stay sharp, edgerunner.*

</div>

---

## Capri veille sur tes bots

<table align="center"><tr>
<td align="center"><img src="docs/idle.webp" height="190" alt="Capri idle"><br><b>Tout va bien</b><br><sub>au moins un bot en ligne</sub></td>
<td align="center"><img src="docs/glitch.webp" height="190" alt="Capri glitch"><br><b>Alerte</b><br><sub>un bot vient de planter</sub></td>
<td align="center"><img src="docs/sleep.webp" height="190" alt="Capri sommeil"><br><b>Sommeil</b><br><sub>aucun bot en ligne</sub></td>
</tr></table>

Elle change d'état en direct selon tes bots, et dans l'onglet **Capri** tu peux aussi **discuter avec elle** : de tes bots, de tes projets, de tout et de rien.

## Aperçu

<p align="center"><img src="docs/dashboard.png" alt="Tableau de bord" width="92%"></p>
<p align="center"><img src="docs/ide.png" alt="Éditeur de code avec Capri" width="92%"></p>
<p align="center"><img src="docs/bot.png" alt="Page d'un bot : console, fichiers, tâches" width="46%"> <img src="docs/capri.png" alt="Discussion avec Capri" width="46%"></p>

## Fonctionnalités

| | |
|---|---|
| **Contrôle** | Démarrer, arrêter, redémarrer, actions groupées, redémarrage automatique après crash (coupé si le bot plante en boucle) |
| **Console en direct** | Logs en temps réel (WebSocket), filtre, envoi de commandes au bot, historique sur disque |
| **Catégories** | 10 catégories détectées automatiquement (Sécurité, Modération, Gestion, Tickets, Musique, Économie et jeux, Logs, IA, Utilitaires, Communauté), modifiables, repliables, actions par catégorie |
| **Monitoring** | CPU et mémoire par bot et au total, graphiques, uptime, journal d'activité |
| **Ajout de bot** | Dépose un zip : langage, commande, dépendances détectés, scan des tokens en clair et du code suspect |
| **Import MCSManager** | Reprend tes instances existantes en un clic |
| **Diagnostic** | JSON invalides (avec ligne et colonne), dépendances manquantes, tokens en clair, intents, binaires natifs |
| **Éditeur de code** | Façon VS Code dans le navigateur : explorateur, onglets, coloration, numéros de lignes, indentation auto, `Ctrl+S` |
| **Capri modifie le code** | Elle propose, tu vois le **diff**, tu valides, tu peux **annuler**. Jamais de modification sans ton accord, jamais de `.env` ni de token |
| **Modèles de bots** | Base, Utilitaires, Bienvenue, Modération : un bot discord.js prêt à lancer en un clic |
| **Fichiers** | Explorateur, téléchargement, création et suppression |
| **Sauvegardes** | Manuelles et automatiques, restauration avec copie de sécurité |
| **Mise à jour d'un bot** | Nouveau zip, en gardant `.env`, `config.json`, `db/` et les bases SQLite |
| **Tâches planifiées** | Redémarrage, arrêt, démarrage ou sauvegarde à heure fixe |
| **Infos Discord** | Ping, serveurs et membres de chaque bot |
| **Alertes** | Webhook Discord et message privé quand un bot plante en boucle |
| **Capri** | Amie et assistante : analyse tes bots, propose des correctifs, retient ce qu'elle apprend |
| **Animations** | Transitions de pages, cartes qui apparaissent en cascade, compteurs qui s'illuminent, statuts qui pulsent, fond néon animé (désactivées si ton système réduit les animations) |
| **Confort** | Palette de commandes `Ctrl+K`, recherche, animation de démarrage |
| **Comptes** | Owner et admins, changement de mot de passe, sessions révocables |

## Installation (Windows)

1. Installe [Node.js 18 ou plus](https://nodejs.org).
2. Décompresse le projet, puis double-clique sur **`start.bat`** (il installe les dépendances au premier lancement).
3. Ouvre **http://127.0.0.1:3000** et connecte-toi.

Premier lancement : le compte `sixn` est créé avec un mot de passe par défaut (affiché dans la console). **Change-le tout de suite** avec le bouton « Mot de passe ». Pour choisir le tien dès le départ : `PANEL_OWNER_USER` et `PANEL_OWNER_PASSWORD`, ou `node set-login.js <nom> <mot_de_passe>`. Pour l'ouvrir à tes admins sur le réseau local, définis `HOST=0.0.0.0` avant de lancer (voir « Sécurité »).

## Capri : donner un cerveau à ton amie

Onglet **Capri > Réglages du cerveau** (réservé au owner) :

- **Ollama** (local) : tout reste sur ton PC. URL `http://127.0.0.1:11434/v1`, nom du modèle, pas de clé.
- **Claude** (clé API Anthropic) ou toute API compatible OpenAI (NVIDIA, OpenAI…) : tes messages et l'état de tes bots (tokens masqués) partent vers ce service.

Dans l'éditeur, Capri voit le fichier ouvert et peut proposer des modifications : tu vérifies le diff, tu cliques sur **Appliquer**, et tu peux **Annuler**. Elle ne modifie jamais rien toute seule, et ne touche ni au `.env` ni aux tokens (ils sont masqués avant tout envoi). Ses notes se trouvent dans `data/capri-notes.json`.

## Sécurité

- Ne publie **jamais** `data/`, `bots/` ni un `.env` : le `.gitignore` fourni les exclut.
- Le panel écoute sur ton PC uniquement par défaut et n'a pas de HTTPS. Pour des admins distants, passe par un VPN (Tailscale…), n'expose pas le port sur Internet.
- Cookies `HttpOnly` + `SameSite=Strict`, requêtes protégées contre le CSRF, blocage après 5 échecs de connexion, tokens masqués dans les logs, écritures de fichiers atomiques.
- Si un token a été partagé ou publié, **régénère-le** dans le portail développeur Discord.

## Structure

```
server.js        serveur, gestionnaire de processus, API, WebSocket
capri.js         cerveau et mémoire de Capri
templates.js     modèles de bots
public/          interface (index.html) + assets Capri (polices, animations)
test/run.js      tests d'intégration  ->  npm test
set-login.js     définir le compte principal
docs/            visuels du README
```

## Tests

```
npm install
npm test
```

## Feuille de route

- [ ] Alertes par email
- [ ] Commande `/capri chat` dans les bots Discord
- [ ] Capri vocale sur le PC (via [Capri Desktop](https://github.com/lachydotmcg/capri-desktop))
- [ ] Interface en français et en anglais

## Crédits et licence

Le style (palette, polices, animations, art de **Capri**) vient du projet [capri-desktop](https://github.com/lachydotmcg/capri-desktop) de lachydotmcg, sous licence [PolyForm Noncommercial 1.0.0](https://polyformproject.org/licenses/noncommercial/1.0.0). Les mentions obligatoires sont dans [`NOTICE.md`](NOTICE.md). Tant que le projet embarque ces visuels, **l'usage reste non commercial** : ne le vends pas et ne l'intègre pas à un service payant.

Polices : Barlow et Share Tech Mono (SIL OFL 1.1).

<div align="center"><sub>Fait avec du néon et trop de café · v1.3</sub></div>
