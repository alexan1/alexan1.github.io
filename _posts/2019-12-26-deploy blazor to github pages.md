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

Also you need [to add custom domain name](https://alexsolution.com/domain-name/), it won't work without it.

Okay, I did this and it's working. But it includes several steps to perform when you need to update website.

This is easy way to automate this using [GitHub Actions](https://github.com/features/actions).

And for this we have [GitHub Pages Deploy Action](https://github.com/marketplace/actions/deploy-to-github-pages) on Marketplace.

To create Action you need create <i>.yml</i> file in your repo in folder <i>/.github/workflows/</i>.

As template I used the [following example](https://github.com/fernandreu/blazor-pages/blob/master/.github/workflows/gh-pages.yml).

And this is my <i>main.yml</i>:

```
name: Build and Deploy
on: [push]
jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v1
    - name: Setup .NET Core
      uses: actions/setup-dotnet@v1
      with:
        dotnet-version: 3.1.100
    - name: Publish with dotnet
      run: dotnet publish --configuration Release --output build
    - name: Deploy to Github Pages
      uses: JamesIves/github-pages-deploy-action@releases/v3
      with:
        ACCESS_TOKEN: ${{ secrets.ACCESS_TOKEN }}
        BASE_BRANCH: master
        BRANCH: gh-pages # The branch the action should deploy to.
        FOLDER: build/BlazorGame/dist # The folder the action should deploy.
        CLEAN: true
```
        
How it works: your .NET Core project compiles, creates new branch and the deploy dist folder to this branch.

You just need to add two files <i>404.html</i> and <i>.nojekyll</i> and setup GitHub Pages options.
