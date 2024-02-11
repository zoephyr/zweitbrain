# Overview of services for Nelumbo Cloud

1. Web API on CFWP [`cf-open-cms`] or [`cf-nelumbo-server`](lol corn-fritters = CF)
   1. Hono
   2. SuperTokens or Lucia Auth
   3. CFWorkers packages - interface with pages, workers, etc
   4. REST based or GraphQL based (or both?)
   5. Proper tests with Vitest
2. ISR Manager on NextJS [`vercel-open-cms`] or [`vercel-nelumbo-cms-server`]
   1. Allows visual overview of data
   2. CRUD functions out to `cf-open-cms`
   3. Previews cached ISRs by revalidating tag
   4. POINT HERE: Workers must be able to have KV and R2 setup to cache properly
      1. Next ISR will have to validate the tag based on KV and sha
      2. A new file update will have a new SHA, KV will update that tag's entry SHA
      3. Thus, we can revalidate based on specific IDs and topics for posts!
   5. NOT JUST CONTENT viewed here, individual files and file types
   6. Must refer to R2 allowed filetypes - we may need another abstraction layer here.
   7. Must be able to talk out to [`vps-open-cms`/`vps-nelumbo-server`]
3. Sapphire Bot on VPS [`vps-nelumbo-bot`]
4. MinIO & S3 API layer on VP [`vps-nelumbo-server`]
   1. Possibly written as a simple Hono w/ Auth server 
      1. Could tilt to express if need be
      2. Possibly use Rust->WASM here if it benefits 