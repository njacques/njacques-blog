---
title: Yarn 2 and Private Repos with Authentication
date: 2020-03-15T16:00:37.408Z
draft: false
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

To break down the settings here:

1. **npmScopes**: You need to tell Yarn to use a private registry for a given namespace. In this case, the namespace is `@fontawesome` but as per the Yarn docs we drop the `@` symbol as it's not valid here.
2. **npmRegistries**: Yarn also needs to know about the authentication for the private registry, so we create a key with the URL of the registry (here omitting the protocol, so it works with both http and https). Nested within this, you can supply the auth token.

Hopefully this might help someone out.
