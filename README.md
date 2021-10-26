<p align="center"><img src="https://raw.githubusercontent.com/arcticicestudio/styleguide-javascript/main/assets/images/repository-hero.svg?sanitize=true"/></p>

<p align="center">JavaScript code style based on the <a href="https://github.com/airbnb/javascript" target="_blank">Airbnb JavaScript Style Guide</a>.</p>



Every major open source project has its own style guide, a set of standards and conventions for the writing and design of code, documentations and assets. It is much easier to understand a large codebase when all the code in it is in a consistent style.

A style guide establishes and enforces styles to improve the intelligibility and communication within the project community. It ensures consistency and enforces best practice in usage and language composition.

## Getting Started

The [project documentation][docs] contains chapters to learn about the [comprehensive base rule set][docs-r] including [ECMAScript +6 (ES 2015+)][docs-r-ecma6] and [React][docs-r-react] specific styles like e.g. [Higher-Order Components][docs-rules-react-hoc], the [component methods & properties ordering][docs-r-react-order#meth_props] and [props][docs-r-react-props].

### ESLint Configurations

To follow these rules in a project use the official extensible code linter configurations [@arcticicestudio/eslint-config-base][gh-t-pkg-esl-conf-base] for [ESLint][]. The advanced [@arcticicestudio/eslint-config][gh-t-pkg-esl-conf] package provides support for specific [React][] and [JSX A11Y][npm-eslint-plugin-jsx-a11y] rules as well as compatibility integrations for other projects like [Prettier][].

To lint projects build with [TypeScript][], the [@arcticicestudio/eslint-config-typescript][gh-t-pkg-esl-ts] package can be extended for full compatibility with the TypeScript compiler in combination with the powerful ESLint engine. It also allows to lint mixed projects consisting of both TypeScript and JavaScript sources.

## Contributing

Read the [contributing guide][gh-b-contrib] to learn about the development process and how to propose [enhancement suggestions][gh-b-contrib#enhance] and [report bugs][gh-b-contrib#bug], how to [submit pull requests][gh-b-contrib#pr] and the project‘s [style guides][gh-b-contrib#stgs], [branch organization][gh-b-contrib#vcs] and [versioning][gh-b-contrib#ver] model.

The guide also includes information about [minimal, complete, and verifiable examples][gh-b-contrib#mcve] and other ways to contribute to the project like [improving existing issues][gh-b-contrib#help_issues] and [giving feedback on issues and pull requests][gh-b-contrib#help_fb].

<p align="center"><img src="https://raw.githubusercontent.com/arcticicestudio/nord-docs/master/assets/images/nord/repository-footer-separator.svg?sanitize=true" /></p>

<p align="center">Copyright &copy; 2018-present <a href="https://www.arcticicestudio.com" target="_blank" rel="noreferrer">Arctic Ice Studio</a> and <a href="https://www.svengreb.de" target="_blank" rel="noreferrer">Sven Greb</a></p>

<p align="center"><a href="https://github.com/arcticicestudio/styleguide-javascript/blob/main/LICENSE" target="_blank" rel="noreferrer"><img src="https://img.shields.io/static/v1.svg?style=flat-square&label=License&message=MIT&logoColor=eceff4&logo=github&colorA=4c566a&colorB=88c0d0"/></a></p>

[docs-r-ecma6]: https://arcticicestudio.github.io/styleguide-javascript/rules/ecmascript_6+_styles.html
[docs-r-react-order#meth_props]: https://arcticicestudio.github.io/styleguide-javascript/rules/react/ordering.html#component-methods-and-properties
[docs-r-react-props]: https://arcticicestudio.github.io/styleguide-javascript/rules/react/props.html
[docs-r-react]: https://arcticicestudio.github.io/styleguide-javascript/rules/react/index.html
[docs-r]: https://arcticicestudio.github.io/styleguide-javascript/rules/index.html
[docs-rules-react-hoc]: https://arcticicestudio.github.io/styleguide-javascript/rules/react/higher_order_components.html
[docs]: https://arcticicestudio.github.io/styleguide-javascript
[eslint]: https://eslint.org
[gh-b-contrib]: https://github.com/arcticicestudio/styleguide-javascript/blob/main/CONTRIBUTING.md
[gh-b-contrib#bug]: https://github.com/arcticicestudio/styleguide-javascript/blob/main/CONTRIBUTING.md#bug-reports
[gh-b-contrib#enhance]: https://github.com/arcticicestudio/styleguide-javascript/blob/main/CONTRIBUTING.md#enhancement-suggestions
[gh-b-contrib#help_fb]: https://github.com/arcticicestudio/styleguide-javascript/blob/main/CONTRIBUTING.md#give-feedback-on-issues-and-pull-requests
[gh-b-contrib#help_issues]: https://github.com/arcticicestudio/styleguide-javascript/blob/main/CONTRIBUTING.md#improve-issues
[gh-b-contrib#mcve]: https://github.com/arcticicestudio/styleguide-javascript/blob/main/CONTRIBUTING.md#mcve
[gh-b-contrib#pr]: https://github.com/arcticicestudio/styleguide-javascript/blob/main/CONTRIBUTING.md#pull-requests
[gh-b-contrib#stgs]: https://github.com/arcticicestudio/styleguide-javascript/blob/main/CONTRIBUTING.md#style-guides
[gh-b-contrib#vcs]: https://github.com/arcticicestudio/styleguide-javascript/blob/main/CONTRIBUTING.md#branch-organization
[gh-b-contrib#ver]: https://github.com/arcticicestudio/styleguide-javascript/blob/main/CONTRIBUTING.md#versioning
[gh-t-pkg-esl-conf-base]: https://github.com/arcticicestudio/styleguide-javascript/tree/main/packages/@arcticicestudio/eslint-config-base
[gh-t-pkg-esl-conf]: https://github.com/arcticicestudio/styleguide-javascript/tree/main/packages/@arcticicestudio/eslint-config
[gh-t-pkg-esl-ts]: https://github.com/arcticicestudio/styleguide-javascript/tree/main/packages/@arcticicestudio/eslint-config-typescript
[npm-eslint-plugin-jsx-a11y]: https://www.npmjs.com/package/eslint-plugin-jsx-a11y
[prettier]: https://prettier.io
[react]: https://reactjs.org
[typescript]: https://www.typescriptlang.org
