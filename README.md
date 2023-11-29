<h1 align="center" width="100%">
  <img src="https://raw.githubusercontent.com/jstayton/suri/v1/logo.png" width="200" alt="Suri" />
</h1>

<h3 align="center" width="100%">
  <i>Your own shortlinks as an easily deployed static site with Node.js</i>
</h3>

You're viewing a template repository tailored for deploying Suri with Node.js.
That could be on a cloud platform that supports Node.js and/or serving static
sites, or just on your own machine. Head over to
[the main repository](https://github.com/surishortlink/suri) to learn more about
Suri, including additional deployment options.

## Setup: Step By Step

1. Hit the "Use this template" button above and then "Create a new repository".
   Fill in the required details to create a new repository based on this one.
2. Make sure you have a compatible version of [Node.js](https://nodejs.org/)
   (see `engines.node` in [`package.json`](package.json)).
   [nvm](https://github.com/nvm-sh/nvm) is the recommended installation method
   on your own machine:

   ```bash
   nvm install --lts
   ```

3. Install dependencies with npm:

   ```bash
   npm install
   ```

4. Build the static site:

   ```bash
   npm run build
   ```

5. Deploy the generated `build` directory to its final destination.

## How It Works

### Manage Links

At the heart of Suri is the [`links.json`](src/links.json) file, located in the
`src` directory, where you manage your links. All of the template repositories
include this file seeded with a few examples:

```json
{
  "/": "https://www.youtube.com/watch?v=CsHiG-43Fzg",
  "1": "https://fee.org/articles/the-use-of-knowledge-in-society/",
  "gh": "https://github.com/surishortlink/suri"
}
```

It couldn't be simpler: the key is the "shortlink" path that gets redirected,
and the value is the target URL. Keys can be as short or as long as you want,
using whatever mixture of characters you want. `/` is a special entry for
redirecting the root path.

### Build Static Site

Suri ships with a `suri` executable file that generates the static site from the
`links.json` file. The static site is output to a directory named `build`.

All of the template repositories are configured with a `build` script that
invokes this executable, making the command you run simple:

```bash
npm run build
```

When you make a change to the `links.json` file, simply re-run this command to
re-generate the static site, which can then be re-deployed.

### Config

Configuration is handled through the [`suri.config.json`](suri.config.json) file
in the root directory. There is only one option at this point:

| Option | Description                                                        | Type    | Default |
| ------ | ------------------------------------------------------------------ | ------- | ------- |
| `js`   | Whether to redirect with JavaScript instead of a `<meta>` refresh. | Boolean | `false` |

### Public Directory

Finally, any files in the `public` directory will be copied over to the `build`
directory without modification when the static site is built. This can be useful
for files like `favicon.ico` or `robots.txt` (that said, Suri provides sensible
defaults for both).
