---
title: Tailwindcss In NextJS
description: Setting up Tailwindcss In A NextJS Project
featuredImgURL: https://source.unsplash.com/featured/?space,moon
featuredImgAlt: nextjs tailwind image
slug: tailwind-nextjs
keywords: NextJS, Tailwind, React
---


[Tailwindcss](https://www.tailwindcss.com)

In this guide, we'll walk through how to install [Tailwindcss](https://www.tailwindcss.com) in a new [Next.js](https://nextjs.org) project.
To start off you will create a new nextjs project

```
npm init next-app tailwind-next-example

```

## Step 1: Install the dependencies

To install the plugin, use your favorite package manager.

```
npm install tailwindcss autoprefixer postcss-loader --save-dev
```

and also install the next-css plugin:

```
npm install @zeit/next-css
```

## Step 3: Configure the build pipeline

you will need to create a postcss.config.js file in the root of you app

Open up your gatsby-config.js, and add 'gatsby-plugin-postcss' to the plugins array.

```
module.exports = {
  plugins: [
    require('tailwindcss'),
    require('autoprefixer')
  ]
};
```

and then you will also need a next.config.js

```
const withCSS = require('@zeit/next-css');

module.exports = withCSS({});

```

** Note October 1 2019, there is a current bug in next.js loader so use the following ~~~~ hack if you encounter it **

```
const withCSS = require('@zeit/next-css');

function HACK_removeMinimizeOptionFromCssLoaders(config) {
  console.warn(
    'HACK: Removing `minimize` option from `css-loader` entries in Webpack config',
  );
  config.module.rules.forEach(rule => {
    if (Array.isArray(rule.use)) {
      rule.use.forEach(u => {
        if (u.loader === 'css-loader' && u.options) {
          delete u.options.minimize;
        }
      });
    }
  });
}

module.exports = withCSS({
  webpack(config) {
    HACK_removeMinimizeOptionFromCssLoaders(config);
    return config;
  },
});

```

## Step 3: Add Tailwindcss to CSS file

Everything should be ready to go, all we need to do now is to actually use Tailwind within our CSS! First, create a global.css file. I put mine at styles/tailwind.css. Then, add the following Tailwind directives to your new file:

// tailwind.css

```
@tailwind base;

@tailwind components;

@tailwind utilities;
```

## Step 4: Import css into the project

Now before we configure PostCSS to use Tailwind, we need to install it.

** Using NPM **

```
  import React from 'react'
  import Link from 'next/link'
  import Head from 'next/head'
  import Nav from '../components/nav'
  import '../styles/tailwind.css'

  const Home = () => (
    <div>
      <Head>
        <title>Home</title>
      </Head>
```

## Step 5: Have fun

Eventually, you may wish to import your CSS in a custom component to ensure it gets loaded on every page.

You can now start using Tailwind CSS utilities in your className attributes!



## Credits

[statickit](https://statickit.com/guides/next-js-tailwind) Most of this is a modification of that list of steps

