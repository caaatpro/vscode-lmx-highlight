VSCODE-LMX-HIGHLIGHT
===

[![License: MIT](https://img.shields.io/badge/License-MIT-brightgreen.svg)](https://opensource.org/licenses/MIT)

Special plugin for VS Code highlighting text in code

### Preview

- with `material night` color theme:
![](https://github.com/caaatpro/vscode-lmx-highlight/raw/master/assets/material-night.png)

- with `material night eighties` color theme:
![](https://github.com/caaatpro/vscode-lmx-highlight/raw/master/assets/material-night-eighties.png)

### Config

`lmx:`,`FIXME:` are built-in keywords. You can override the look by customizing the setting.

To customize the keywords and other stuff, <kbd>command</kbd> + <kbd>,</kbd> (Windows / Linux: File -> Preferences -> User Settings) open the vscode file `settings.json`.

| | type | default | description |
|---|---|---|---|
| lmxhighlight.isEnable | boolean | true | Toggle the highlight, default is true. |
| lmxhighlight.isCaseSensitive  | boolean | true | Whether the keywords are case sensitive or not. |
| lmxhighlight.keywords | array | N/A | An array of keywords that will be hilighted. You can also specify the style for each keywords here. See example below for more infomation. |
| lmxhighlight.keywordsPattern  | string | N/A | Specify keywords via RegExp instead of `lmxhighlight.keywords` one by one. NOTE that if this presents, `lmxhighlight.keywords` will be ignored. And REMEMBER to escapse the back slash if there's any in your regexp (using \\ instead of signle back slash). |
| lmxhighlight.defaultStyle | object | N/A | Specify the default style for custom keywords, if not specified, build in default style will be applied. [See all available properties on VSCode doc DecorationRenderOptions section](https://code.visualstudio.com/docs/extensionAPI/vscode-api) |
| lmxhighlight.include | array | [<br>`"**/*.js"`,<br>`"**/*.jsx"`,<br>`"**/*.ts"`,<br>`"**/*.tsx",`<br>`"**/*.html"`,<br>`"**/*.php"`,<br>`"**/*.css",`<br>`"**/*.scss"`<br>] | Glob patterns that defines the files to search for. Only include files you need, DO NOT USE `{**/*.*}` for both permormance and avoiding binary files reason. <br> For backwards compatability, a string combine all the patterns is also valid `"{**/*.js,**/*.jsx,**/*.ts,**/*.tsx,**/*.html,**/*.php,**/*.css,**/*.scss}"` |
| lmxhighlight.exclude | array | [<br>`"**/node_modules/**"`,<br>`"**/dist/**",`<br>`"**/bower_components/**"`,<br>`"**/build/**",`<br>`"**/.vscode/**"`,<br>`"**/.github/**"`,<br>`"**/_output/**"`,<br>`"**/*.min.*"`,<br>`"**/*.map"`<br>] | Glob pattern that defines files and folders to exclude while listing annotations. <br> For backwards compatability, a string combine all the patterns is also valid `"{**/node_modules/**,**/bower_components/**,**/dist/**,**/build/**,**/.vscode/**,**/_output/**,**/*.min.*,**/*.map}"` |
| lmxhighlight.maxFilesForSearch | number | 5120 | Max files for searching, mostly you don't need to configure this. |
| lmxhighlight.toggleURI | boolean | false | If the file path within the output channel not clickable, set this to true to toggle the path patten between `<path>#<line>` and `<path>:<line>:<column>`. |


an example of customizing configuration:

```js
{
    "lmxhighlight.isEnable": true,
    "lmxhighlight.isCaseSensitive": true,
    "lmxhighlight.keywords": [
        "DEBUG:",
        "REVIEW:",
        {
            "text": "NOTE:",
            "color": "#ff0000",
            "backgroundColor": "yellow",
            "overviewRulerColor": "grey"
        },
        {
            "text": "HACK:",
            "color": "#000",
            "isWholeLine": false,
        },
        {
            "text": "lmx:",
            "color": "red",
            "border": "1px solid red",
            "borderRadius": "2px", //NOTE: using borderRadius along with `border` or you will see nothing change
            "backgroundColor": "rgba(0,0,0,.2)",
            //other styling properties goes here ... 
        }
    ],
    "lmxhighlight.keywordsPattern": "lmx:|FIXME:|\\(([^)]+)\\)", //highlight `lmx:`,`FIXME:` or content between parentheses
    "lmxhighlight.defaultStyle": {
        "color": "red",
        "backgroundColor": "#ffab00",
        "overviewRulerColor": "#ffab00",
        "cursor": "pointer",
        "border": "1px solid #eee",
        "borderRadius": "2px",
        "isWholeLine": true,
        //other styling properties goes here ... 
    },
    "lmxhighlight.include": [
        "**/*.js",
        "**/*.jsx",
        "**/*.ts",
        "**/*.tsx",
        "**/*.html",
        "**/*.php",
        "**/*.css",
        "**/*.scss"
    ],
    "lmxhighlight.exclude": [
        "**/node_modules/**",
        "**/bower_components/**",
        "**/dist/**",
        "**/build/**",
        "**/.vscode/**",
        "**/.github/**",
        "**/_output/**",
        "**/*.min.*",
        "**/*.map",
        "**/.next/**"
    ],
    "lmxhighlight.maxFilesForSearch": 5120,
    "lmxhighlight.toggleURI": false
}
```

### Commands

This extension contributes the following commands to the Command palette.

- `Toggle highlight` : turn on/off the highlight
![](https://github.com/caaatpro/vscode-lmx-highlight/raw/master/assets/toggle-highlight.gif)
- `List highlighted annotations` : list annotations and reveal from corresponding file
![](https://github.com/caaatpro/vscode-lmx-highlight/raw/master/assets/list-annotations.gif)
