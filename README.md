# nextjs-monorepo

A proof of concept for an attempt to set up a monorepo-style NextJS serving implementation.

The key precepts we're trying to fit into is:

- NextJS running from a subdirectory, in this POC that's `sites/www.example.com`
- Application code distributed around the repo, for example here `apps/foo/*.tsx`
- Module resolution throughout the repo is "repo-absolute", which is exemplified by the import of `js/button` from `apps/foo/header.tsx`.

All of this code at the time of writing seems to typecheck fine. However, at runtime we get:

```
./app/mypage/page.tsx:1:1
Module not found: Can't resolve '../../../../apps/foo/header'
```

Looking at https://github.com/vercel/next.js/pull/22867, we should be able to enable the `experimental.externalDir` config setting to enable some form of usage like this. But there's no documentation about this config setting, and adding it to this project does not solve the problem above.
