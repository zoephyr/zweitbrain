# Results found from the 02/11/2024

Right now, using the Cloudflare Workers environment for D1 and KV has proven to be a DX nightmare, of sorts

There just isn't a good way to natively setup and maintain everything, this is stuff other platforms have nearly all figured out

So, architecture is going to tilt to building out a community-focused content management system using agnostic solutions where possible.

Calling out some services in scope:
- SQLite, or
- PostgreSQL
- Redis
- SapphireJS on PM2 - Discord Bot
- MinIO S3 API storage
- NextJS API and Dashboard UI
- Grafana
- Elastic Alternative (OpenSearch)

These all should run where possible on a single VPS 
We should be able to make multiple services stack on a single 6cpux16GB machine.

This will be the basis for Zweit - second office, open source community management.

The Nelumbo CMS system will provide auth for multi-tenant applications that serve a widerange of discord users.
