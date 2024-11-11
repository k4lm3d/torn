# Hexo Icarus Starter Template (hist)

***(Feel free to change or delete this file)***

- Technology: [Hexo](https://hexo.io/)
- Theme: [Icarus](https://ppoffice.github.io/hexo-theme-icarus/) by [PPOffice](https://github.com/ppoffice)

## Documetations:

- [Hexo Documentation](https://hexo.io/docs/)
- [Icarus Theme Documentation](https://ppoffice.github.io/hexo-theme-icarus/uncategorized/getting-started-with-icarus/)

## Procedures:

- [Install **Hexo** and its dependencies](https://hexo.io/docs/#Installation)
- [Setup an Hexo site](https://hexo.io/docs/setup/)
- [Install Icarus as a node package via NPM](https://ppoffice.github.io/hexo-theme-icarus/uncategorized/getting-started-with-icarus/#install-npm)
- Start the Hexo local server: `hexo server`

___

# Deploy on GitHub Pages

If you're using GitHub Pages, uncomment the code below the `_config.yml`:

```yml
deploy:
  type: git
  repo: https://github.com/username/username.github.io.git
  branch: gh-pages
  message: "Site updated {{ now('YYYY-MM-DD HH:mm:ss') }}"
```

Then, create a `workflow` folder inside `.github` directory and `pages.yml` file inside it. Then, copy and paste the code below.

```yml
name: Pages

on:
  push:
    branches:
      - main  # default branch

jobs:
  pages:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - uses: actions/checkout@v3
        with:
          token: ${{ secrets.GITHUB_TOKEN }}
          # If your repository depends on submodule, please see: https://github.com/actions/checkout
          submodules: recursive
      - name: Use Node.js 18.x
        uses: actions/setup-node@v2
        with:
          node-version: '16'
      - name: Cache NPM dependencies
        uses: actions/cache@v2
        with:
          path: node_modules
          key: ${{ runner.OS }}-npm-cache
          restore-keys: |
            ${{ runner.OS }}-npm-cache
      - name: Install Dependencies
        run: npm install
      - name: Build
        run: npm run build
      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public

```
