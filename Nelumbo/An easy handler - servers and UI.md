# Introduction 

Remix could be an easy handler to setup for this type of thing. Remix on Cloudflare pages works well, possibly even with Hono injected - where it will shine is using it with Tanstack to create an easy system for managing file feeds. Here, we will begin looking at what it will tack to get Remix running as a thin layer over the CFW platform. In the advice of cloudflare, I'm working based on their open-source plan: https://blog.cloudflare.com/production-saas-intro


# Phase 1: JSON API

A good first phase is to build up a representation of the API handler at the JSON level, this could also be a good goal to close and capture a "contract" for how the API will operate. Using a light typescript schema of the D1 database, and associated KV values that may be loaded for certain content collections - we could possibly have very structured data broken down for delivery quite quickly - how we choose to do it is a good question though...

Using Hono is a good idea for speed, efficiency, etc, but may introduce some coupling layer concerns in the Remix handler. Hono as an API itself could be a great idea, but at this point if I'm using another web server to eject from Remix, what if I just wrote the server in something even more performant?

A potential solution I'd love to look at is to get https://github.com/gofiber/fiber running on workers. With Fiber, the requests could asynchronously be handled out to R2 and KV to obtain the records at an ultra fast rate.  This would lead to the JSON API being decoupled entirely from Remix, and is a direction I'd love to take. Having an ultra-fast web server would limit our benches to the CF platform itself.

# Phase 2: Dashboard UI

This is where remix would come in as a great solution. Getting a very lightweight handler on top of CF, and eventually on top of Vite as well, and Hono as a possible interop middle layer.

In essence though, this is where the  "manager" would come in - Remix would act as an actions/loaders handler for the different UI actions that need to come in. Problem we *might* face here is that we may want way more flexibility in what controls our UI. 

Now, before addressing the next stages (Article Edge-Rendering, and Feature Upgrades), we should ask what DIRECTION we want this to go in

Perhaps there's a new idea:

# **Golang & GoFiber-based JSON API**

This would mean that the server is written "server-less" as a file server from the ground up. We'd want the Fiber fileserver to do some simple operations on `Cloudflare`, and work as the *backbone* of the CMS that is *decoupled* from any UI implementation

This would allow a project as the UI to be hosted in ANY rendering consideration, and keeps our services "light" or "scoped". Using this Fiber implementation would allow the Worker to access everything without UI restrictions. What we might lose is TYPESAFETY, meaning we need to enforce a good way to "guarantee" our typesafety. One good bet is to possible use a `graphql` server on the go side, and have our UI hit `graphql` out to the API to request what files and what data it wants.

Overall, we need to experiment with these webserver solutions and see what typesafety looks like in a UI like NextJS or SolidStart, and what the DX is like when writing the `manager` application. Given this, I propose a restructuring to incorporate a `Go-API` layer and `UI-Manager` level, so that there is further separation, and a significant performance benefit by using a static based webserver.

Some advantages here are that 
1. Go is lightweight on memory and overhead, and favored among the light-VM/serverless crowd
2. Go is really damn fast, and will be an amazing web-worker base
3. The API will be abstracted for anyone to use, and could possibly be a worker PACKAGE that is imported from a typescript binding
   1. This would provide a way to import the CMS for anyone to automatically setup in their workers environment
   2. This may streamline the process used in Microfeed, which is the inspiration for this project
   3. A TypeScript binding would allow fine-grained control over the architecting or "terraform" of this project, by providing a simple way to write a script that executes your environment params to bind keys and secrets in CFPages easily! (SST-Ion anyone?)
4. Changes to the API can be non-reliant on any UI changes and versioning, which will be 100% decoupled
5. Further, the decoupling means anyone can use this "light-CMS" API on the CF platform, then host the manager UI anywhere else they wish
   1. But, the preferred way will be with a UI that is hosted on CF. Perhaps then...
   2. We could tilt to trying Solid for the UI management side of things?
6. Consumers can be in any hosting solution - as long as they can hit the API back and forth with auth, they'll get their data properly

This should be a pretty clean setup, if I'm correct.
