---
title: Yarn 2 and Private Repos with Authentication
date: 2020-03-10T22:34:37.408Z
draft: true
---
One of the problems I faced recently trying out Yarn 2, was configuring it to authenticate a private repository. The project uses Font Awesome Pro, which requires you to configure their repo in your `.npmrc` file and provide an auth token.

Yarn 2 no longer reads the `.npmrc` file, and private registries have to be configured in the project's `.yarnrc.yml` file instead.

It took me a little playing around and squinting at the docs in order to get the right config settings, so I'm posting them here in case they're helpful to someone else.

```yml
npmRegistries:
    //npm.fontawesome.com:
        npmAlwaysAuth: true
        npmAuthToken: "YOUR-TOKEN"
npmScopes:
    fortawesome:
        "https://npm.fontawesome.com"
```
