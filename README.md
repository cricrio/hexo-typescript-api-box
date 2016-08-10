# Typescript API box

## Installation

Add this package to your hexo site:

```
npm install --save hexo-typescript-api-box
```

Configure this plugin to point it at your `docs.json` (see below), in `_config.yml`:

```
typescript_api_box:
  data_file: docs.json
```

## Generating docs.json

Add the code you want to document as a submodule:

```
git submodule add URL_OF_REPO code
```

Add typedoc (our branch for now, pending https://github.com/TypeStrong/typedoc/pull/266) as a dependency of your project:

```
npm install --save typedoc@tmeasday/typedoc#add-source-to-json-built
```

Generate docs.json with an npm script similar to:

```
"scripts": {
    "build": "cd code; typedoc --json ../docs.json",
    "prestart": "npm run build",
    "start": "hexo serve",
    "predeploy": "npm run build",
    "deploy": "hexo-s3-deploy",
  }
```

> Note that we've added the `build` script as a `prestart` and `predeploy` script which makes sense.

## Usage

To use a code reference, use the `tsapibox` tag:

```
{% tsapibox ApolloClient.constructor %}
```

In this version this will be an H3 (nested sidebar entry). We'll probably iterate on this.

Ensure you've added a box for each referenced type, or the links will go nowhere.

## Theming

The build HTML is styled by the [hexo-theme-meteor](https://github.com/meteor/hexo-theme-meteor).
