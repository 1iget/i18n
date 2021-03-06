# Contributing to electron-i18n

🇨🇳 🇹🇼 🇧🇷 🇪🇸 🇰🇷 🇯🇵 🇷🇺 🇫🇷 🇹🇭 🇳🇱 🇹🇷 🇮🇩 🇺🇦 🇨🇿 🇮🇹

💚 First off, thanks for taking the time to contribute! 💚

Anyone is welcome to join in the effort, regardless of technical experience or 
familiarity with the Electron project.

This project adheres to the Contributor Covenant [code of conduct](code_of_conduct.md).
By participating, you are expected to uphold this code. Please report unacceptable
behavior to electron@github.com.

The following is a set of guidelines for contributing to Electron's localization
effort. These are just guidelines, not rules, so use your best judgment and 
feel free to propose changes to this document in a pull request.

## Translating

Here are some guidelines to keep in mind as a translator:

- Don't open pull requests to translate Electron; instead, do all translations on  [Crowdin](https://crowdin.com/project/electron).
- Do not translate JavaScript keywords like `String`, `Event`, `Array`, `Class`, etc.
- Do not translate Electron classes, method names, event names, etc.
- If you find an error in the source English docs, open a pull request on the [electron/electron](https://github.com/electron/electron/tree/master/docs) repository.
- If you've been working as a translator and want to have more influence over the approved translations in your language, let us know and we'll make you a proofreader.

Electron's localization effort uses [Crowdin], an awesome platform for 
collaborative translation. Changes on Crowdin are  automatically turned into 
pull requests on this GitHub repository.

To get started, visit 
**[crowdin.com/project/electron](https://crowdin.com/project/electron)** 
and log in with your GitHub account.

## Proofreading

If you're using a platform like Utopian.io and would like to be promoted to 
proofreader status on the Electron project, please translate 1,000 words or 
more before applying. When contacting us, please include a link to your existing translations on the project.

## Developing `electron-i18n`

The rest of this document describes how this repo is structured, how
it syncs with Crowdin, and how to make technical changes.

**If you're just here to translate, you probably don't need to read this.**

### Environment Setup

To fetch the latest docs, you need a GitHub token. Visit
github.com/settings/tokens/new](https://github.com/settings/tokens/new)
to create one. No special scopes needed.

```sh
cp .env.example .env
```

Then edit `.env` and add your token. 

```sh
npm run build
```

### Adding a Language

Occasionally people ask for new languages to be enabled for translation. The 
process for this is simple:

1. Visit https://crowdin.com/project/electron/settings#translations
1. Click the [Target Languages] button.
1. Choose your language(s) you wish to add (or remove):

<img src="https://user-images.githubusercontent.com/2289/34370816-40f085bc-ea7c-11e7-9700-8d346d61113f.png">

That's it! The Crowdin stats and language list in the README will be updated automatically when `npm run build` is run.

### Source Content

Electron's documentation and website are authored in English.

The source content in this repo is collected from a few places:

- Markdown files from the [electron](https://github.com/electron/electron/tree/master/docs) repo.
- YAML files from the [electronjs.org](https://github.com/electron/electronjs.org/blob/master/data/locale.yml) repo
- Electron's [structured API docs](https://electronjs.org/blog/api-docs-json-schema).

Here's the directory structure:

```
content
└── en-US
    ├── api
    ├── docs
    └── website
```

### Translated Content

[The Crowdin project](https://crowdin.com/project/electron) is configured to automatically **pull** the latest English content out of this repo and **push** the translated content back into this repo.

Translations are added under a directory named after the locale. The _contents_ of these files differ by language, but the _directory structure and filenames_ for each locale is always identical.

```
content
├── en-US
│   ├── api
│   ├── docs
│   └── website
├── es-ES
│   ├── api
│   ├── docs
│   └── website
├── pt-BR
│   ├── api
│   ├── docs
│   └── website
└── zh-TW
    ├── api
    ├── docs
    └── website
```

To get a sense of how content is transformed, see [crowdin.yml](crowdin.yml)

[Crowdin]: https://crowdin.com/project/electron
