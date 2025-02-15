# Contributing to Backpack Foundations

You want to help us enable Skyscanner to create beautiful, coherent products at scale? That's awesome! :heart:

## Table of contents

* [Prerequisites](#prerequisites)
* [Getting started](#getting-started)
* [Adding a new component](#adding-a-new-component)
* [How to](#how-to)

## Prerequisites

### Licence

By contributing your code, you agree to license your contribution under the terms of the [APLv2](./LICENSE).

All files are released with the Apache 2.0 licence.

If you are adding a new file it should have a header comment containing licence information:

<details>
<summary>Show/hide licence header</summary>

```
Backpack - Skyscanner's Design System

Copyright 2016-<current year> Skyscanner Ltd

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

  http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```

</details>

### Installing Node

Backpack is developed using Node, using the following versions:

* `LTS/Gallium` (Node ^16.13.0)
* `^8.1.0` (npm)

This is enforced using a pre-install hook that calls out to [ensure-node-env](https://github.com/Skyscanner/ensure-node-env).

If you use [nvm](https://github.com/creationix/nvm) or [nave](https://github.com/isaacs/nave) to manage your Node environment, Backpack has built-in support for these. Just run `nvm use` to install the correct Node version.

To install npm, use `npm install --global npm@^8.1.0`.

### Code style

Backpack uses a combination of [ESLint](https://eslint.org) and [Prettier](https://prettier.io) to enforce coding styles. ESLint runs as a pre-commit hook, so it isn't possible to commit code that causes ESLint to fail.

We recommend that you install [a plugin to your editor](https://eslint.org/docs/user-guide/integrations#editors) to run ESLint automatically, which will then show you any errors inline. You can even enable an option to fix ESLint errors automatically upon saving.

## Getting started

### Getting the code

You should first fork the [foundations repo](https://github.com/Skyscanner/backpack-foundations/fork)

Then you should pull code down using the following command

```
git clone https://github.com/YOUR_USERNAME/backpack-foundations.git
```

### Install dependencies

Run `npm install` to install dependencies from npm.

<details>
<summary>A note on dependencies</summary>

Backpack Foundations is a multi-package repository, also known as a monorepo. This means that instead of having one code repository for each npm package, we manage them all inside this single repository.

We use [Lerna](https://lernajs.io) to achieve this. Lerna links packages together inside this repo by 'bootstrapping'.

When you run `npm install`, Lerna is bootstrapped automatically as a post-install hook. However, if you change dependencies within a package, you will need to run Lerna manually with `npm run bootstrap`.

</details>

### Build the code

Backpack Foundations code depends on some things that must be built first, such as icon fonts, SVGs and tokens.

Use `npm run build` to do this.

## Adding icons

If you want to add icons, please discuss them with us first.

Once they're signed off, you can [raise a request](https://bit.ly/backpack-request) and attach the SVG files. If you're feeling heroic and want to make the PR yourself, just copy the correctly named SVG files to the `lg` and `sm` directories in `./packages/bpk-svgs/src/icons/` and then run `npm run build`.

### Tokens

Any visual CSS parameters of the component, such as *color, margins, paddings* etc. should not live as magic numbers in the component code, but as **tokens** in the `bpk-<android/ios/react-native/web/common>` package.

Tokens are defined in the `src/base` directory. Tokens come in two layers: In `aliases.json`, all base tokens are defined with concrete values, such as colours, numbers and sizes. The other files then map those aliases to tokens for specific elements.

> You should probably not touch `aliases.json`, as our color palette or grid rarely changes.

#### Backpack documentation

For documentation changes, please see our [Backpack docs repo](http://github.com/Skyscanner/backpack-docs).

## How to

<details>
<summary>Create a pull request to Backpack Foundations</summary>

For anything non-trivial, we strongly recommend speaking to somebody from Koala before starting work on a PR. This lets us pass on any advice or knowledge we already have about the work you're proposing. It might even be something we're already working on. After this, follow the steps below.

1. [Fork the repository](https://github.com/Skyscanner/backpack-foundations/fork).
2. Create a new branch.
3. Make your changes.
4. Commit and push your new branch.
5. Submit a [pull request](https://github.com/Skyscanner/backpack-foundations/pulls).
6. Notify someone in Koala squad or drop a note in #backpack.

Don't forget to update [`UNRELEASED.md`](UNRELEASED.md) for any user-facing changes.

Bear in mind that small, incremental pull requests are likely to be reviewed faster.

</details>

<details>
<summary>Run tests</summary>

`npm test` will pick up any files that end in `-test.js`, so you don't need to do anything to make Jest pick them up.

You can also run the tests in 'watch mode', which means the process will continually run and run tests every time files change. Use `npm run jest:watch` to do this.

</details>

<details>
<summary>Run linters manually</summary>

* `npm run lint` to lint both JS and SCSS.
* `npm run lint:js` to lint JS.
* `npm run lint:js:fix` to lint and try to automatically fix any errors.
* `npm run lint:scss` to lint SCSS.
* `npm run lint:scss:fix` to lint and try to automatically fix any SCSS errors.

</details>

<details>
<summary>Publish packages (Koala squad members only)</summary>

- Update the [unreleased changelog](/UNRELEASED.md) with every package that has changed, separating out `BRAKING`, `ADDED` and `FIXED` changes. See [`CHANGELOG_FORMAT.md`](https://github.com/Skyscanner/backpack/blob/main/CHANGELOG_FORMAT.md) for tips.
  - Some useful commands for determining "what's changed?":
    - `npm run lerna updated`
    - `npm run lerna diff <package-name>`
- Make sure you are an owner of the npm packages (speak to a member of the Koala squad).
- **Run `npm run release`** (this will run several checks and then `lerna publish`). Do not run `npm publish`.
- You’ll be asked to confirm the new versions and descriptions for every package that has changed.
- If you need to make changes you can exit without confirming and no changes will be made.
- Once the publish is done, move anything from `UNRELEASED.md` to `CHANGELOG.md` and push these changes directly to `main`.

Be aware that if `bpk-foundations-common` has changed, *all* packages in the repository will be updated as they all depend on `bpk-foundations-common`. Changing an existing token is almost always worth a "major" release, whereas adding a new token is usually a "minor" release.

</details>

## And finally..

If you have any questions at all, don't hesitate to get in touch. We love to talk all things Backpack and we look forward to seeing your contribution!
