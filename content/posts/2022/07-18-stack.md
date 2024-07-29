---
title: Not using Javascript to build a site in 2022
date: 2022-07-18
published: true
tags: ['frontend', 'tech stack']
canonical_url: false
description: "How I go about building single page landing pages as efficiently as possible?"
---

I have seen people use modern javascript framework to put out a simple website online. When we need just need a landing page that is mainly focused conveying/promoting/showing projects, using a complex tech stack is not really necessary. When you have a hammer, everything looks like a nail :P

I have built a few landing pages recently and I have tried use the platform features and minimal tech stack to achieve the same. This blog post is the run down of how I build them.

> If you use this approach, and use sematic HTML then your lighthouse score should be over 90 for performance, accessiblity and best practices. You may argue that its just a landing page, but I can give you examples of landing pages with really bad load times, 10 level deep `div` hell, unnecessary complex build setup.

# TECH/LANGUAGE's USED
* HTML
* CSS
* [OPEN PROPS](https://open-props.style)(not really necessary, helps in quick prototyping - but don't use frameworks, please)
* Javacript(optional)
* Github/Bitbucket
* [BROWSERSYNC](https://browsersync.io/)
* little bit of SHELL commands(use can use file explorer)
* [BUNNY FONTS](https://fonts.bunny.net/)
* SVG for favicon
* [UNSPLASH](https://unsplash.com) for social image
* [SQUOOSH](https://squoosh.app) to compress image
* [NETLIFY](https://netlify.app) to deploy the site

> Let say you want to build a personal website displaying your career details, contact information, display picture, projects, side projects and achievements.

# STEP 1: Make a directory and create 3 files. `index.html`, `styles.css`, `scripts.js`(optional)
```bash
mkdir [name of project]
cd [name of project]
touch index.html styles.css scripts.js
```

# STEP 2: Open the folder in a text editor, open `index.html` and paste the code block below and change stuff within [] as needed
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <meta name="theme-color" content="[choose a color]">

  <title>[choose a title]</title>
  <!-- Using emoji as favicon -->
  <link rel="shortcut icon" href="data:image/svg+xml,<svg xmlns=%22http://www.w3.org/2000/svg%22 viewBox=%220 0 100 100%22><text y=%22.9em%22 font-size=%2290%22>[choose an emoji]</text></svg>" type="image/x-icon">
  <!-- Linking a font -->
  <link rel="preconnect" href="https://fonts.bunny.net">
  <link href="https://fonts.bunny.net/css?family=[choose a font]" rel="stylesheet" />
  <!-- Using a css variables library -->
  <link rel="stylesheet" href="https://unpkg.com/open-props">
  <link rel="stylesheet" href="https://unpkg.com/open-props/normalize.min.css"/>
  <!-- Linking our own css file(this is the file we created) -->
  <link rel="stylesheet" href="styles.css">
  <!-- For social sharing preview -->
  <meta property="og:type" content="website">
  <meta property="og:url" content="[domain of the site deployed(more in deployement section)]">
  <meta property="og:title" content="[choose a title]">
  <meta property="og:image:secure_url" content="[place an image in the root and put its link here]">
  <meta property="og:description" content="[choose a description]">
  <meta property="og:site_name" content="[choose a title]">
  <meta property="og:locale" content="en_US">
  <!-- For twitter sharing preview -->
  <meta name="twitter:card" content="summary">
  <meta name="twitter:site" content="[choose a twitter handle]">
  <meta name="twitter:creator" content="[choose a twitter handle]">
  <meta name="twitter:url" content="[domain of the deployed site]">
  <meta name="twitter:title" content="[choose a title]">
  <meta name="twitter:description" content="[choose a description]">
  <meta name="twitter:image" content="[place an image in the root and put its link here]">
</head>
<body>
  <main class="parent">
    <!-- THIS IS WHERE THE CONTENT WILL RESIDE -->
  </main>
  <!-- Linking our js file(optional)(this is the file we created) -->
  <script src="scripts.js"></script>
</body>
</html>
```

Add content to the page using semantic HTML elements. Read more [sematics in HTML](https://developer.mozilla.org/en-US/docs/Glossary/Semantics#semantics_in_html)Use `h1` tag for top level heading, and go up from there. Use `p` tag for long paragraphs. Using `section`, `article` and `form` whereever appropriate. Basically don't use `div` for everything.

# STEP 3: Install `browersync` to sync the browser to the latest code change on save(live preview)
1. Install browsersync: `npm install -g browser-sync`
2. Open a new terminal window/tab, navigate to the project root folder.
3. Run `browser-sync start --server --files "css/*.css"`
4. Open the URL to view your site.

* Keep this terminal window/tab open, and open the code editor

# STEP 4: Open `styles.css` and paste the code block below
```css
:root {
  /* ANY CUSTOM CSS VARIABLES USED THROUGH OUT THE PAGE */
  --content-font: '[choosen font in the link tag]', sans-serif;
}

body {
 /* ANY STYLES THAT IS USED THROUGHOUT THE PAGE */
 font-family: var(--content-font);
}

.parent {
  display: grid;
  grid-template-columns: 1fr min(80ch, calc(100% - 16px)) 1fr;
  grid-column-gap: 8px;
  place-items: center;
}

.parent > * {
  grid-column: 2;
}
```

The styles on the `.parent` class sets up a nice grid layout for mobile and desktop layouts.
Add background color, give color to various headings, setup proper font sizes and add all other fancy things to make your site your own. Go through [OPEN PROPS](https://open-props.style) website(the CSS variables library we are using to build this site) for inspiration.

> At this point you have fairly working website.

* Test your site in both OS dark theme and light theme.

TIPS:
1. Use the CSS `@media` rule with `prefers-color-scheme` property with `dark` and `light` values to target both the color schemes differently.
2. Use CSS logical properties as much as possible, to future proof your website.
3. Setup fluid typography so the text is readable on different screen sizes.
4. Don't forget to make images responsive.

# STEP 5: Adding `Javascript(optional)`
For a website that is just to convery something to an user, we don't really need javascript. Having said that if you need some form of updates to the content(for example count up to a target number as is implemented [here](https://bellaregrants.netlify.app/#remaining-funds) you will need to rely on javascript. Use javascript only if you need it.

# STEP 6: Change all the content as needed(stuff marked to be changed within [])
In the HTML code snippet, the meta tags and some other stuff are marked to be changed with `[]`, change them to fit the theme of the website.

# STEP 6: Deploying
I use [github](https://github.com) and [bitbucket](https://bitbucket.org) to keep my code. How to push your code to github and bitbucket will need to be a separate blog post(there are plenty of resources online). Once you have the code on the above platforms, get an account on [NETLIFY](https://netlify.app) and follow this [HOW TO DEPLOY A STATIC SITE ON NETLIFY](https://www.netlify.com/blog/2016/10/27/a-step-by-step-guide-deploying-a-static-site-or-single-page-app/) guide.

# STEP 7: Adding social preview image.
When websites are shared on twitter and other social media platforms, you can add an image to be show n. Choosing an image from [UNSPLASH](https://unsplash.com) is what i do most of the time. Once I download it, I use the [SQUOOSH APP](https://squoosh.app/) to compress the image. Once I have the compressed image, I bring down the size of the image to be 1050x600 pixels(WxH).

Now the image is ready and place it in the root of the project directory.

The image is supposed to be linked on the meta tags on the head section on the `index.html` file. If the image name is `og-image.jpg` and the site name on netlify is `supersite.netlify.app` then the url in the `og` meta tag should be `https://supersite.netlify.app/og-image.jpg`. Test if the images works by inputing the site domain in the input field on various social media sites/apps(it should show a preview).

> You now have a link that you can share with people, your own little corner on the internet. You can buy your own custom domain if you fancy, but it's going to cost you.
