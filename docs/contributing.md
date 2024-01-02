---
title: Contributing
---

This guide details how to contribute to this Repo and Site

## What contributions we take

Any!

You're welcome to fix grammar, typos, add pages, remove pages etc

## How to get up and running

Consider installing the below tools before working on this site

* Pre commit
* mkdocs

### Pre commit

Requires you have Pre-commit installed on your laptop. This just installs the local rules

```shell
pre-commit install
```

### mkdocs

Install mkdocs and then [material for mkdocs](https://squidfunk.github.io/mkdocs-material/getting-started/)

## Running the site

Once things are installed, you can run the below

```shell
mkdocs serve
```

You should then get the below

```text
INFO    -  Documentation built in 0.29 seconds
INFO    -  [14:44:53] Watching paths for changes: 'docs', 'mkdocs.yaml'
INFO    -  [14:44:53] Serving on http://127.0.0.1:8000/BeReal/
```

Navigate to http://127.0.0.1:8000/BeReal/ and the site should be live

## Adding a page

Before adding a page, open an [Issue](https://github.com/userbradley/BeReal/issues/new/choose) and select `New Page`

Once your new page is accepted, create the new page in the `docs/` directory under the desired location.

If we assume the example of `docs/domains/test.md`

We need to then add this to the `mkdocs.yaml` file to get the page to show up in the site

Add it to the desired location using the below example

```diff
nav:
...
  - Domains:
      - domains/index.md
      - Top Level Domains: domains/top-level-domains.md
      - Sub Domains: domains/sub-domains.md
+     - Test: domains/test.md
```

## Pushing Changes

Make sure you're working on a Fork of this repo.

Once ready, git commit and push your changes

```shell
git add .
git commit -m 'feat: <describe what you've done>'
git push
```

Click the `Contribute` button and Open a Pull request

## Errors you may see

### Precommit error

```text
Trims extra whitespaces..................................................Failed
```

Just run `git add .` and `git commit` again
