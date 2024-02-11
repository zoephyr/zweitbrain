# Testing: Can Next on Vercel rebuild off of changes to Cloudflare R2 and KV?

What we'll need to do is build a testing harness that allows a separate Vercel build of NextJS to ISR on some R2 and KV values in Cloudflare

## It may benefit us to make two testing projects:
- A Remix project that has a UI with loaders and actions to quickly change some stuff
  - This project will upload and CRUD on some R2 bucket with a .MD file in KV/D1 entries
- A Next project that has a manual revalidateTag action that can refresh the cache for this file

## Now, we must figure out a few things:
- How to interface with R2, KV, and D1 in Remix
- How to, in app directory, create a static generation step that downloads the .MD file from CF
  - This will have the revalidate concept on it, where we expose a route that will revalidate the tag for this post/item/route.

## A few things will be handy here:
- A cloudflare workers remix template, that has D1, R2, KV bindings
  - Expose an API using remix as the handler, use that to serve the updated files
  - R2 uploader and D1 handler for versioning an entry of a file (with SHA hash)
  - A harness for the API to lookup in D1 the post by route or ID, grab the KV cache value of updated R2 sha 
- A Next project template with ISR to lookup and revalidate 

## BONUS stretch:
- Get a GraphQL server running with Remix, so that GraphQL request can hit an endpoint, and make queries/mutations on the fileserver.



