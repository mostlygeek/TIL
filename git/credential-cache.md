# Git Credential Cache

Github recommends cloning repositories via HTTPS. However, pushing changes requires entering your username and password each time. This can be avoided by using [git-credential-cache](https://git-scm.com/docs/git-credential-cache).

```
# set up to use an in memory cache
> git config --global credential.helper 'cache --timeout 7200'
> ... do some stuff
> git push
> Username for 'https://github.com':
> Password for 'https://<some user>@github.com'
> ...
```

After entering valid credentials they will be cached for 7200 seconds. The timeout can be tweaked for personal preference. 

Also if using multifactor authentication a Personal access token must be used instead of a regular username and password. These can be generated and revoked at [https://github.com/settings/tokens](https://github.com/settings/tokens).



