---
layout: post
title: A day on github action
tags:
  - github action
  - cicd  
comments: true
image:
  path: /images/github-actions/github-actions.jpg
---

Today, when I explore my github account, I see many projects I created in the past during my spare time using .NET. There are some projects I'm still hoping I could complete them one day, however due to the complexity of those project setup, it takes much longer to resume the development and publish beta version whenever I have spare time. 
<!--more-->

Luckily, GitHub offers free CI/CD platform - `GitHub Actions` that lets me easily automate the build, test and deployment pipeline. In addtion, it offers free package management platform - `GitHub Packages` that allows me to host and manage my projects' packages in private. These two platform combined together provides most I need for all my projects, so I decide to take a day tuor among these two platforms and hopefully I could get something working at the end. 

Usually when I start something new in a short time, my first thing is to write down a list of puzzles/chanllenges I might be enocuntered and do a quick search on the web to get some clarity

## Chanllenges

### Github Actions

#### How and where to start the intial setup? 

GitHub actions is pretty simple to start, it has a starter kit template for various of projects. As soon as you have your project hosted on github, you can start by clicking on "Actions" from menu and pick up the workflow template suitable for your project type. I choose .NET from `Continous integration` section as start.

<img src="images/github-actions/1.png" width="50%"/>


#### How much free time do I have before I get charged? 

From my understanding,for GitHub free account, you won't be charged for `public` repositories. For `private` repositories, there are certain amount of free minutes for hosted runner (aka build engine consumption) and storage listed below.

<img src="images/github-actions/2.png" width="50%"/>

[About billing for GitHub Actions](https://docs.github.com/en/billing/managing-billing-for-github-actions/about-billing-for-github-actions){:target="_blank"}

#### Where can I find succinct documents (no more than 2-3)? 
I personally find docs below are very helpful for me to get the CI/CD up running and publish the packages to GitHub Packages
- [Understanding GitHub Actions](https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions)
- [Workflow syntax for GitHub Actions](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions){:target="_blank"}
- [Publishing a NuGet package using GitHub and GitHub Actions](https://www.meziantou.net/publishing-a-nuget-package-following-best-practices-using-github.htm){:target="_blank"}
  
### Github Packages

#### How can I upload the packages? 
You can find more details from [Working with the NuGet registry](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-nuget-registry){:target="_blank"}.

If you ever work with other package management platform in .NET, you probably only need to know the following two commands

**Add source server and authenticate to GitHub Packages**

```
dotnet nuget add source --username USERNAME --password ${{ secrets.GITHUB_TOKEN }} --store-password-in-clear-text --name github "https://nuget.pkg.github.com/NAMESPACE/index.json"
```
> `USERNAME` is the name of your personal account on GitHub. 
> 
> [GITHUB_TOKEN](https://docs.github.com/en/actions/security-guides/automatic-token-authentication#using-the-github_token-in-a-workflow){:target="_blank"} is a authenticate token GitHub recommends to use for access and publish packages associated with the workflow repository. 
> 
> `NAMESPACE` is the name of the personal account or organization to which your packages are scoped.
{: .prompt-info }

> If you run above command to add GitHub Packages source from your machine, you need to use [Personal Access Token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens) as password 
{: .prompt-tip } 

**Publish package**

```
dotnet nuget push "bin/Release/PROJECT_NAME.1.0.0.nupkg"  --api-key YOUR_GITHUB_PAT --source "github"
```
> [YOUR_GITHUB_PAT](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens){:target="_blank"} is your personal access token.
{: .prompt-info }

> If you have already configured authentication in [Add source server and authenticate to GitHub Packages](#how-can-i-upload-the-packages), you don't have to supply `--api-key`
{: .prompt-tip } 

#### How can I access the packages? 
You can find more details from [Installing a package](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-nuget-registry#installing-a-package)

#### Where to find the packages from UI?
You can find more details from [Viewing a repository's packages](https://docs.github.com/en/packages/learn-github-packages/viewing-packages#viewing-a-repositorys-packages){:target="_blank"}

#### Are there any limitations in free version? 
Yes, GitHub offers `500 MB` storage `per repository` if I understand correctly. The storage used by a repository is the total storage used by GitHub Actions artifacts and GitHub Packages.

<img src="images/github-actions/2.png" width="50%"/>

[About billing for GitHub Actions](https://docs.github.com/en/billing/managing-billing-for-github-actions/about-billing-for-github-actions){:target="_blank"}

## Put everything in action

It's time to put everyhing in action as all above chanllenges have been resolved. 

Here is what I would like to experiment with GitHub Actions and Packages

1. Build the solution when code changes are made in `main` branch
2. Create nuget package and upload to GitHub Packages when I create `release` from GitHub repository and associate package version with release name.

### Flowchat
<img src="images/github-actions/Github-Actions-Net-Flow.jpg" width="50%"/>

### The `YAML`
<details>
<summary>Click to expand</summary>

<script src="https://gist.github.com/javafun/ee4948ff2d52f422c23d40205dd126df.js"></script>

</details>


### The `YAML` with reusable actions (cleaner)

<details>
<summary>Click to expand</summary>

<script src="https://gist.github.com/javafun/856783ff464c025f79bbe49b9778badc.js"></script>

<script src="https://gist.github.com/javafun/4999aec8c0937b532e57388f32222d11.js"></script>

</details>


### Outcome
<img src="images/github-actions/create-upload-package.gif" width="80%"/>


## Reference
* [GitHub Actions](https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions){:target="_blank"}
* [GitHub Packages](https://docs.github.com/en/packages/learn-github-packages/introduction-to-github-packages){:target="_blank"}
* [Default environment variables](hhttps://docs.github.com/en/actions/learn-github-actions/variables#default-environment-variables){:target="_blank"}
* [Workflow syntax for GitHub Actions](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions){:target="_blank"}
* [Sharing steps in github action workflow](https://www.jameskerr.blog/posts/sharing-steps-in-github-action-workflows/){:target="_blank"}
* [Composite Actions](https://docs.github.com/en/actions/creating-actions/about-custom-actions#composite-actions){:target="_blank"}
* [Publishing a NuGet package using GitHub and GitHub Actions](https://www.meziantou.net/publishing-a-nuget-package-following-best-practices-using-github.htm){:target="_blank"}
* [Working with the NuGet registry](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-nuget-registry){:target="_blank"}
* [About billing for GitHub Actions](https://docs.github.com/en/billing/managing-billing-for-github-actions/about-billing-for-github-actions){:target="_blank"}
* [About billing for GitHub Actions](https://docs.github.com/en/actions/learn-github-actions/usage-limits-billing-and-administration){:target="_blank"}
  
Happy Coding! 😇
