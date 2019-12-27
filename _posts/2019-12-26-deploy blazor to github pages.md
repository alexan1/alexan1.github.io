---
layout: post
title: deploy blazor to github pages
---
There are two [hosting models for Blazor](https://docs.microsoft.com/en-us/aspnet/core/blazor/hosting-models?view=aspnetcore-3.1):
1. Blazor Server
2. Blazor WebAssembly

Latest is client side model, so it can be hosted as static website, for example in [Azure Storage](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-blob-static-website), [FireBase](https://firebase.google.com/) or [GitHub Pages](https://pages.github.com/).

It's easy with GitHub Pages and it's free.

If you need to deploy there you go to Settings -> GitHub Pages -> Source, but it doesn't work this way with Blazor. 

Although Blazor is client side application, it need to be compiled before deployment. 

So I opened project in VS, published to local folder, initialized git repo and published it on GitHub. And you need to add two files to repo: <i>404.html</i> file with a script that handles redirecting the request to the <i>index.html</i> page. You can take this file [here](https://github.com/blazor-demo/blazor-demo.github.io/blob/master/404.html). Also you need to add empty file <i>.nojekyll</i>.
