# Contributing to `yaml`

The YAML spec is somewhat complicated, and `yaml` tries its best to make it as easy as possible to work with it. The primary goal of this project is to make YAML as pleasant as possible to work with. To that end, the order of priorities is:

1. **Maintain compatibility**. There exists a number of YAML libraries written in and for various languages, based on various versions of the specification. This library currently passes more of the [YAML Test Matrix](https://matrix.yaml.io/) than any other, and it should be kept that way.

2. **Support all YAML features**. Everything that you might want to do with YAML should be possible with `yaml`. In a somewhat perverse way, this means that we need to break the spec a bit in order to allow working with comments. This also means that we want to simultaneously maintain compatibility with multiple versions of the spec, in particular the most widely used 1.1 and 1.2.

3. **Keep it simple**. Extending the library needs to be done carefully, and keep in all of its users. Different applications have different needs and so are provided with different APIs. In particular, custom tags are supported, but aren't part of the built-in schemas. Reading or writing external files or URLs is rather explicitly left out of the core functionality for security reasons.

## Getting Started

To start hacking `yaml`, this should get you set up:

```sh
git clone https://github.com/eemeli/yaml.git # or your own fork
cd yaml
git submodule update --init # required by tests
npm install
npm test # just to be sure
```

## Repository Directory & File Structure

- **`browser/`** - Browser-optimised build of the library, which should work in IE 11 & later. Used automatically by e.g. Webpack & Rollup via the `"browser"` value in `package.json`. A corresponding minimal set of the library's required polyfills is available at `playground/src/polyfill.js`
- **`dist/`** - Node-optimised build of the library, which should work in Node.js 6.0.0 and later without polyfills.
- **`docs/`** - Source files for the library's [documentation site](https://eemeli.org/yaml). Maintained as a git submodule to allow merges from its upstream source, [Slate](https://lord.github.io/slate). See its [`README`](./docs/README.md) for installation instructions. Note that the build target is the `gh-pages` branch of _this_ repo.
- **`playground/`** - Source files for a browser-based [playground](https://eemeli.org/yaml-playground/) using this library. Also contains the Selenium browser tests for the library. Maintained as a git submodule to allow for easier publication.
- **`src/`** - Source files for the library.
- **`tests/`** - Tests for the library. `tests/yaml-test-suite` is a git submodule of a custom fork of the [YAML Test Suite](https://github.com/yaml/yaml-test-suite)
- **`types/`** - Part of the library's published API; various types included in the YAML 1.1 types, but not in the default YAML 1.2 schemas.
-  **`{map,pair,parse-cst,scalar,schema,seq}.js`** - Part of the library's published API; see the documentation site for more details. Not transpiled, so use CommonJS `require()` for imports.

## Contributing Code

First of all, make sure that all the tests pass, and that you've added test cases covering your changes. Our set of test suites is rather extensive, and is a significant help in making sure no regressions are introduced. Note that the CI environment runs tests in e.g. Node.js 6.0 and IE 11, so using new language features may require extending the minimal set of [polyfills](./playground/src/polyfill.js)

If you're intending to contribute to the upstream repo, please make sure that your code style matches the Prettier and ESLint rules. The easiest way to do that is to configure your editor to do that for you, but `lint` and `prettier` npm scripts are also provided.
