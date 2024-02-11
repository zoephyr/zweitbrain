# Goal for Week of February 12, 2024

The project will need a VPS to test S3 functionality for "cold" storage, as well as moving back and forth from caches. 

We should implement an API on the VPS that can be accessed by a simple UI in Cloudflare Workers. This API will be for testing
  - We'll need to grab a Contabo VPS

We want to have an API on the VPS that can:
- Lookup a file and see if it is already stored, by comparing a SQL table of searches
  - This means we'll need PSQL or SQLite running locally
  - We'll need something like NGINX or HatTip to ensure the networking is open
- Save the file if it isn't, respond back with proper code if not
- REST API operations for the MinIO compatible API. We basically want to emulate UploadThing on a local server.
- After this, we can start to modify the API on a CFWP Hono side to communicate with this webserver

When we have these two servers able to communicate cache with each other, we'll have a pretty simple way to start communicating how to hit caches, and warm them entirely.

R2 will become "warm" storage, and the Server S3 (Z3) will be where data is backfilled.

Goal of Zweit project more clearly becomes that we should provide simple quickstarts and "meta" frameworks for deploying tools easily on Vercel and CF platforms


