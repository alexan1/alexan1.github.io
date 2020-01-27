---
layout: post
title: publish nuget package
hidden: true
---
I developed library for my project. Then I thought: why don't publish it on?

It's very simple actually. Just followed [this tutorial](https://docs.microsoft.com/en-us/nuget/nuget-org/publish-a-package): packed project from visual studio and upload to [nuget.org](https://www.nuget.org/packages/WikiDataiLib/).

Okay, I did ir manually, but I want to automate process of updating library version.

For this you can use or [Azure Pipelines](https://medium.com/@yanxiaodi/using-azure-devops-pipelines-to-publish-the-nuget-package-from-github-repo-fb58be4e9be8) or [GitHub Actions](https://brainlesscoder.com/2019/12/25/publishing-net-standard-nuget-package-with-github-actions/).

I decided to go with GitHub Actions using this [Publish NuGet Action](https://github.com/rohith/publish-nuget).

So, I increased library minor version and published it.

But instead just updating version other package was published and now I have 2 packages with version 1.0.0 and 1.0.2.

And you can't just delete package from Nuget Gallery, you can only unkist it and unlisted version 1.0.0.

Just to check how versioning works, I increased version again to 1.0.3 and published again.

And now I have [package](https://www.nuget.org/packages/WikiDataLib/) (two versions).
