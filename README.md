# Selenium IDE &middot; [![Build Status](https://api.travis-ci.com/SeleniumHQ/selenium-ide.svg?branch=trunk)](https://travis-ci.com/SeleniumHQ/selenium-ide)

![logo](https://www.seleniumhq.org/selenium-ide/img/selenium-ide128.png)

_An integrated development environment for Selenium scripts_

Selenium IDE is an Electron application written to enable recording and playback of Selenium scripts.

## Installation

Installation can be performed in a variety of ways:

1. Prepackaged binaries will be able to be installed directly. (Okay, not yet, but very soon.)
2. The application can be built manually using the below instructions.

### Prepackaged

No binaries are available currently, as we are in the process of obtaining signing certificates.
Sorry, my bad.

### Building Manually

To build manually, you must have the below prerequisites installed and follow the steps afterward.

#### Prerequisites

- [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- [NodeJS v16](https://nodejs.org/en/download/)
- [Pnpm](https://pnpm.io/installation)

#### Building

1. `git clone https://github.com/SeleniumHQ/selenium-ide` – Clone the IDE repo
2. `cd selenium-ide` – Navigate into the IDE folder
3. `pnpm -r i` – Install dependencies
4. `pnpm run build` – Build the app
5. `pnpm run start` – Run the app

## What now?

Here's a draft of the general tasks ahead. Feel free to pitch in and announce which you wish to take upon yourself:

- Selectors accuracy - an option is ranking selectors - we can optimize selectors correctness and test stability by collecting as many attributes as we can per user event. The most likely properties will be used for the selectors, with fallback to the others.
- Intelligent editing.
- Export to Selenium code in different languages.

## Contributing

If you'd like to contribute to the codebase, start by building manually using the above commands. The below tips are meant to assist you as well.

- If you'd like to iterate more quickly, `yarn watch` will facilitate near-realtime rebuilding for rapid iteration. (make change -> `yarn start` -> test change)
- To activate the devtools on an page, `CommandOrControl+F12` or `CommandOrControl+Option+I` will open the devtools. For your convenience, the [React Developer Tools](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en) are pre-installed in the Electron environment.
- VSCode has a defined workspace structure and run command, as well as file mappings to allow for breakpoints to work across sourcemaps for the main process.
- The Chrome dev tools are available at `localhost:8315` to use if the inline dev tools are not enough, though I'd highly advocate for the in-window dev tools, since they have the React Developer Tools installed as well.

## Questions or want to chat?

If you have questions, check out [our FAQ](https://github.com/SeleniumHQ/selenium-ide/wiki/Frequently-Asked-Questions).

You can also find us on the [#selenium](irc://freenode.net/selenium) IRC
channel, which is also available on
[Slack](https://www.selenium.dev/support/#ChatRoom).

## Architecture

The codebase is Javascript and relies heavily on the NodeJS, Electron, and
React ecosystem. This is a collection of packages arranged in a monorepo
config. Excepting the code-export packages, which are fully untyped, these
packages are fully typed using Typescript.

### Packages

These are the main packages. They're used to run the thing:

- selenium-ide: Main Electron app. Built with Webpack, React frontend. Communicates
via the IPC protocols.

- side-runner: NodeJS Task Runner. Built with Typescript.

- side-cli: Experimental CLI using React and Ink.

- side-runtime: Playback system wrapper. Takes side files and executes
them. Used by both selenium-ide and side-runner.

- side-api: This is the API shape of selenium-ide. This is intended to be used
to help share the API types with plugins in a lower footprint way.

- side-model: This is used to provide metadata around the standard commands and
argument types.

- side-commons: This is like the typical utils/helpers folder, except meant to
be shared across packages instead of just folders.

- side-code-export: NodeJS transpiler for .side files. Used to export to other
languages (C#, Java, Javascript, Python, Ruby).

- code-export-*: Code export format for various languages.
