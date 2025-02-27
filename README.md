![Obsidian](./assets/logoSilver.jpg)

<div align="center">GraphQL, built for Deno.</div>

<div align="center">

<h1 align="center">
	<a>Obsidian</a>
	<a href="https://twitter.com/intent/tweet?text=Meet%20Obsidian!%20Deno's%20first%20native%20GraphQL%20caching%20client%20and%20server%20module&url=http://obsidian.land/&via=obsidian_land&hashtags=deno,denoland,nodejs,graphql,javascript" rel="nofollow"><img src="https://camo.githubusercontent.com/83d4084f7b71558e33b08844da5c773a8657e271/68747470733a2f2f696d672e736869656c64732e696f2f747769747465722f75726c2f687474702f736869656c64732e696f2e7376673f7374796c653d736f6369616c" alt="Tweet" data-canonical-src="https://img.shields.io/twitter/url/http/shields.io.svg?style=social" style="max-width:100%;"></a>
</h1>

<p align="center">from <em align="center">Lascaux</em></p>

</div>

<p align="center">
  <img alt="GitHub" src="https://img.shields.io/github/license/open-source-labs/obsidian">
  <img alt="GitHub issues" src="https://img.shields.io/github/issues-raw/open-source-labs/obsidian?color=yellow">
  <img alt="GitHub last commit" src="https://img.shields.io/github/last-commit/open-source-labs/obsidian?color=orange">
  <img alt="GitHub Repo stars" src="https://img.shields.io/github/stars/open-source-labs/obsidian?style=social">  
</p>

## Features

- GraphQL query abstraction and caching in SSR React projects, improving the performance of your app
- Normalized caching, optimizing memory management to keep your site lightweight and fast
- Fullstack integration, leveraging client-side and server-side caching to streamline your caching strategy

## Overview

Obsidian is Deno's first native GraphQL caching client and server module. Boasting lightning-fast caching and fetching capabilities alongside headlining normalization and destructuring strategies, Obsidian is equipped to support scalable, highly performant applications.

Optimized for use in server-side rendered React apps built with Deno, full stack integration of Obsidian enables many of its most powerful features, including optimized caching exchanges between client and server and extremely lightweight client-side caching.

## Documentation and Demo

[obsidian.land](http://obsidian.land)

## Installation

<div align="center"><strong>QUICK START</strong></div>
<br>

In the server:

```javascript
import { ObsidianRouter } from 'https://deno.land/x/obsidian/mod.ts';
```

In the app:

```javascript
import { ObsidianWrapper } from 'https://deno.land/x/obsidian/clientMod.ts';
```

## Creating the Router

```javascript
import { Application, Router } from 'https://deno.land/x/oak/mod.ts';
import { ObsidianRouter, gql } from 'https://deno.land/x/obsidian/mod.ts';

const PORT = 8000;

const app = new Application();

const types = (gql as any)`
  // Type definitions
`;

const resolvers = {
  // Resolvers
}

interface ObsRouter extends Router {
  obsidianSchema?: any;
}

const GraphQLRouter = await ObsidianRouter<ObsRouter>({
  Router,
  typeDefs: types,
  resolvers: resolvers,
  redisPort: 6379,
});

const router = new Router();
router.get('/', handlePage);

function handlePage(ctx: any) {
  try {
    const body = (ReactDomServer as any).renderToString(<App />);
    ctx.response.body = `<!DOCTYPE html>
      <html lang="en">
      <head>
        <meta charset="UTF-8">
        <title>SSR React App</title>
      </head>
      <body>
        <div id="root">\${body}</div>
        <script src="/static/client.tsx" defer></script>
      </body>
      </html>`;
  } catch (error) {
    console.error(error);

app.use(GraphQLRouter.routes(), GraphQLRouter.allowedMethods());

await app.listen({ port: PORT });
```

## Creating the Wrapper

```javascript
import { ObsidianWrapper } from 'https://deno.land/x/obsidian/clientMod.ts';

const App = () => {
  return (
    <ObsidianWrapper>
      <MovieApp />
    </ObsidianWrapper>
  );
};
```

## Making a Query

```javascript
import { useObsidian, BrowserCache } from 'https://deno.land/x/obsidian/clientMod.ts';

const MovieApp = () => {
  const { query, cache, setCache } = useObsidian();
  const [movies, setMovies] = (React as any).useState('');

  const queryStr = `query {
      movies {
        id
        title
        releaseYear
        genre
      }
    }
  `;

  return (
    <h1>{movies}</h1>
    <button
      onClick={() => {
        query(queryStr)
        .then(resp => setMovies(resp.data))
        .then(resp => setCache(new BrowserCache(cache.storage)))
      }}
    >Get Movies</button>
  );
};
```

## Making a Mutation

```javascript
import { useObsidian, BrowserCache } from 'https://deno.land/x/obsidian/clientMod.ts';

const MovieApp = () => {
  const { mutate, cache, setCache } = useObsidian();
  const [movies, setMovies] = (React as any).useState('');

  const queryStr = `mutation {
    addMovie(input: {title: "Cruel Intentions", releaseYear: 1999, genre: "DRAMA" }) {
      id
      title
      releaseYear
      genre
    }
  }
  `;

  return (
    <h1>{movies}</h1>
    <button
      onClick={() => {
        mutate(queryStr)
        .then(resp => setMovies(resp.data))
        .then(resp => setCache(new BrowserCache(cache.storage)))
      }}
    >Get Movies</button>
  );
}
```

## Documentation

[obsidian.land](http://obsidian.land)

## Authors

_Lascaux_ Engineers

[Alonso Garza](https://github.com/Alonsog66)  
[Burak Caliskan](https://github.com/CaliskanBurak)  
[Matt Meigs](https://github.com/mmeigs)  
[Travis Frank](https://github.com/TravisFrankMTG/)  
[Lourent Flores](https://github.com/lourentflores)  
[Esma Sahraoui](https://github.com/EsmaShr)  
[Derek Miller](https://github.com/dsymiller)  
[Eric Marcatoma](https://github.com/ericmarc159)  
[Spencer Stockton](https://github.com/tonstock)  
