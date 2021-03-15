# routify-starter

Starter template for [Routify](https://github.com/sveltech/routify).

### Get started

#### Starter templates
| Template                                  | Description                                                 |
|-------------------------------------------|-------------------------------------------------------------|
| [master](https://example.routify.dev/)    | Default template, includes examples folder                  |
| [blog](https://blog-example.routify.dev/) | Generates a blog from local markdown posts. Includes mdsvex |
| [auth](https://auth-example.routify.dev/) | Embedded login on protected pages. Includes Auth0           |

To use a template, run:

`npx @sveltech/routify init`

or

`npx @sveltech/routify init --branch <branch-name>`

The above commands will populate the current directory, they don't create a new one.

### npm scripts

| Syntax           | Description                                                                       |
|------------------|-----------------------------------------------------------------------------------|
| `dev`            | Development (port 5000)                                                           |
| `dev:nollup`     | Development with crazy fast rebuilds (port 5000)                                  |
| `dev-dynamic`    | Development with dynamic imports                                                  |
| `build`          | Build a bundled app with SSR + prerendering and dynamic imports                   |
| `serve`          | Run after a build to preview. Serves SPA on 5000 and SSR on 5005                  |
| `deploy:*`       | Deploy to netlify or now                                                          |
| `export`         | Create static pages from content in dist folder (used by `npm run build`)         |

### SSR and pre-rendering

SSR and pre-rendering are included in the default build process.

`npm run deploy:(now|netlify)` will deploy the app with SSR and prerendering included.

To render async data, call the `$ready()` helper whenever your data is ready.

If $ready() is present, rendering will be delayed till the function has been called.

Otherwise it will be rendered instantly.

See [src/pages/example/api/[showId].svelte](https://github.com/sveltech/routify-starter/blob/master/src/pages/example/api/%5BshowId%5D.svelte) for an example.

### Production

* For SPA or SSR apps please make sure that url rewrite is enabled on the server.
* For SPA redirect to `__app.html`.
* For SSR redirect to the lambda function or express server.

### Typescript

For Typescript, we recommend [@lamualfa](https://github.com/lamualfa) excellent [routify-ts](https://github.com/lamualfa/routify-ts/)

New project: `npx routify-ts init <project-name> [routify-init-args]`

Existing project: `npx routify-ts convert [project-directory]`


### Issues?

File on Github! See https://github.com/sveltech/routify/issues .

# SMELTE
## 介绍
Smelte是一个 使用Material Design规范在Svelte和Tailwind CSS之上构建的UI框架 .它带有许多组件和实用程序功能，可以轻松构建漂亮的响应式布局，同时还要确保捆绑包的大小和性能，这一切都要归功于Svelte。

## 安装
```node
npm install smelte or yarn add smelte
```

## 在rollup打包器下的配置
Then add the Smelte Rollup plugin (after svelte but before css)
```js
// rollup.config.js
const smelte=require("smelte/rollup-plugin-smelte");

plugins=[ 
  ...your plugins, 
  smelte({ 
    purge: production,
    output: "public/global.css", // it defaults to static/global.css which is probably what you expect in Sapper 
    postcss: [], // Your PostCSS plugins
    whitelist: [], // Array of classnames whitelisted from purging
    whitelistPatterns: [], // Same as above, but list of regexes
    tailwind: { 
      colors: { 
        primary: "#b027b0",
        secondary: "#009688",
        error: "#f44336",
        success: "#4caf50",
        alert: "#ff9800",
        blue: "#2196f3",
        dark: "#212121" 
      }, // Object of colors to generate a palette from, and then all the utility classes
      darkMode: true, 
    }, 
    // Any other props will be applied on top of default Smelte tailwind.config.js
  }),
]
```

## 引入Css样式
Then you should add Tailwind utilites CSS in your app component.
```js
import "smelte/src/tailwind.css" ;
```

例如: 在App.svelte文件下进行样式引入
``` svelte
// App.svelte
<script>
  import { Router } from "@roxi/routify";
  import { routes } from "../.routify/routes";
</script>

<style  global>
  @import "../assets/global.css";
  @import "smelte/src/tailwind.css" ;
</style>

<Router {routes} />
```
只有上面是不够的,新建一个windcss.css,里面放编译过的tailwindcss的样式,需要这样手动引入,不然识别不出tailwindcss
而后在global.css中引入也行,在index.html中进行引入也行

## 报错
当上面的文件都准备好的时候,可以进行npm run dev进行页面调试,此时页面报错,进行以下插件安装
``` node
npm install svelte-waypoint
```

## 组件内容进行控件引入
当smelte的环境以及样式都引入成功之后,我们可以在我们的页面进行smelte的控件引入,例如:
``` svelte
// example的index.svelte页面

<script>
  import { TextField } from "smelte";
</script>
<style>
</style>


<div style="width: 100%; text-align: center; margin-top: 4rem;">
  <TextField label="Test label" />
</div>

```

