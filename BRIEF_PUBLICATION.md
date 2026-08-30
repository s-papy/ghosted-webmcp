# BRIEF — session terminal : publier et déployer Cash Pipeline (WebMCP Challenge)

*À coller dans une session terminal lancée depuis `~/Desktop/CERVEAU/cash-pipeline-webmcp/`. Nouveau projet, aucun brief précédent.*

---

## Contexte, honnêtement

Cowork (moi, dans une session séparée, bac à sable Linux) a écrit ce projet de zéro pour **The WebMCP Challenge** (devpost, deadline **3 septembre 2026, 13h PDT**) : une app 100% cliente (aucun backend, aucune dépendance) qui suit les opportunités de cash (bourses, hackathons, missions freelance) — modifiable à la main via une interface, ou par un agent via des outils WebMCP (`document.modelContext.registerTool`).

Fichiers déjà présents dans ce dossier :
- `index.html` — l'app entière (HTML+CSS+JS inline), localStorage comme seule persistance.
- `README.md` — pitch, tableau des 6 outils, instructions de lancement/déploiement.
- `LICENSE` — MIT.

Vérifié avant d'écrire ce brief (pas juste écrit, exécuté) :
- `node --check` sur le `<script>` extrait : syntaxe propre.
- Les 6 outils (`add_opportunity`, `update_status`, `remove_opportunity`, `get_deadlines`, `get_pipeline_summary`, `search_opportunities`) exécutés dans un harnais Node avec un faux `document.modelContext` et un faux `localStorage` : ajout, changement de statut, recherche, suppression, résumé — tout produit le résultat attendu (voir sortie dans la conversation Cowork si besoin de la revoir).

**Aucun dépôt git n'existe encore pour ce projet.** Ce dossier n'a jamais été un `git init` — c'est la première étape ci-dessous.

**Important, appris à la dure sur un autre projet aujourd'hui même** : Spap a un dossier `hindsight-alpha` séparé (un autre projet, pour un autre hackathon — Alpaca). Cowork avait par erreur commencé à modifier ce dossier-là avant de se faire recadrer et de tout annuler proprement (`git restore`). Ce brief ne concerne que **ce nouveau dossier `cash-pipeline-webmcp`** — ne touche à rien dans `hindsight-alpha`, ni à son dépôt git, ni à son remote GitHub.

## Ce qu'on te demande

1. **Initialiser le dépôt git local** dans ce dossier (`git init`, `git add -A`, premier commit).
2. **Créer un nouveau dépôt GitHub public** dédié à ce projet (nom suggéré : `cash-pipeline-webmcp`, ou ce que Spap préfère) — via `gh repo create` si le CLI GitHub est authentifié, sinon créer manuellement sur github.com puis ajouter le remote et pousser.
3. **Vérifier que la licence est bien détectée** : sur la page GitHub du dépôt, la section "About" doit afficher "MIT License" automatiquement (GitHub la détecte depuis le fichier `LICENSE` à la racine — pas d'action si le fichier est bien à la racine, juste à vérifier visuellement après le push).
4. **Déployer une URL live testable.** Le plus simple avec ce qui est probablement déjà en place sur ce Mac : activer **GitHub Pages** sur ce dépôt (Settings → Pages → Deploy from branch → `main` / racine). Sinon, si Vercel ou Netlify sont déjà authentifiés en CLI, un déploiement statique fonctionne aussi (`vercel --prod` ou `netlify deploy --prod`, sans configuration puisque c'est un simple fichier statique).
5. **Mettre à jour `README.md`** : remplacer les deux lignes `_add the deployed URL here..._` et `_add the YouTube link here_` — la première avec l'URL live obtenue à l'étape 4, la seconde reste en attente (la vidéo est prévue **mercredi**, pas encore tournée). Commit + push de cette mise à jour.
6. **Tester réellement l'URL live** : ouvrir la page dans Chrome avec `chrome://flags/#enable-webmcp-testing` activé (ou dans le navigateur intégré de ChatGPT si disponible), et confirmer que la page se charge sans erreur console. Un simple screenshot ou une confirmation en une ligne suffit — pas besoin de faire fonctionner un agent WebMCP complet à ce stade.

## Hors périmètre

- **Ne jamais toucher à `hindsight-alpha`** (fichiers, git, remote) — projet totalement séparé, déjà repris en main par Spap.
- **Ne pas soumettre le projet sur Devpost.** Créer le repo et déployer, oui ; remplir/soumettre le formulaire `webmcp.devpost.com` reste une action de Spap lui-même (cohérent avec le reste du sprint : lui seul valide et clique "submit" sur ces plateformes).
- **Ne pas inventer d'informations personnelles** (nom légal, etc.) si un formulaire quelconque en demande au passage — laisser `[À REMPLIR PAR SPAP]` le cas échéant.
- **Aucun `git push --force`**, sur ce dépôt ou un autre.
- Ne pas payer/activer un service tiers payant pour l'hébergement — GitHub Pages suffit et est gratuit.

## En fin de séance

Verdict net, pas d'entre-deux : soit "🟢 publié — voici l'URL du repo public et l'URL live", soit "🔴 bloqué sur X" avec la raison précise (ex. `gh` non authentifié, Pages qui ne se déploie pas). Pas besoin de fichier de suivi séparé pour un projet de cette taille — rapporte directement le résultat à Spap dans le chat/terminal.

---

**Le dépôt doit être public et sa licence visible dans le "About" — ce n'est pas une convention maison, c'est une exigence du règlement du WebMCP Challenge lui-même. Sans ça, la soumission Devpost n'est pas valide.**
