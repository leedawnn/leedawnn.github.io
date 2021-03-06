---
emoji: π
title: 'eslint, stylelint μ€μ νκΈ°(with VSCODE)'
date: '2022-05-10 01:30:00'
author: leedawn
tags: eslint stylelint prettier
categories: environment
---

## introduction

`ESLint`λ μ½λ© μ»¨λ²€μμ μλ°°λλ μ½λλ μν° ν¨ν΄μ μλ κ²μΆνλ λκ΅¬λ€. μ²μλΆν° μ μ©νκ² μ¬μ©ν  μ μλ μ€νμΌ κ°μ΄λ(built-in rule)μ μ κ³΅νμ§λ§ κ°λ°μκ° μμ μ μ€νμΌ κ°μ΄λλ₯Ό μμ±ν  μλ μλ€.

`Prettier`λ μ½λμ μ΅λ κΈΈμ΄, ν¨μμμ, μμλ°μ΄ν(')λ₯Ό μ¬μ©ν  κ²μΈμ§ μλλ©΄ ν° λ°μ΄ν(")λ₯Ό μ¬μ©ν  κ²μΈμ§ λ± μ½λκ° μμκ² λ³΄μ΄λλ‘ νλμ§μ μ€μ μ λμλ€. νμ§λ§ μ½λμ μλ¬λ₯Ό μ‘μλ΄μ§ λͺ»νλ€.

## install eslint & Airbnb style guide

`Airbnb style guide`λ₯Ό κΈ°λ³ΈμΌλ‘ `eslint`μ νμ νλ¬κ·ΈμΈλ€μ λ‘μ»¬ μ€μΉνμ. `eslint`λ₯Ό μ μ­μΌλ‘ μ€μΉν  μλ μμΌλ κΆμ₯νμ§ μλλ€. λ§μ½ μ μ­μΌλ‘ μ€μΉν  κ²½μ°μλ κ³΅μ  μ€μ κ³Ό νμ νλ¬κ·ΈμΈμ λ‘μ»¬ μ€μΉν΄ μ£Όμ΄μΌ νλ€. 

μ°Έκ³ λ‘ μ΄ κΈμμμ μ€νμΌ κ°μ΄λλ ``javascript``μ λν μ€λͺλ λ€μ΄μμ§λ§, ``react``μ ``typescript``λ₯Ό μ¬μ©νλ€λ κ°μ νμ μμ±λμλ€.

```bash
$ cd <project-folder>
$ npm init -y
# install eslint & plugins(μ¬κΈ°μ μ€λͺνλ νλ¬κ·ΈμΈμ΄ λλ¬΄ λ§μμ λ€ μ°μ§ μκ² λ€,,)
$ npm install -D eslint eslint-config-airbnb-base eslint-plugin-import eslint-plugin-html
```

| νλ¬κ·ΈμΈ                      | μ€λͺ                                                                                                          |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------- |
| eslint-config-airbnb          | Airbnbμ style guideλ₯Ό eslintμ μ€μ  νμΌμΈ .eslintrc.jsonμ νμ₯ν΄ μ£Όλ νλ¬κ·ΈμΈ(React κ΄λ ¨ νλ¬κ·ΈμΈ λ―Έν¬ν¨) |
| eslint-config-prettier        | λΆνμνκ±°λ prettierκ³Ό μΆ©λν  μ μλ λͺ¨λ  κ·μΉμ ν΄μ                                                        |
| eslint-config-react           | Reactμ λν lint μ€μ                                                                                         |
| eslint-config-react-app       | CRA(create-react-app)μμ μ¬μ© κ°λ₯ν lint μ€μ                                                                |
| eslint-plugin-flowtype        | flow typeμ λν lint μ€μ                                                                                     |
| eslint-plugin-import          | ES6+ import/export μ§μ νλ¬κ·ΈμΈ                                                                              |
| eslint-plugin-jsx-a11y        | μ νλ¦¬μΌμ΄μμ μ κ·Όμ± νμ€μ μ μ©νλ λ°νμ λΆμ λκ΅¬                                                        |
| eslint-plugin-prettier        | Prettierλ₯Ό ESLint νλ¬κ·ΈμΈμΌλ‘ μΆκ°. μ¦, Prettierμμ μΈμνλ μ½λμμ ν¬λ§· μ€λ₯λ₯Ό ESLint μ€λ₯λ‘ μΆλ ₯        |
| eslint-plugin-react           | λ¦¬μ‘νΈμ κ΄λ ¨λ λ£°μ μ μν νλ¬κ·ΈμΈ                                                                          |
| eslint-plugin-react-hooks     | λ¦¬μ‘νΈ hooksμ κ΄λ ¨λ λ£°μ μ μν νλ¬κ·ΈμΈ                                                                    |
| eslint-plugin-testing-library | νΉμ  νμ€νΈ λΌμ΄λΈλ¬λ¦¬ ν¨ν€μ§μ λν good practicesλ₯Ό μ μ©νλ κΆμ₯ κ΅¬μ±                                      |
| eslint-webpack-plugin         | JavaScript μ½λμ λ¬Έμ λ₯Ό μ°Ύκ³  μμ                                                                             |

> μΉν© Eslint κ³΅μ ννμ΄μ§μμλ loaderλ‘ μΈν eslintλ μ¬μ©νμ§λ§κ³  pluginμ ν΅ν΄μ μ¬μ©νλΌκ³  κΆνλ€.
> The loader eslint-loader will be deprecated soon, please use this plugin instead.

``typescript``λ₯Ό μ¬μ©νλ€λ©΄ λ€μκ³Ό κ°μ νλ¬κ·ΈμΈμ μΆκ°λ‘ κ³ λ €νμ.
| νλ¬κ·ΈμΈ | μ€λͺ |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------- |
| typescript-eslint/typescript-estree | ESTree(μλ°μ€ν¬λ¦½νΈ AST μ€ν) νΈν ASTλ₯Ό μμ±νλ νμμ€ν¬λ¦½νΈ νμ |
| typescript-eslint/parser | typescript-estreeλ₯Ό νμ©ν νμμ€ν¬λ¦½νΈμ© ESLint νμ(ESLint κΈ°λ³Έ νμμΈ espreeλ₯Ό λμ ν¨) |
| typescript-eslint/eslint-plugin | TypeScriptκ΄λ ¨ linting κ·μΉμ μ²λ¦¬νλ νλ¬κ·ΈμΈ |

## .eslintrc.json

νλ‘μ νΈ λ£¨νΈμ `.eslintrc.json` νμΌμ μμ±νκ³  νμμ λ°λΌ λ€μκ³Ό κ°μ΄ μ€μ μ λ³κ²½νλ€. μμΈν μ€μ  λ°©λ²μ [Configuring ESLint](https://eslint.org/docs/user-guide/configuring/)μ μ°Έμ‘°νλ€.

```json
{
  "extends": ["airbnb", "airbnb/hooks", "react-app", "prettier"],
  "env": {
    "browser": true,
    "jasmine": true,
    "jest": true
  },
  "settings": {
    "import/extensions": [".js", ".jsx"],
    "import/resolver": {
      "node": {
        "extensions": [".js", ".jsx"]
      },
      "typescript": {
        "project": "."
      }
    },
    "react": {
      "pragma": "React",
      "version": "detect"
    }
  },
  "rules": {
    // "off" or 0 - turn the rule off
    // "warn" or 1 - turn the rule on as a warning (doesnβt affect exit code)
    // "error" or 2 - turn the rule on as an error (exit code is 1 when triggered)
    // "no-var": "off",
    "arrow-body-style": "off",
    "semi": ["warn", "never"],
    "react/jsx-one-expression-per-line": "off",
    "react/jsx-filename-extension": ["error", { "extensions": [".js", ".jsx"] }],
    "react/jsx-indent": "warn",
    "react/jsx-props-no-spreading": "off",
    "react/no-array-index-key": "warn",
    "react/require-default-props": "off",
    "react/jsx-wrap-multilines": "off",
    "react/jsx-uses-react": "off",
    "react/react-in-jsx-scope": "off",
    "import/prefer-default-export": "off",
    "import/no-unresolved": "off",
    "import/order": "off",
    "import/no-anonymous-default-export": "off",
    "import/no-extraneous-dependencies": [
      "error",
      {
        "devDependencies": [".storybook/**", "src/stories/**"]
      }
    ],
    // "max-lines": ["warn", 150],
    "no-param-reassign": ["error", { "props": false }],
    "no-use-before-define": "off",
    "@typescript-eslint/no-use-before-define": ["error"],

    "no-shadow": "off",
    "no-unused-expressions": ["warn"],
    "@typescript-eslint/no-shadow": ["error"],
    "@typescript-eslint/camelcase": "off",
    "@typescript-eslint/unbound-method": "off",
    "@typescript-eslint/no-non-null-assertion": "off",
    "@typescript-eslint/no-unsafe-member-access": "off",
    "@typescript-eslint/no-unsafe-assignment": "off",
    "@typescript-eslint/no-unused-vars": ["warn", { "argsIgnorePattern": "^_" }],
    "prefer-const": ["warn"],
    "prefer-destructuring": ["error", { "object": true, "array": false }],
    "lines-between-class-members": "off",
    "jsx-a11y/click-events-have-key-events": "off",
    "jsx-a11y/label-has-associated-control": [
      "error",
      {
        "labelComponents": ["label"],
        "labelAttributes": ["htmlFor"],
        "controlComponents": ["input"]
      }
    ],
    "import/extensions": [
      "error",
      "ignorePackages",
      {
        "js": "never",
        "jsx": "never"
      }
    ]
  }
}
```

### extends

ESLint μ€μ μ νμ₯ (airbnb, prettierμ μ€μ μ μ μ©ν  μ μλ€.)

### env

μ¬μ  μ μλ μ μ­ λ³μλ₯Ό μ κ³΅νλ€. μλ₯Ό λ€μ΄, node νκ²½μΈ μν¬μ€νμ΄μ€λ©΄ ``node: true``λ₯Ό μΆκ°ν΄μΌ νκ³ , μΉ νκ²½μ΄λΌλ©΄ ``browser: true``, ``es6: true`` λ±μ μΆκ°ν΄μΌ νλ€.

### rules

μμ²΄μ μΌλ‘ μ μν κ·μΉμ μ μ© ([ESLint Rules](https://eslint.org/docs/rules/))

## install ESLint VSCode extention

VSCode λ§μΌνλ μ΄μ€μμ VS Code ESLint extensionμ μ€μΉνλ€.
λ©λ΄μ Code > κΈ°λ³Έ μ€μ  > μ€μ μΌλ‘ μ΄λνμ¬ `setting.json`μ μλ μ€μ μ μΆκ°νλ€.

```json
{
  "eslint.validate": [
    "html",
    "javascript",
    "javascriptreact",
    "typescript",
    "typescriptreact"
  ],
  "eslint.alwaysShowStatus": true,
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  }
}
```

λ§μ½, typescriptλ₯Ό μ¬μ©νλ€λ©΄ javascript λμ μ ``typescript``λ₯Ό λ£μ΄μ£Όμ.

## ESLint + Prettier

μ½λ ν¬λ§·ν°μΈ Prettierλ₯Ό μ€μΉνμ¬ ESLintμ ν¨κ» μ¬μ©ν΄λ³΄μ.

VSCode λ§μΌνλ μ΄μ€μμ prettier-vscode μ΅μ€νμμ μ€μΉνλ€.

prettier-vscode μ΅μ€νμμ μ€μΉν΄ μ¬μ©νλ€λ©΄ Prettierλ₯Ό λ³λ μ€μΉν  νμκ° μμ§λ§ Prettier CLIλ₯Ό μ¬μ©ν  κ²½μ°λ₯Ό λλΉν΄ Prettierλ₯Ό μ€μΉνλλ‘ νμ.

```bash
# --save-exact μ΅μμ μ¬μ©νμ¬ package.jsonμ ^ μμ΄ λ±λ‘λλλ‘ μ€μΉνλ€.
$ npm install --save-dev --save-exact prettier
```

νλ‘μ νΈ λ£¨νΈμ Prettierμ μ€μ  νμΌμΈ ``.prettierrc.json`` νμΌμ μμ±νκ³  λ€μκ³Ό κ°μ΄ μ€μ νμ. μμΈν μ€μ  λ°©λ²μ [Configuring Prettier](https://prettier.io/docs/en/configuration.html)λ₯Ό μ°Έμ‘°νλ€.

```json
{
  jsxSingleQuote: true
  semi: true
  printWidth: 120
  proseWrap: never
  singleQuote: true
  htmlWhitespaceSensitivity: "css"
  endOfLine: "lf"
}
```

## autofix

νμΌ μ μ₯κ³Ό ν¨κ» μ§λμΌλ‘ Prettier ν¬λ§·νμ΄ μ€νλλλ‘ νλ €λ©΄ λ©λ΄μ βCode > κΈ°λ³Έ μ€μ  > μ€μ βμΌλ‘ μ΄λνμ¬ ``settings.json``μ λ€μ μ€μ μ μΆκ°νλ€.

```json
...
  /////////////////////////////
  // ESLint
  "eslint.validate": [
    "html",
    "javascript",
    "javascriptreact",
    "typescript",
    "typescriptreact"
  ],
  "eslint.alwaysShowStatus": true,
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  }
  /////////////////////////////
  // Prettier
  // μμ  ν μ μ₯ν  λ prettierλ‘ μλ μ€νμΌλ§
  "editor.formatOnSave": true,
  // μμ  ν μ μ₯ν  λ eslintλ‘ autofix μ€ν (ex. let => const)
  "editor.codeActionsOnSave": { "source.fixAll.eslint": true },
  "editor.defaultFormatter": "esbenp.prettier-vscode",
...
```

## Babel-eslint

λ€μ μμ μ private νλ μ μ μ μκ³Ό κ°μ΄ μμ§ ECMAScript μ μ νμ€μ΄ μλ μ μ λ¨κ³μ μλ°μ€ν¬λ¦½νΈ μ½λμ κ²½μ° eslintκ° μμ€ μ½λλ₯Ό νμ±ν  μ μμ΄ μλ¬κ° λ°μνλ κ²½μ°κ° μλ€.

```javascript
class MyClass {
  #privateField = ''; // Parsing error: Unexpected character '#'
}
```

μ΄λ¬ν κ²½μ° ``babel-eslint``λ₯Ό μ¬μ©ν΄ μλ°μ€ν¬λ¦½νΈ μμ€ μ½λλ₯Ό νμ±ν΄μΌ νλ€. λ€μκ³Ό κ°μ΄ ``babel-eslint``λ₯Ό μ€μΉνλ€.

```bash
$ npm install --save-dev babel-eslint
```

νμ§λ§, μ΄ νλ‘μ νΈμμλ ``typescript`` κ΄λ ¨ ν¨ν€μ§κ° νμνκΈ° λλ¬Έμ μλμ κ°μ΄ μ€μΉν΄μ€λ€.

```bash
# typescript-eslint μ μ©
$ npm i --save-dev typescript eslint @typescript-eslint/parser @typescript-eslint/eslint-plugin
```

κ·Έ λ€μ, μλμ κ°μ΄ ``.eslintrc.json``μ parserλ₯Ό μ€μ νλ©΄ μλ¬κ° λ°μνμ§ μλλ€.
``Babel``κ³Ό ν¨κ» μ¬μ©λλ νμλ‘λ ``babel-eslint``κ° μκ³  ``Typescript`` κ΅¬λ¬Έ λΆμμ μν΄ μ¬μ©λλ ``@typescript-eslint/parser``κ° μλ€.

```json
{
  // "parser": "babel-eslint",
  "parser": "@typescript-eslint/parser"
  ...
}
```

``parserOptions``μ ESLint μ¬μ©μ μν΄ μ§μνλ €λ Javascript μΈμ΄ μ΅μμ μ§μ ν  μ μλ€.

```json
{
  "parser": "@typescript-eslint/parser",
  "parserOptions": {
    "project": "./tsconfig.json"
  },
  "env": {
    "node": true
  },
  "extends": ["plugin:@typescript-eslint/recommended"]
}
```

``"extends": ["plugin:@typescript-eslint/recommended"]`` μ€μ μ ν΅ν΄ @typescript-eslint/eslint-plugin μ μ©κ³Ό λμμ recommened κ·μΉμ νμ₯νλ€.

μμΈν λ΄μ©μ [recommened κ·μΉ μΈλΆλͺ©λ‘](https://github.com/typescript-eslint/typescript-eslint/tree/master/packages/eslint-plugin#supported-rules)μ μ°Έκ³ νμ.



> μΈμ© :
> https://poiemaweb.com/eslint 
> https://github.com/typescript-eslint/typescript-eslint#packages-included-in-this-project 
> https://github.com/miriyas/foundation

```toc

```
