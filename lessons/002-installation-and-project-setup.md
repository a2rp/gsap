# 002 - Installation and project setup

## Learning goals

- Install GSAP from npm in a module-based project.
- Import GSAP from the package and know when plugin registration is needed.

## Core idea

For modern projects, install the `gsap` package with the package manager already used by the application. Import GSAP from a JavaScript module. Keep package management and bundler setup aligned with the existing project rather than mixing CDN scripts and package imports.

## How it works

The starter below uses Vite to serve an ES module entry file and resolve the `gsap` dependency. The same import style is used by common bundlers. A plugin is a separate import and should be registered with `gsap.registerPlugin()` so bundlers retain it. GSAP 3.13 and newer publish the plugins on npm; older private-registry instructions can be stale.

``js
import { gsap } from "gsap";

const box = document.querySelector(".box");

gsap.to(box, { x: 100, duration: 0.6 });
``

Read the code from the target outward: identify the animated value, then the GSAP configuration that controls its start, destination, timing, or lifecycle. In DOM examples, make sure the selected elements exist before this module runs. In object examples, update the visible interface from the changing object value yourself.

## When to use it and its limits

Use npm installation when the application already has a build step, needs dependency version control, or imports code from modules. A CDN can be convenient for a disposable single-file demo, but choose one loading strategy for a project and follow its corresponding import pattern.

Installing GSAP does not configure a project that has no JavaScript module support. The version in the lockfile controls the version teammates and deployment builds install. For plugins, use import paths supported by the installed package version.

## Common mistakes

- Mixing `import { gsap } from "gsap"` with a separate global `gsap` script and accidentally creating two loading paths.
- Running npm commands from the wrong directory, so `package.json` is not the project's one.
- Forgetting to register an imported plugin.
- Copying an old private-registry `.npmrc` setup into a current project.

## Recap and practice

In a fresh Vite vanilla project, install GSAP, import it in `src/main.js`, and animate the demo box. Then add `ScrollTrigger` as an imported and registered plugin. Confirm the page still builds after restarting the dev server.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous lesson</th><th>Chapter Q&amp;A</th><th>Chapter example</th><th>Next lesson</th></tr></thead>
  <tbody><tr><td><a href="001-gsap-and-animation-fundamentals.md">001 - GSAP and animation fundamentals</a></td><td><a href="../qnas/002-installation-and-project-setup.md">Q&amp;A</a></td><td><a href="../examples/002-installation-and-project-setup.md">Example</a></td><td><a href="003-tweens-with-gsap-to.md">003 - Tweens with gsap.to()</a></td></tr></tbody>
</table>
