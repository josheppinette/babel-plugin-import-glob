# Babel Plugin Import Glob

Babel plugin to enable importing modules using glob patterns.

## Usage

Given the following file structure:

```txt
├── images
│   ├── cat.webp
│   └── dog.webp
└── videos
    ├── example-1.mp4
    └── example-2.mp4
```

_Simple_

```js
import { cat, dog } from './images/*.webp'
```

_Alias_

```js
import { cat as c, dog as d } from './images/*.webp'
```

_Default_

```js
import videos from './videos/*.mp4'

console.log(videos['example-1'])
```

_Namespace_

```js
import * as videos from './videos/*.mp4'

console.log(videos['example-1'])
```

## Install

```sh
$ npm install @jteppinette/babel-plugin-import-glob
```

**Configuration**

This plugin simply needs to be added to the Babel plugins array.

Here is a simple bare-bones babel configuration file which only supports
this singular plugin.

_.babelrc_

```json
{
  "plugins": ["@jteppinette/babel-plugin-import-glob"]
}
```

## History

This repo was originally forked from and inspired by [novemberborn/babel-plugin-import-glob](https://github.com/novemberborn/babel-plugin-import-glob). All license and git commits have been kept intact.

The origin repo mentioned above had stagnated for many years and was missing a features that I needed:

- You could not import the default export.
- Namespace import keys were transformed into valid identifiers instead of simply using their wildcard path names.

While I do not think we would ever merge the two, I would be open to the idea.

## Development

### Required Software

If you are using [nix](https://zero-to-nix.com/start/install/) & [direnv](https://direnv.net/docs/installation.html), then your dev environment will be managed automatically. Otherwise, you will need to manually install the following software:

- [direnv](https://direnv.net/docs/installation.html)
- [git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- [nvm](https://github.com/nvm-sh/nvm?tab=readme-ov-file#installing-and-updating)
- [pre-commit](https://pre-commit.com/#install)

### Getting Started

**Setup**

> If you are using nvm, you will need to install the correct version of node using `nvm install $(cat .node-version)`.

```sh
$ direnv allow
$ pre-commit install
$ npm install
```

**Test**

```sh
$ npm test
```

### Publishing

The publish process is automated by GitHub Actions. Once a release is
created (at the end of these steps), the package will be published to
the public npm registry.

Authentication uses npm [trusted publishing](https://docs.npmjs.com/trusted-publishers)
(OIDC), so no long-lived token is required. This is a one-time setup on
npmjs.com: configure this repository and the `publish` workflow as a
trusted publisher for the package.

1. Bump version, commit, and tag:

   ```sh
   $ npm run version:<major|minor|patch>
   ```

2. Commit the changes, tag the commit, and push the tags:

   ```sh
   $ git push origin main --tags
   ```

3. Convert the tag to a release in GitHub.

   ```sh
   $ open "https://github.com/jteppinette/babel-plugin-import-glob/releases/new?tag=<tag>"
   ```
