# github-ci-npm-publish

A simple npm package with a GitHub Actions workflow that publishes to npm when a `v-*` tag is pushed.

The publishable package lives in **`packages/x`**; the workflow builds and publishes only that package.

## Publishing

1. **Create an npm access token**  
   On [npmjs.com](https://www.npmjs.com/) → Account → Access Tokens → Generate New Token (choose “Automation” for CI).

2. **Add the token to GitHub**  
   In your repo: **Settings** → **Secrets and variables** → **Actions** → **New repository secret**  
   - Name: `NPM_TOKEN`  
   - Value: your npm token

3. **Release by pushing a tag**  
   Tag format must be `v-` followed by the version (e.g. `v-1.0.0`):

   ```bash
   git tag v-1.0.0
   git push origin v-1.0.0
   ```

   The workflow will run, set the package version from the tag, and publish to npm.

## Workflow

- **Trigger:** Push of a tag matching `v-*` (e.g. `v-1.0.0`, `v-2.1.3`).
- **Version:** The part after `v-` becomes the published version (e.g. `v-1.0.0` → `1.0.0`).
- **Scope:** Only the package in **`packages/x`** is built and published; the rest of the repo is ignored for publish.

To publish a different path, edit `.github/workflows/publish.yml` and change the `defaults.run.working-directory` value (e.g. to `packages/my-package`).

## License

ISC
