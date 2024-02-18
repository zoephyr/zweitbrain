# A Response to Workers Platform DX issues

With a fresher perspective on the capabilities of the Cloudflare Workers platform, it's more evident that the developer tooling experience is at a "power-user" level that is stacked onto "developer" territory - essentially that is to say, Cloudflare Workers is something you are probably going to spend some time sink into and develop for at a professional level, rather than Vercel deploy and forget.

This is not bad, but does raise a question of "how should one use CF workers in their app?"

Workers are just that: Workers. They're not a replacement for "true serverless" as I'd put it, as some Lambdas become big and bulky enough on AWS or other FaaS providers that even they have issues

A worker is akin to a very light web-service worker - it's job may not function as well as "I'm using it as the full application layer", but in the sense that something like Vercel does - layer workers as a CDN layer over the underlying functions provided by certain serverless secret sauce.

If we refer to the [Vercel secret sauce](https://vercel.com/blog/behind-the-scenes-of-vercels-infrastructure), we can see there is some kind of architecture decision based around "Vercel CDN", but this is not specifically called out as "Cloudflare" (although we essentially know that it is a mixture of AWS CloudFront and Cloudflare DNS. Weird secret sauce, maybe? Who knows)

We also know that the Vercel Edge Middleware and functions are specifically outside the realm of AWS entirely [thanks to this chart](https://vercel.com/_next/image?url=https%3A%2F%2Fimages.ctfassets.net%2Fe5382hct74si%2F17wRK6w0tIbXhcKwHilCxR%2Fd082e25874a13d1787f2a4dd6c83295b%2FGroup_513640.png&w=1920&q=75&dpl=dpl_7KGZHvMXaQ7YvD1LYErmy4BVNMrF). It seems CF Workers are only used in an "outside Amazon request handling" manner - just as a speed boost thanks to "edge" runtime. Architecting an app off Vercel's platform in an a similar manner, to get the performance boosts that Workers can give, must be done by a careful decision to use the Workers by name alone - data in, data out, and routing functions - no crazy hijinks with the D1 and KV offerings as this architecture is probably already taken care of with a k8s redis and SQLish setup - not much else needs to happen here.