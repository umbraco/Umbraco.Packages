# Umbraco v14 "Bellissima" Resources

Umbraco v14 brings us a new backoffice, codenamed Bellissima, that replaces the legacy technology of AngularJS with the modern technologies of Web Components, Lit and TypeScript. The v14 release is planned for the end of May 2024, the first beta was released on March 6th.

HQ and the community have been hard at work understanding the new technologies involved and sharing their learnings as they go. This  is a collection of the resulting videos, articles and source code that can help anyone wanting to build v14 'extensions' - a term that covers both packages and backoffice customisations.

Many thanks to [Markus Johansson](https://www.enkelmedia.se/blogg/2023/11/18/resources-for-umbraco-14-bellissima-new-backoffice) for taking the initiative on collecting these resources, and to everyone listed below who has been working and learning in public. As this is a public repo, if we are missing any resources please raise a PR to add them.

> [!TIP]
> Visit the `package-development` channel in the [Umbraco Discord Server](https://discord.com/channels/869656431308189746/882984798719729704) to read Bellissima discussions from the last few months, and post your own questions if you can't find answers elsewhere.

## The Front-end Technologies

If you want to do some background reading on the front-end technologies being used in Bellissima:

- Matt Brailsford listed [a glossary of key tech / concepts](https://dev.to/mattbrailsford/back-to-the-front-end-exploring-the-future-of-the-umbraco-ui-part-3-glossary-2aeh) that we need to learn about, with links for each.

- Markus Johansson recommends watching Michele Stieven's ["Using Lit and Web Components to build Single-Page Applications"](https://www.youtube.com/watch?v=I9RbleMxxXw) for a great overview of Lit and its different building blocks.

## HQ Documentation

Umbraco HQ is keeping the official documentation updated as the project progresses:

- [Beta Release Notes](https://our.umbraco.com/download/releases/1400) - expectation management about the status of the beta releases.

- [Backoffice Overview](https://docs.umbraco.com/umbraco-cms/v/14.latest-beta/extending-backoffice/customize-backoffice) - includes links to Storybook documentation and some terminology that we need to get familiar with.

- [Installing v14](https://docs.umbraco.com/umbraco-cms/v/14.latest-beta/fundamentals/setup/install/preview-builds) - unless you need to be cutting edge, use the 'prerelease' feed not the 'nightly' feed.

## Other Resources

> [!WARNING]
> Please remember that the resources listed below may be outdated. We have grouped them into sections, in descending date order.

### Videos

- 04/04/24 [Packages Question Time - Bellissima Edition](https://youtu.be/3wwWkgJG71U) - Community package developers put questions to Jacob and Filip from Umbraco HQ.

- 29/03/24 [umbraCoffee - Bellissima!](https://www.youtube.com/watch?v=COaq5oLRTvE) - umbraCoffee hosts Marcin and Callum talk with Richard Soeteman about his experience with the new backoffice while working on his packages Member Export, SEO Checker and Media Protect.

- 26/03/24 [Bellissima Migrazione dei Pacchetti](https://youtu.be/7QgpDzZ8Cys) - Lee Kelleher's talk about migrating packages to v14, first given at Umbraco Spark.

- 'UmbraCollab' sessions with Jacob Overgaard, Bellissima team lead at Umbraco HQ (recorded over Discord):
  - 18/04/24 [Umbraco Bellissima Property Editors - Part 4](https://www.youtube.com/watch?v=FrNgHrdg_m8) - the Our.Umbraco.GMaps property editor works, and a nuget package got created!
  - 11/04/24 [Umbraco Bellissima Property Editors - Part 3](https://www.youtube.com/watch?v=35rOUy8YBA4) - Sebastiaan and Jacob make even more progress!
  - 27/03/24 [Umbraco Bellissima Property Editors - Part 2](https://www.youtube.com/watch?v=U2k6Qoj5dyc) - Jacob helps us make progress with converting the Our.Umbraco.GMaps property editor.
  - 22/02/24 [Umbraco Bellissima Property Editors - First Look](https://www.youtube.com/watch?v=arztzoXqFzM) - Jacob helps us start with an empty install of a Bellissima preview release and build a property editor in JavaScript.

- 05/03/24 [Umbraco Kent Virtual Meetup on Bellissima](https://www.youtube.com/watch?v=SVpHFlKCJSw) - Jacob Overgaard gives a great explanation about the fundamentals about the new backoffice.

- 15/12/23 [Practical Adventures with Bellissima](https://www.youtube.com/watch?v=OwLOtzvx_o4) - Nathan Woulfe, lead developer on the Umbraco Workflow package at HQ, talks about his initial experience of migrating the Workflow package.

- 24/11/23 [Mounting your UI in the New Backoffice](https://www.youtube.com/watch?v=mxozXXPAALI) - Niels Lyngsø, UI/UX Engineer at Umbraco HQ, takes a deep dive into the core concepts of the new backoffice.

- 23/08/23 [Packages Question Time](https://www.youtube.com/watch?v=5vRzEMzrIec) - Bjarke Berg (the Head of CMS) and Niels Lyngsø answer package-related Bellissima questions from the community.

- 14/06/23 [Exploring the New Backoffice](https://www.youtube.com/watch?v=P14r9Sr0ATI) - Jacob Overgaard gives an early look at the new backoffice at Codegarden 2023.

### Articles

- 02/04/24 [Creating your own UI extension points](https://dev.to/mattbrailsford/series/26940) - Matt Brailsford shares a series of learnings from working on Umbraco Commerce v14.

- 21/03/24 [Using ChatGPT to Convert Backoffice Language Files](https://richardsoeteman.net/blog/converting-backoffice-language-files-using-chatgpt/) - Richard Soeteman shares how he used ChatGTP to automatically convert the backoffice language files in to the new Umbraco Bellissima format.

- 08/02/24 [Early Adopter's Guide to Umbraco v14 - Property Editors](https://dev.to/kevinjump/series/26366) - Kevin Jump's 3 part series about working with Property Editors.

- 02/02/24 [Early Adopter's Guide to Umbraco v14 - Gotchas](https://dev.to/kevinjump/series/26289) - Kevin Jump's ongoing collection of 'gotchas' that he's experienced.

- 30/01/24 [Early Adopter's Guide to Umbraco v14 - Communication](https://dev.to/kevinjump/series/26248) - Kevin Jump's 4 part series that covers how to communicate with the server.

- 27/01/24 [Early Adopter's Guide to Umbraco v14](https://dev.to/kevinjump/series/26221) - Kevin Jump's initial 14 part series about developing packages for Bellissima.

- 30/11/23 [Contentment for Bellissima](https://dev.to/leekelleher/contentment-for-bellissima-199d) - Lee Kelleher's thoughts about migrating Contentment.

- 16/11/23 [Umbraco 14 auto install](https://richardsoeteman.net/blog/auto-install-latest-umbraco-14/) - Richard Soeteman shares a Powershell script to automatically install Umbraco 14 and get it ready for package development.

- 23/09/23 [First Steps with Umbraco 14](https://www.andybutland.dev/2023/09/umbraco-14-package-migration.html) - Andy Butland, Head of DXP at Umbraco HQ, shares 4 posts about his first experiences with v14.

- 21/10/22 [Back to the Front-end](https://dev.to/mattbrailsford/series/20031) - Matt Brailsford's 10 part series exploring each aspect of the frontend tech stack.

### Source Code

- [Bellissima](https://github.com/umbraco/Umbraco.CMS.Backoffice) - the source code for the v14 new backoffice

- **Packages**

  - [Umbraco Workflow v14](https://github.com/umbraco/Umbraco.Workflow.Client.Preview/tree/main) - a preview of the client-side assets for Umbraco Workflow on v14, released by Nathan Wolfe for other package developers to review.

  - [uSync v14 branch](https://github.com/KevinJump/uSync/tree/v14/dev) - Kevin Jump's progress with the uSync package on v14.

  - [Contentment v14 branch](https://github.com/leekelleher/umbraco-contentment/tree/dev/wip/bellissima) - Lee Kelleher's progress with the Contentment package on v14.

  - [Personalisation Groups v14 branch](https://github.com/AndyButland/UmbracoPersonalisationGroupsCore/tree/feature/migrate-to-14) - Andy Butland's progress with the Personalisation Groups package on v14.

  - [UI Examples](https://github.com/umbraco/UI-Examples/tree/dev/v14) - examples of how to use the Umbraco UI in real scenarios in the back office (still under development).

  - [Examine Peek](https://github.com/warrenbuckley/Examine-Peek) - A small simple package to show creating an Umbraco Entity Action to open a custom dialog with a simple API call
