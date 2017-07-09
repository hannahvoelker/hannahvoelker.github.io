# noto-emoji-iconset

Iconset for [`iron-icon`](https://elements.polymer-project.org/elements/iron-icon) to use Google's Emojis. [See the Documentation](https://raulsntos.github.io/noto-emoji-iconset).

[See for yourself](https://raulsntos.github.io/noto-emoji-iconset/components/noto-emoji-iconset/demo).

<!---
```
<custom-element-demo>
  <template>
    <script>window.Polymer = {dom: 'shadow'};</script>
    <script src="../webcomponentsjs/webcomponents-lite.js"></script>
    <link rel="import" href="noto-emoji-iconset.html">
    <link rel="import" href="emoji-icon.html">
    <style is="custom-style">
      #container {
        display: flex;
        justify-content: space-between;
        padding: 10px;
      }
      
      iron-icon, emoji-icon {
        --iron-icon-width: 64px;
        --iron-icon-height: 64px;  
        --emoji-icon-width: 64px;
        --emoji-icon-height: 64px;
      }
    </style>
    <div id="container">
      <next-code-block></next-code-block>
    </div>
  </template>
</custom-element-demo>
```
-->
```html
<iron-icon icon="emoji:😆"></iron-icon>
<iron-icon icon="emoji:😛"></iron-icon>
<iron-icon icon="emoji:🎉"></iron-icon>
<emoji-icon emoji="dog"></emoji-icon>
<emoji-icon emoji="cat"></emoji-icon>
```

![Emojis](https://github.com/raulsntos/noto-emoji-iconset/raw/master/hero.png)

## How to install
You can clone this repo directly to your server but I recommend using bower:

`bower install --save raulsntos/noto-emoji-iconset`

## Important note
The emojis will not render properly if you don't use Shadow DOM so be sure to enable it.

**The good news:** Polymer will switch to Shadow DOM by default eventually (soon).

Take a look at the [demo](https://github.com/raulsntos/noto-emoji-iconset/blob/master/demo/index.html) to see how I'm using the iconset. Just be sure to add this code before loading Polymer (or every element implemented with Polymer):
```html
<script>
window.Polymer = {
  dom: 'shadow'
}
</script>
```

## How to use the set
To use the set simply import this set and use it like any other iconset. Use the prefix **emoji** followed by colon (**:**) and the emoji in unicode (`🎉`). Example:
```html
<html>
  <head>
    ...
    <link rel="import" href="bower_components/noto-emoji-iconset/noto-emoji-iconset.html">
    ...
  </head>
  <body>
    ...
      <iron-icon icon="emoji:🎉"></iron-icon>
    ...
  </body>
</html>
```

## But it's hard to type emojis in my laptop! :angry:
I know! That's why there's also a Polymer element included `emoji-icon` which lets you use the emoji shortname (like you do in GitHub). Example:
```html
<html>
  <head>
    ...
    <link rel="import" href="bower_components/noto-emoji-iconset/emoji-icon.html">
    ...
  </head>
  <body>
    ...
      <emoji-icon emoji="tada"></emoji-icon>
    ...
  </body>
</html>
```

### Nice features of `emoji-icon`
- You can use shortnames instead of typing the emoji (making it easier to use when you are not developing using your phone :wink:)
- The element uses a dictionary to translate emoji shortnames to unicode, the dictionary is stored in `emoji-dictionary.html`. The element imports the JSON variable **only once** since that's how the `<link rel="import">` tag works.

## Can I change the size?
Yes! If you are using `iron-icon`, see how to do it in their [documentation](https://elements.polymer-project.org/elements/iron-icon#styling). If you are using `emoji-icon` you can also find how in `iron-icon`'s documentation because it's the exactly the same but replacing `iron` with `emoji` in the CSS variables.

## How to build the iconset
### Requirements
- [Go](https://golang.org/)
- [Git](https://git-scm.com/)

### What it does
You can build the iconset yourself by using the build.go file included in this repository, simple use `go run build.go`.

The script uses `git` to clone the Noto GitHub repository (you can also download the repository manually, the script will not clone it as long as a folder named `noto-emoji` exists in the root of this project).

If you have already cloned or downloaded the Noto repository but want to update it to the latest version use the flag `-update-noto` when running the script: `go run build.go -update-noto` to overwrite the folder (or you can delete it manually and then run the script).

To overwrite the `emoji-dictionary.html` use the `-update-dictionary` flag, works the same way as the `-update-noto` flag.

The script will overwrite the `noto-emoji-iconset.html` and `emoji-dictionary.html` files without a warning.

### You might not want to build the element yourself, use the one downloaded by bower
It might take a few minutes since it has to download the entire Noto repository, go through over 800 svg images and then download and parse a JSON that contains over 1000 elements. Also, the script was not built to be fast, I implemented it quickly so there might be a few things that could've been done better, the purpose of the script is to automate the process of transforming the latest version of Google's Noto Emoji into a Polymer element, once the script has fullfilled its purpose there is no need for it anymore (until Google updates the Noto repository), so it's likely that no user will ever run the go script but me in order to update the element.

## Known issues
- I'm using the SVG icons provided by Google in the [Noto repository](https://github.com/googlei18n/noto-emoji) and they are currently outdated so there are a few missing emojis, when Google updates their repository I'll include the new emoji. If you want to know the state of this issue check the Noto repository issue ~~[#62](https://github.com/googlei18n/noto-emoji/issues/62)~~ (duplicate of [#30](https://github.com/googlei18n/noto-emoji/issues/30)).
- I would prefer to make `emoji-icon` extend from `iron-icon` instead of creating a new element with an `iron-icon` tag inside and redefining every CSS variable but Polymer does not seem to support extending custom elements yet. See issue [#2280](https://github.com/Polymer/polymer/issues/2280) in the Polymer repo.
