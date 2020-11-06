# fk-sass
Fictive Kin starter Sass package.

## usage

There are two ways to use fk-sass. 1) Through npm, where project specific styles extend the base package or 2) download and copy directly to your project.

### Download and copy

Download this repo and copy the `scss` directory into your project. Your sass compile step should include that directory as a load-path so that the `@use` and `@forward` statements work as expected.

And example compile script would look like:

```
sass scss:css --source-map --load-path=scss
```

### Through NPM

Run the following in your project directory to install:

```
yarn add @fictivekin/fk-sass --dev
```

Copy the `example-project` directory from this repo into your project where sass files will live.

Add this new directory and the `node_modules` fk-sass directory to your sass compile script. Here is an example compile script:

```
sass scss:css --source-map --load-path=scss --load-path=node_modules/@fictivekin/fk-sass/scss
```

With this setup, the project sass files are setup to either overwrite the fk-sass files, fall-back to the fk-sass files, or be a supplement to the fk-sass files.

This allows you to create prooject specific styles without altering the base package.

Note that there are examples of how this plays out practically in the `example-project` directory. Several modules have `_settings.scss` files that are intended to give you control over the look of modules without having to rewrite or copy the base styles.

## Things to know

### Assets

There is a css url helper available. Add it for use in your sass partial with:

```
@use 'lib/assets';
```

or

```
@use 'lib/assets' as *;
```

It is also included in the config collection, which you can use with:

```
@use 'config' as *;
```

`config/_assets.scss` has a good example of how `http-url`, `font-url`, and `image-url` are used. This file also lets you set where these asset directories are located. **Remember:** create a `config/_assets.scss` file in your project sass files to overwrite the directories that are set in the base package.

Buildstamps can also be an important part of asset linking. To utilize this, your build/deploy process should add a `_buildstamp.scss` file in your sass directory where a `$BUILDSTAMP` variable is set (to whatever naming convention you use for this purpose).

### Configuration and Custom Properties

The `config` and `_1_base/properties` directories seem to accomplish similar tasks — they both contain files that control settings that can affect a lot of your project.

All files in the number folders — `_1_base`, `_2_layout`, etc. — write out actual CSS styles. All files in `config` and `lib` do not write out CSS, and are designed for use as helpers in other files.

This is why custom properties are set in `_1_base`, but sass variables are set in `config`. You'll want to visit both sets of files to prepare your project's setup.

### Grid

At this time, there is no all-encompasing grid system included with fk-sass. The growing prevelence of CSS grid means it is often simpler (with less unused CSS) to define the grid within specific modules where it is used.

This is something we'll evaluate with use.
