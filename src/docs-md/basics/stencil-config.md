# Stencil Config

The `stencil.config.js` file is where all Stencil configuration happens.

Here's an example configuration:

```
exports.config = {
  serviceWorker: {
    globPatterns: [
      '**/*.{js,css,json,html,ico,png,jpeg}'
    ],
    globIgnores: [
      'build/app/svg/*.js'
    ]
  },
  copy: [
    { src: 'images' },
    { src: 'styles', dest: 'css' }
  ]
};
```

### Config entries

- `bundles`

The `bundles` config is an array of objects that represent how components are grouped together in lazy-loaded bundles. This config is rarely needed as Stencil handles this automatically behind the scenes.

- `collections`

The `collections` config specifies a list of third-party Stencil libraries. This config is rarely needed as Stencil handled this automatically behind the scenes.

- `srcDir`,  default value: `src`

The `srcDir` config specifies the source directory.

- `wwwDir`,  default value: `www`

The `wwwDir` config specifies the public web distribution directory. This directory is commonly the root directory for a server, where all static files can be served. This directory is built and rebuilt directly from the source files. We recommend this directory is not committed to a repository.

- `buildDir`,  default value: `build`

The `buildDir` config specifies where stencil's build files are saved after each build. These are the generated scripts which will be requested by the browser. The build directory should be relative to the `wwwDir` setting.

- `publicPath`, default value: `/build`

The `publicPath` config sets the fallback client-side base path for all Stencil build assets. By default the loader script will automatically figure out the relative path to load your components, but uses `publicPath` as a fallback. It's recommended to have it start with `/`. Note that this only sets the base path the browser requests, but this does not set where files are saved during build. To change where files are saved at build time, use the `buildDir` config. You can also use the publicPath from in your components logic. This can be helpful when loading files into a component from JavaScript. Here is an example of this:

```
...
export class SamplePage {
  @Prop({ context: 'publicPath'}) private publicPath: string;

 loadImage() {
   fetch(`${this.publicPath}/assets/my-image.svg`).then(res => {
     return res.text()
   }).then(svg => {
     console.log(svg)
   })
 }
}
```

- `serviceWorker`

The `serviceWorker` config lets you customize the service worker that gets automatically generated by the Stencil compiler. You can
set any of the values listed [here in the Workbox documentation](https://workboxjs.org/reference-docs/latest/module-workbox-build.html#.Configuration), to override our default service worker settings.

-  `copy`

The `copy` config is an array of objects that define any files or folders that you would like to
get copied over to your `buildDir` when a build is performed. Each object in the array must include a `src` property which can be either an `absolute path`, a `relative path` or a `glob pattern`. You can also provide the optional `dest` property which can be either an `absolute path` or a path `relative` to your `buildDir`.

- `plugins`

The `plugins` config can be used to add your own [rollup](https://rollupjs.org) plugins. For example, to add the `@stencil/sass` plugin you would add `const sass = require('@stencil/sass');` to the top of the `stencil.config` file and then add `sass()` to the `plugins` array in your config file.

<stencil-route-link url="/docs/testing" router="#router" custom="true">
  <button class="backButton">
    Back
  </button>
</stencil-route-link>

<stencil-route-link url="/docs/prerendering" custom="true">
  <button class="nextButton">
    Next
  </button>
</stencil-route-link>