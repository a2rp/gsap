# 002 - Installation and project setup Q&A

## What is the basic npm install command?

Run `npm install gsap` from the project directory that contains its `package.json`. This adds the package to the project dependencies and updates the lockfile.

## Do I need to import GSAP in every file?

A module that directly uses GSAP must import it, unless your own project has a shared module that re-exports the API. Prefer an explicit shared module over an implicit global.

## How do I use a plugin with a bundler?

Import the plugin from its package subpath, then call `gsap.registerPlugin(PluginName)`. Registration makes the dependency explicit and helps prevent tree-shaking from removing plugin code.

## Can I use a CDN instead of npm?

Yes, for a simple browser demo, but follow the CDN script-loading pattern and do not also import the same library through a bundler. Pick one approach per app.

## Why does my dependency work locally but fail in deployment?

Check that the package is declared in `package.json`, the lockfile is committed, the build uses a compatible Node version, and plugin imports match the installed GSAP version.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous Q&amp;A</th><th>Chapter lesson</th><th>Chapter example</th><th>Next Q&amp;A</th></tr></thead>
  <tbody><tr><td><a href="001-gsap-and-animation-fundamentals.md">001 - GSAP and animation fundamentals Q&amp;A</a></td><td><a href="../lessons/002-installation-and-project-setup.md">Lesson</a></td><td><a href="../examples/002-installation-and-project-setup.md">Example</a></td><td><a href="003-tweens-with-gsap-to.md">003 - Tweens with gsap.to() Q&amp;A</a></td></tr></tbody>
</table>
