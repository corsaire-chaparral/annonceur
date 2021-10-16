# Annonceur

Petit logiciel pour l’annonceur.

Fait avec [Svelte](https://svelte.dev).


## Participants

Créer le fichier JSON des participants (cela peut être fait à partir d’un export CSV avec les colonnes `id`, `prenom`, `nom`, `equipe`, `sigle_equipe`).

```json
[
  {
    "id": 1,
    "prenom": "Johnny",
    "nom": "Dowey",
    "Sexe": "M",
    "equipe": "Champs",
    "sigle_equipe": "CHM"
  },
  {
    // ...
  }
]
```

## Démarrer

```bash
git clone https://github.com/corsaire-chaparral/annonceur
cd annonceur
```

*Vous devez avoir [Node.js](https://nodejs.org) installé.*

Installez les dépendences...

```bash
npm install
```

...puis démarrez [Rollup](https://rollupjs.org):

```bash
npm run dev
```

Naviguez à [localhost:5000](http://localhost:5000). Vous devriez voir l’app en cours. Les changements seront reflétés automatiquement.

By default, the server will only respond to requests from localhost. To allow connections from other computers, edit the `sirv` commands in package.json to include the option `--host 0.0.0.0`.

## Construire l’app en prod

Pour créer une version optimisée de l’app:

```bash
npm run build
```

Vous pouvez rouler l’app avec `npm run start` grâce à [sirv](https://github.com/lukeed/sirv), qui est déjà inclus dans les dépendences de votre package.json pour que l’app fonctionne lorsqu’elle est déployée sur des plateformes comme [Heroku](https://heroku.com).


## Single-page app mode

By default, sirv will only respond to requests that match files in `public`. This is to maximise compatibility with static fileservers, allowing you to deploy your app anywhere.

If you're building a single-page app (SPA) with multiple routes, sirv needs to be able to respond to requests for *any* path. You can make it so by editing the `"start"` command in package.json:

```js
"start": "sirv public --single"
```

## Deploying to the web

### With [Vercel](https://vercel.com)

Install `vercel` if you haven't already:

```bash
npm install -g vercel
```

Then, from within your project folder:

```bash
cd public
vercel deploy --name my-project
```

### With [surge](https://surge.sh/)

Install `surge` if you haven't already:

```bash
npm install -g surge
```

Then, from within your project folder:

```bash
npm run build
surge public my-project.surge.sh
```
