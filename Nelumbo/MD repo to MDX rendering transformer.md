A possible approach I just had is to take .MD files and split them into CF KV entries. We could take these MD files and insert them into an .MDX re-parser, where we insert them into components that can load and transform rendered HTML. Instead of making CSS classes, we actually are changing the entire rendering structure by making "blocks" that can interpret the .MD parsed, and insert into large sections of .MDX as reparsed `React` components. 

In essence, anyone can get the experience of writing MD files, and autogenerating .MDX rendered into React components. These can then be returned as JSON, or sent to a rendering in RSCs format such as NextJS on Vercel. 

The main benefit I am looking to obtain is to have a repository be agnostic in just .MD file. Then, if someone wishes to render in MDX - they can use React, Preact, or Vue from the provided packages. For something like Solid which uses a slightly different flexible rendering method, the .MD files can be provided for a Solid parser to convert them using something like https://github.com/high1/solid-jsx

## Essentially: my goal is to use .MD files to, on the fly, create any templated "rendering" method

One challenge is how to "parse" an MD file to be properly read by the .MDX file format. 
- What challenges does this pose? How do we "split" the file into many "blocks"?
- Is it just easier to write in .MDX and tell authors to use `Obsidian` or `VSCode` with these features enabled?

A sacrifice will have to be made somewhere, and perhaps a compromise can be made to inject .MDX for MD files, while also reading MDX files "as is".