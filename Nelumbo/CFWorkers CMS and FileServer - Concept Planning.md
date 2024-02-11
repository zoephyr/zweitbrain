
# This is a concept for a CMS backed entirely by the Cloudflare Worker's Platform (CFWP)
Included products will be:
- R2 (S3 Compatible API on Cloudflare Cache)
- KV (Key-value store, config vars, rate-limiting)
- D1 (Serverless SQL platform)
Target products include
- Queues, for processing multiple file entries
- Vectorize, to create embeddings of .MDX content files that get piped into an LLM


## Concept: Hono-based CMS for CFWP
Using `Hono`, one is able to achieve a fast "request" based API that will leverage the underlying workers calls for D1, KV, and R2. Now, Hono was selected for 2 things:
- The ability to run quick, and build quick, on the `'workerd'` container environment
- The ability to run as part of the request handler stack in something like Solid, or Remix, preferably with `Tanstack (Query)` for quickly building API actions and loaders. 

As well we can look into 
- possible `Zustand` for any SPA-like state management, otherwise stick to URL params as needed.
- using external consumers, like on Vercel/Netlify
	- using ISR to automatically revalidate tags to the R2/KV buckets that hold these data
  
Theoretically, there isn't much need for much else. The goal of this project is

## Concept: Discord Bot that manages and reads CMS

This CMS system is to be integrated with Discord auth. Essentially, the "community" layer is to allow certain users authentication/authorization for elevated permissions. Using packages such as
- `SuperTokens`, or
- `LuciaAuth` for React
Can allow for an easy way to integrate this authentication

**EXPLORATION QUESTION:** Is it possible to create a role for a user in a Discord server, and read that as a permission set? Perhaps we need a button that "reimports" or "revalidates" a users permissions, and aligns them with the same content that they have access to in the server

## Concept: Open up project ideas to be part of a larger feature set

If this CMS is built as an extensible API in TypeScript on the CFWP, then any consumer can possible interact with this API as a way to create multiple data sources. We could potentially move this app to be mildly multi-tenanted, as an easy way to host multiple inter-related sites based on the same concepts of access, authoring, and data-governance

# Project codename: Nelumbo

The project name comes from the genus for the Lotus flower.

A few main project names come out of this

- `Nucifera` for the server-side bot, possibly written using `SapphireJS`.
- `Lutae` for the CMS on R2, KV, D1, all on CFWP.
- `teatime` for the S3 compatible API management on VPS along side `Nucifera`, more of a configuration manager that keeps all systems running and update content together (probably interfacing to `MinIO` for S3 actions on a VPS filesystem)



