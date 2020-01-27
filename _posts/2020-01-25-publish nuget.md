---
layout: post
title: publish nuget package
hidden: true
---
I developed library for my project. Then I thought: why don't publish it?

It's very simple actually. Just followed [this tutorial](https://docs.microsoft.com/en-us/nuget/nuget-org/publish-a-package): packed project from visual studio and uploaded it to [nuget.org](https://www.nuget.org/packages/WikiDataiLib/).

Okay, I did ir manually, but I want to automate this process.

For this you can use or [Azure Pipelines](https://medium.com/@yanxiaodi/using-azure-devops-pipelines-to-publish-the-nuget-package-from-github-repo-fb58be4e9be8) or [GitHub Actions](https://brainlesscoder.com/2019/12/25/publishing-net-standard-nuget-package-with-github-actions/).

I decided to go with GitHub Actions using this [Publish NuGet Action](https://github.com/rohith/publish-nuget).

So, I incremented library minor version from 1.0.0 to 1.0.2 and published it.

But instead just updating version of the package, it was published as new one and now I have 2 packages.

And you can't just delete package from Nuget Gallery, you can only unkist it and I unlisted version 1.0.0.

Just to check how versioning works, I incremented version to 1.0.3 and published again.

And now I have [package](https://www.nuget.org/packages/WikiDataLib/) (two versions).
