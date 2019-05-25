# Setup Inicial

## Meus Globais
Instalei o setup do Wesbos global, para que não tenha toda vez que instalar localmente. Para remover, basta o comando

```bash
npm remove --global eslint-config-wesbos babel-eslint eslint eslint-config-prettier eslint-config-airbnb eslint-plugin-html eslint-plugin-prettier eslint-plugin-import eslint-plugin-jsx-a11y eslint-plugin-react prettier eslint-plugin-react-hooks
```

Lembrar também de deletar o arquivo `~/.eslintrc`

## Iniciando
Vamos integrar o **eslint**, o **Prettier** e o **Airbnb Style Guide**. Vamos seguir o tutorial do Wesbos.
[Tutorial](https://github.com/wesbos/eslint-config-wesbos)

Abaixo estão as instruções do Wesbos. Se formos usar outras configs, recomendo essas [aqui](https://blog.echobind.com/integrating-prettier-eslint-airbnb-style-guide-in-vscode-47f07b5d7d6a)

## 1. Download Prettier e ESLint extensions para VSCode

Nada a dizer sobre esse passo.

## Installing

You can use eslint globally and/or locally per project.

It's usually best to install this locally once per project, that way you can have project specific settings as well as sync those settings with others working on your project via git.

I also install globally so that any project or rogue JS file I write will have linting and formatting applied without having to go through the setup. You might disagree and that is okay, just don't do it then 😃.

## Local / Per Project Install

1. If you don't already have a `package.json` file, create one with `npm init`.

2. Then we need to install everything needed by the config:

```bash
npx install-peerdeps --dev eslint-config-wesbos
```

3. You can see in your package.json there are now a big list of devDependencies.

4. Create a `.eslintrc` file in the root of your project's directory (it should live where package.json does). Your `.eslintrc` file should look like this:

```json
{
  "extends": ["wesbos"]
}
```

Tip: You can alternatively put this object in your `package.json` under the property `"eslintConfig":`. This makes one less file in your project.

5. You can add two scripts to your package.json to lint and/or fix:

```json
"scripts": {
  "lint": "eslint .",
  "lint:fix": "eslint . --fix"
},
```

6. Now you can manually lint your code by running `npm run lint` and fix all fixable issues with `npm run lint:fix`. You probably want your editor to do this though.

## Settings

If you'd like to overwrite eslint or prettier settings, you can add the rules in your `.eslintrc` file. The [ESLint rules](https://eslint.org/docs/rules/) go directly under `"rules"` while [prettier options](https://prettier.io/docs/en/options.html) go under `"prettier/prettier"`. Note that prettier rules overwrite anything in my config (trailing comma, and single quote), so you'll need to include those as well.

```js
{
  "extends": [
    "wesbos"
  ],
  "rules": {
    "no-console": 2,
    "prettier/prettier": [
      "error",
      {
        "trailingComma": "es5",
        "singleQuote": true,
        "printWidth": 120,
        "tabWidth": 8,
      }
    ]
  }
}
```

## With VS Code

You should read this entire thing. Serious!

Once you have done one, or both, of the above installs. You probably want your editor to lint and fix for you. Here are the instructions for VS Code:

1. Install the [ESLint package](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
2. Now we need to setup some VS Code settings via `Code/File` → `Preferences` → `Settings`. It's easier to enter these settings while editing the `settings.json` file, so click the `{}` icon in the top right corner:

```js
  // These are all my auto-save configs
"editor.formatOnSave": true,
// turn it off for JS and JSX, we will do this via eslint
"[javascript]": {
  "editor.formatOnSave": false
},
"[javascriptreact]": {
  "editor.formatOnSave": false
},
// tell the ESLint plugin to run on save
"eslint.autoFixOnSave": true,
// Optional BUT IMPORTANT: If you have the prettier extension enabled for other languages like CSS and HTML, turn it off for JS since we are doing it through Eslint already
"prettier.disableLanguages": ["javascript", "javascriptreact"],
```

## Arquivos usados no boilerplate

- Tive que criar um `package.json` para colocar os pacotes.
- Também criei um `.eslintrc` que contém as infos do eslint que quero fazer override.
- Criei aqui um `.markdownlint.json` que é para a extensão markdownlint do vscode, para desabilitar alguns códigos de erro no MD.
- Criei um arquivo `example-code.js` para brincar com js e linting
