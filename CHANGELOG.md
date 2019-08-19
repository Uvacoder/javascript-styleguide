<p align="center"><img src="https://raw.githubusercontent.com/arcticicestudio/styleguide-javascript/develop/assets/images/repository-hero.svg?sanitize=true"/></p>

<p align="center"><a href="https://github.com/arcticicestudio/styleguide-javascript/releases/latest" target="_blank"><img src="https://img.shields.io/github/release/arcticicestudio/styleguide-javascript.svg?style=flat-square&label=Release&logo=github&logoColor=eceff4&colorA=4c566a&colorB=88c0d0"/></a> <a href="https://arcticicestudio.github.io/styleguide-javascript" target="_blank"><img src="https://img.shields.io/github/release/arcticicestudio/styleguide-javascript.svg?style=flat-square&label=Docs&logo=read-the-docs&logoColor=eceff4&colorA=4c566a&colorB=88c0d0"/></a></p>

<p align="center">Changelog for the official <a href="https://github.com/arcticicestudio/styleguide-javascript" target="_blank">Arctic Ice Studio JavaScript Code Style</a></p>

<!--lint disable no-duplicate-headings no-duplicate-headings-in-section-->

# 0.7.0

![Release Date: 2019-08-19](https://img.shields.io/static/v1.svg?style=flat-square&label=Release%20Date&message=2019-08-19&colorA=4c566a&colorB=88c0d0) [![Project Board](https://img.shields.io/static/v1.svg?style=flat-square&label=Project%20Board&message=0.7.0&logo=github&logoColor=eceff4&colorA=4c566a&colorB=88c0d0)](https://github.com/arcticicestudio/styleguide-javascript/projects/3) [![Milestone](https://img.shields.io/static/v1.svg?style=flat-square&label=Milestone&message=0.7.0&logo=github&logoColor=eceff4&colorA=4c566a&colorB=88c0d0)](https://github.com/arcticicestudio/styleguide-javascript/milestone/2)

## Epics

**Monorepo with ESLint packages** — #8 ⇄ #16 (⊶ ac611f7e)
↠ Resolved the epic by converting the repository into a [monorepo][trbdev-monorepo] and migrating the [`@arcticicestudio/eslint-config`][gh-t-pkg-esl] (previously `eslint-config-arcticicestudio`) + [`@arcticicestudio/eslint-config-base`][gh-t-pkg-esl-base] (previously `eslint-config-arcticicestudio-base`) packages!

#### Previous Project State

Previously this repository only contained the actual styleguide documentation while specific projects that implement the guidelines for linters and code style analyzer lived in separate repositories. This was the best approach for modularity and a small and clear code base, but it increased the maintenance overhead by 1(n) since changes to the development workflow or toolbox, general project documentations as well as dependency management required changes in every repository with dedicated tickets/issues and PRs. In particular, Node packages require frequent dependency management due to their fast development cycles to keep up-to-date with the latest package changes like (security) bug fixes.

This styleguide is currently implemented by the [`@arcticicestudio/eslint-config`][gh-t-pkg-esl] (previously `eslint-config-arcticicestudio`) and [`@arcticicestudio/eslint-config-base`][gh-t-pkg-esl-base] (previously `eslint-config-arcticicestudio-base`) Node packages that lived in their own repositories. The development workflow was clean using most of GitHub's awesome features like project boards, _codeowner_ assignments, issue & PR automation and so on, but changes to one of them often required actions for the other package too since they are based on each other and they are using the same development tooling and documentation standards.

##### Monorepo Comparison

Actually I'm not a supporter when it comes to [monorepos][trbdev-monorepo] and next to the advantages a monorepo also comes with disadvantages:

- **No more scoped code** — The developer experience with Git is clearly worse because commits can contains changes to multiple scopes of the code. Since there are only a “transparent separation” of code, that was previously located in a dedicated repository but is not aggregated into a parent (e.g. `packages`) with other modules, commits can now contain changes to multiple code scopes spread over the entire code base.
- **No more assignment of commits to single modules** — Like described in the bullet point above, commit can contain changes to multiple modules, it is harder to detect which commit targeted a specific module.
- **Steeper learning curve for new contributors** — In a dedicated repository that only hosts a specific module it is easier for new developers to contribute to the project, but in a monorepo they might need to change code in multiple places within other modules or the root code/documentation of the entire project.
- **Uniform version number** — In order to keep conform to [SemVer][], the entire project must use a uniform version number. This means that a module that has not been changed since the last version must also be incremented in order to keep compatible with the other modules.
  Using different version numbers prefixed/suffixed with an individual version number **is a not go**, **increases the maintenance overhead** and **and drastically reduces the project overview and quality**! This would result in multiple Git tags on the `master` branch as well as “empty” changelogs and release notes with placeholder logs that only refer to changes of other modules.

#### Project Future

Even though there are disadvantages (see above), a [monorepo][trbdev-monorepo] makes sense **only for specific project modules thar are slightly coupled** and where using dedicated repositories only increases the maintenance overhead **when changes must be reflected in multiple modules anyway**.

In order to reduce the maintenance overhead both Node packages, [`@arcticicestudio/eslint-config`][gh-t-pkg-esl] (previously `eslint-config-arcticicestudio`) and [`@arcticicestudio/eslint-config-base`][gh-t-pkg-esl-base] (previously `eslint-config-arcticicestudio-base`), have been migrated into this repository by adapting to [Yarn workspaces][yarn-d-ws] since they are slightly dependent on each other anyway. This simplifies the development tooling setup and allows to use a unified documentation base as well as a smoother development and testing workflow.

This change also implies that the root of the repository is now the main package for the entire project setup including shared development dependencies, tools and documentations while the packages only contains specific configurations and (dev)dependencies.

##### Scoped Packages

The previous `eslint-config-arcticicestudio` and `eslint-config-arcticicestudio-base` packages were no [scoped packages][npm-d-scope] but suffixed with `-arcticicestudio*`. To simplify the naming and improving the usage of user/organization specific packages both packages are now scoped to `@arcticicestudio` resulting in the new names `@arcticicestudio/eslint-config-base` and `@arcticicestudio/eslint-config`. They can be used through [ESLint's support for shared configuration with scoped packages][esl-d-dev-share_conf#scope].
The previously released public versions [have been deprecated using the `npm deprecate` command][npm-cli-dep] where the provided message points out to migrate to the new scoped packages.

##### Versioning

The style guide itself and all packages using a shared/fixed/locked version. This helps all packages to keep in sync and ensure the compatibility with the latest style guide version.

##### Standard Setup

In order to keep up-to-date with the latest project setup for all _Arctic Ice Studio_ projects, the tools and documentations have been integrated and updated through the following tickets:

- #9 (⊶ 8e992407) „Git ignore and attribute pattern“ — completed ✓
- #10 (⊶ db2a43bc) „Git mail mapping“ — completed ✓
- #11 (⊶ 10253246) „Prettier“ — completed ✓
- #12 (⊶ c21a58a9) „lint-staged“ — completed ✓
- #13 (⊶ b4cac34f) „Husky“ — completed ✓
- #14 (⊶ be122b12) „General repository and package documentations and metadata“ — completed ✓
- #15 (⊶ c25d1efe) „GitHub issue and pull request templates“ — completed ✓

## Features

**GitHub issue and pull request templates** — #15 (⊶ c25d1efe)
↠ Integrated GitHub's feature to define [multiple issue templates][gh-blog-multi-issue-templ] while the [initial template file][gh-blog-intro-issue-templ] is used as a fallback/generic template to link to the specific ones.

<p align="center"><img src="https://user-images.githubusercontent.com/7836623/63289697-fff06f00-c2bf-11e9-9e33-f11870d7c2f2.png" width="250" /></p>

<p align="center"><img src="https://user-images.githubusercontent.com/7836623/63289698-00890580-c2c0-11e9-8873-e36a32a4164d.png" width="250" /></p>

Read the [GitHub Help article][gh-help-issue-templ] for more details about issue and pull request templates. Also check out how to manually create [issue templates][gh-help-pr-templ], a [pull request template][gh-help-issue-templ-repo]. and the guide on [how to create the (deprecated) fallback/generic issue template][gh-help-issue-templ-depr].

## Improvements

**General repository and package documentations and metadata** — #14 (⊶ be122b12)
↠ The previous project repository documentations were not designed for a [monorepo][trbdev-monorepo] layout and have been be updated including various badges provided by the great [shields.io][] project.

Further documentations about the project architecture and technologies as well as guides for contributions to develop, run and maintain the project stayed within the packages itself.
There are also various places that contained outdated documentations and metadata that have been updated too.

See #14 for more details about what exactly has been updated.

## Tasks

<p align="center"><img src="https://raw.githubusercontent.com/remarkjs/remark-lint/02295bc/logo.svg?sanitize=true" width="100" /></p>

**Introducing _remark-lint_** — #5 ⇄ #6 (⊶ fa9af093)
↠ Integrated [remark-lint][gh-remark-lint], a linter built on [remark][], the powerful Markdown processor powered by plugins such as remark-lint.
It is used through [remark-cli][gh-remark-cli] with [remark-preset-lint-arcticicestudio][gh-remark-preset-lint-arcticicestudio], the custom preset that implements the [Arctic ice Studio Markdown Style Guide][styleguide-markdown].

To lint all Markdown sources within the project the `lint:md` NPM script has been added that will be picked up by the main `lint` script.

<p align="center"><img src="https://user-images.githubusercontent.com/7836623/63288499-2365ea80-c2bd-11e9-92bf-637e2e3646c1.png" width="400" /></p>

**Documentation for official ESLint extensible shared configurations** — #7 (⊶ 57b8ce03)
↠ Added information about the official [`@arcticicestudio/eslint-config`][gh-t-pkg-esl] and [`@arcticicestudio/eslint-config-base`][gh-t-pkg-esl-base] extensible shared configurations for [ESLint][] to the documentation.

<p align="center"><img src="https://upload.wikimedia.org/wikipedia/commons/e/e0/Git-logo.svg" width="100" /></p>

**Git ignore and attribute pattern** — #9 (⊶ 8e992407)
↠ Added the [`.gitattributes`][git-d-gitattributes] and [`.gitignore`][git-d-gitignore] configuration files to define the pattern.

**Git mail mapping** — #10 (⊶ db2a43bc)
↠ Added a Git [mailmap][git-d-mailmap] file to link to in documentations and allow contributors to send mails regarding security issues. This prevents unnecessary overhead of updating all documents when new core team and members and contributors are added and additionally adds the main functionality of the file: Mapping commits when someone uses a different email address.

<p align="center"><img src="https://user-images.githubusercontent.com/7836623/63289154-b2273700-c2be-11e9-9adb-11576dd9ff5a.png" width="100" /></p>

**Introducing _Prettier_** — #11 (⊶ 10253246)
↠ Integrated [Prettier][], the opinionated code formatter with support for many languages and integrations with most editors. It ensures that all outputted code conforms to a consistent style and provides the best and recommended style configurations of-out-the-box™.
Read #11 for more details about the configuration and setup as well as included plugins.

To format all compatible sources within the project the `format:pretty` NPM script has been added that will be picked up by the main `format` script.

<p align="center"><img src="https://user-images.githubusercontent.com/7836623/63289152-b2273700-c2be-11e9-870f-2d43d700886d.png" width="100" /></p>

**Introducing _lint-staged_** — #12 (⊶ c21a58a9)
↠ Integrated [lint-staged][gh-lint-staged] to run linters against staged Git files and prevent adding code that violates any style guide into the code base.

Read #12 for more details about the configuration and setup.

<p align="center"><img src="https://user-images.githubusercontent.com/7836623/63289221-e13da880-c2be-11e9-837d-38fd2657df6a.png" width="100" /></p>

**Introducing _Husky_** — #13 (⊶ b4cac34f)
↠ Integrated [Husky][gh-husky], the tool that make Git hooks easy and can prevent bad Git commits, pushes and more _woof_!

Read #13 for more details about the configuration and setup.

# 0.6.0

![Release Date: none](https://img.shields.io/static/v1.svg?style=flat-square&label=Release%20Date&message=-&colorA=4c566a&colorB=88c0d0) ![Milestone](https://img.shields.io/static/v1.svg?style=flat-square&label=Milestone&message=0.6.0&logo=github&logoColor=eceff4&colorA=4c566a&colorB=88c0d0)

↳ Release date of transferred `eslint-config-base` package: _2019-08-14_

## Features

### Style Guide

**Suggestion to use `WeakMap` for hidden properties** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Ported from airbnb/javascript#1722 (⊶ airbnb/javascript@c5411a42)
↠ Added a suggestion to the examples of the [naming conventions for underscores][docs-r-name_conv#undsc] to make properties hidden by using a `WeakMap` when the environment supports it. This is an alternative to just removing the underscore and making the property public.

**Prefer control statements over selection operators** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Ported from airbnb/javascript#1729 (⊶ airbnb/javascript@c8b11641)
↠ Added a new rule to prefer [control statements instead of selection operators][docs-r-ctrl_statm#selec_op].

**Ordering for React instance variables and methods** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Ported from airbnb/javascript#1737 (⊶ airbnb/javascript@ff1c1217)
↠ Added a suggestions about instance variables and methods for the [ordering of React component methods and properties][docs-r-react-order#meth_props].

**UPPERCASE naming convention for constants** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Ported from airbnb/javascript#255 (⊶ airbnb/javascript@33819d67)
↠ Added a new section about [naming conventions for constants][docs-r-name_conv#const].

**Consistent whitespaces inside blocks** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Ported from airbnb/javascript#1798 (⊶ airbnb/javascript@edf942ee)
↠ Added a new section about [consistent whitespaces inside block][docs-r-ws#in_blocks].

**Spacing around commas** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Ported from airbnb/javascript#1798 (⊶ airbnb/javascript@edf942ee)
↠ Added a new section about [whitespaces around commas][docs-r-ws#commas].

**Spacing inside computed properties** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Ported from airbnb/javascript#1798 (⊶ airbnb/javascript@edf942ee)
↠ Added a new section about [whitespaces inside computed properties][docs-r-ws#in_comp_props].

**Spacing around function signatures** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Ported from airbnb/javascript#1798 (⊶ airbnb/javascript@edf942ee)
↠ Added a new section about [whitespaces around function signatures][docs-r-ws#func_sig].

**Spacing inside object literal properties** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Ported from airbnb/javascript#1798 (⊶ airbnb/javascript@edf942ee)
↠ Added a new section about [whitespaces inside object literal properties][docs-r-ws#in_obj_lit_props].

**Trailing spaces at the end of lines** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Ported from airbnb/javascript#1798 (⊶ airbnb/javascript@edf942ee)
↠ Added a new section about [trailing spaces at the end of lines][docs-r-ws#trail_eof].

**Multiple empty lines** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Ported from airbnb/javascript#1798 (⊶ airbnb/javascript@edf942ee)
↠ Added a new section about [multiple empty lines][docs-r-ws#mult_blk_line].

**Unused variables** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Ported from airbnb/javascript#1828 (⊶ airbnb/javascript@edf942ee)
↠ Added a new section about [unused variables][docs-r-vars#unused].

### Packages

#### `@arcticicestudio/eslint-config-base`

**New `function-call-argument-newline` rule** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Transferred from ~~arcticicestudio/eslint-config-arcticicestudio-base#32 ⇄ arcticicestudio/eslint-config-arcticicestudio-base#33~~ (⊶ ~~arcticicestudio/eslint-config-arcticicestudio-base@e25bf80c4~~)
↠ Added and **disabled** the new [`function-call-argument-newline`][esl-r-function-call-argument-newline] core rule introduced in [ESLint version 6.2.0][gh-esl-rl-v6.2.0].

## Improvements

### Style Guide

**Reference `function-paren-newline` for function signature invocation indentations** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Ported from airbnb/javascript#1756 (⊶ airbnb/javascript@a9fc9d8a)
↠ Added a reference for the ESLint core rule [`function-paren-newline`][esl-r-function-paren-newline] to the [function signature invocation indentation][docs-r-func#sig_invoc_indent] section.

**Index as `key` are anti-pattern** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Ported from airbnb/javascript#1899 (⊶ airbnb/javascript@48448a81)
↠ Added additional information [why index as `key` are an anti-pattern][docs-r-react-props#no_idx_key].

**`let` or `const` guideline is incompatible with „destructuring“** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Ported from airbnb/javascript#1927 (⊶ airbnb/javascript@9af5ee89)
↠ Added a info about assignments to the section about [declaration separation][docs-r-vars#dec_sep] to be compatible with rules about [destructuring][docs-r-destrc#obj].

**Reference to `no-prototype-builtins` rule** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Ported from airbnb/javascript#1929 (⊶ airbnb/javascript@924dfb26)
↠ Added a reference to the section about [prototype builtins][docs-r-obj#prot_btin] for the corresponding [`no-prototype-builtins`][esl-r-no-prototype-builtins] rule.

**Reference to `react/jsx-filename-extension` rule** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Ported from airbnb/javascript#1930 (⊶ airbnb/javascript@24da5bb5)
↠ Added a reference to the section about [JSX file extension][docs-r-react-name_conv#jsx_fext] for the corresponding [`react/jsx-filename-extension`][gh-esl-p-react/jsx-filename-extension] rule.

**Reference to `react/no-array-index-key` rule** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Ported from airbnb/javascript#1930 (⊶ airbnb/javascript@24da5bb5)
↠ Added a reference to the section about [index as `key` props][docs-r-react-props#no_idx_key] for the corresponding [`react/no-array-index-key`][gh-esl-p-react/no-array-index-key] rule.

**More best practices for `.bind()` and arrow functions in React** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Ported from airbnb/javascript#2014 (⊶ airbnb/javascript@be07f7a0)
↠ Added more information and best practices in [React about method][docs-r-react-meth] binding (`.bind()`) and arrow functions when used within React classes like properties or in the scope of `render`.

**Better wording for „acronyms and initialisms“ guideline** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Ported from airbnb/javascript#1972 (⊶ airbnb/javascript@5d25a2ee)
↠ Improved the wording in the [acronyms and initialisms][docs-r-name_conv#acrs_inits] section by replacing `capitalized` with `uppercased` to clarify the purpose of guideline.

### Packages

#### `@arcticicestudio/eslint-config`

**Behavior of `react/forbid-prop-types` rule for `array` and `object`** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Ported from airbnb/javascript#1952 (⊶ airbnb/javascript@95286eb4)
↠ Added additional information about the specific behavior of the [`react/forbid-prop-types`][gh-esl-p-react/forbid-prop-types] rule regarding `array` and `object` type.

#### `@arcticicestudio/eslint-config-base`

**ESLint v6.0.0 Support** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Transferred from ~~arcticicestudio/eslint-config-arcticicestudio-base#30 ⇄ arcticicestudio/eslint-config-arcticicestudio-base#31 (⊶ ~~arcticicestudio/eslint-config-arcticicestudio-base@dfee6901~~)
↠ [ESLint v6 has been released][esl-b-rl-6.0.0] including the official [v6 migration guide][esl-d-mg-6.0.0].
To stay up-to-date with the latest security and stability changes as well as new rules, this configuration migrated to v6 while also dropping support for v4 and lower.

##### Updated (dev,peer)dependencies for ESLint v6.0.0 support

To stay up-to-date with the latest security and stability changes as well as new rules, all outdated (dev,peer)dependencies have been updated.

##### Removed deprecated `experimentalobjectrestspread` option

Since ESLint v5, the `parserOptions.ecmaFeatures.experimentalObjectRestSpread` option was deprecated and [has now been removed in v6][esl-d-mg-6.0.0#dep_obj_sprd].
To ensure the feature is used the `parserOptions.ecmaVersion` option has been updated to use ECMAScript version `2018` which includes this syntax feature.

##### Added new rules and adapted to changed default values

ESLint v6 introduced new rules as well as [updating default values and configurations of existing ones][esl-d-mg-6.0.0#recom].
The missing rules have been added while the default values have been compared and adjusted to the current configurations of this package.

##### Removed and replaced deprecated core rules

The following [rules are deprecated][esl-d-r#dep] and have been removed or replaced:

- `require-jsdoc` and `valid-jsdoc` - Both rules were not maintained anymore and were disabled anyway due to too noisy output.
- `no-catch-shadow` - Replaced by [`no-shadow`][esl-r-no-shadow]

**Ignore `__mocks__` for `import/no-extraneous-dependencies`** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Ported from airbnb/javascript#1772 (⊶ airbnb/javascript@8720f5f9)
↠ Added the `__mocks__` pattern as exception for the [`import/no-extraneous-dependencies`][gh-esl-p-import/no-extraneous-dependencies] rule since it should be considered as testing utils.

**Underscore naming pattern for `spec` tests** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Ported from airbnb/javascript#1732 (⊶ airbnb/javascript@8c83d03a)
↠ Extended the pattern for tests named with the `spec` pattern when using an underscore (`*_spec.js`) instead of an dot (`*.spec.js`) for the [`import/no-extraneous-dependencies`][gh-esl-p-import/no-extraneous-dependencies] rule.

**No dangling underscore in function names** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Ported from airbnb/javascript#1907 (⊶ airbnb/javascript@17e04546)
↠ Dangling underscores and not allowed for functions and are now enforced through the [`no-underscore-dangle`][esl-r-no-underscore-dangle] rule.

**Allow `staticContext` (_React Router_) for `no-param-reassign`** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Ported from airbnb/javascript#2029 (⊶ airbnb/javascript@1310ade9)
↠ Added `staticContext` ([_React Router_][react-router]) as exception for the [`no-param-reassign`][esl-r-no-param-reassign] rule.

**Switch from `eslint-restricted-globals` to `confusing-browser-globals`** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Ported from airbnb/javascript#1961 (⊶ airbnb/javascript@21b65e94)
↠ Switched from the superseded [`eslint-restricted-globals`][gh-eslint-restricted-globals] package to the new [`confusing-browser-globals`][gh-confusing-browser-globals] package that is part of the official React repository, used within [CRA][] and maintained by the React core team.

**Allow `jest.setup.js` file name pattern for `import/no-extraneous-dependencies`** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Ported from airbnb/javascript#1998 (⊶ airbnb/javascript@96f95fa3)
↠ Added the `jest.setup.js` file name pattern to the exceptions of the [`import/no-extraneous-dependencies`][gh-esl-p-import/no-extraneous-dependencies] rule to support the general naming of [Jest][] setup files.

**Cleaner example for „array callback return“ handling** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Ported from airbnb/javascript#2004 (⊶ airbnb/javascript@495a62aa)
↠ Removed an unnecessary expression from the examples in the [„callback return“][docs-r-arr#clb_ret] section for arrays.

**Simplified `no-mixed-operators`** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Ported from airbnb/javascript#1864 (⊶ airbnb/javascript@f6acb789)
↠ Simplified the groups for the [`no-mixed-operators`][esl-r-no-mixed-operators] rule to adapt to the [corresponding style guide section][docs-r-comp_op_eq#mix_ops] that has been improved and updated.

## Bug Fixes

### Style Guide

**Updated link anchor for MDN page about `let` keyword** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Ported from airbnb/javascript#1818 (⊶ airbnb/javascript@c068d7cb)
↠ Fixed an anchor on the [“Hoisting”][docs-r-hoisting] page for a MDN link about [„temporal dead zones“][mdn-js-kw-let#tmp_dead_zone] of the `let` keyword.

**Invalid link anchor for W3 page about „ARIA Roles“` keyword** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Ported from airbnb/javascript#1823 (⊶ airbnb/javascript@8a244801)
↠ Fixed an anchor on the [React Accessibility A11Y][docs-r-react-a11y#aria_roles] page for a W3 link about [“ARIA roles”][w3-aria_roles#intro].

**Invalid example for npm `has` package** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Ported from airbnb/javascript#2062 (⊶ airbnb/javascript@030e23b1)
↠ Fixed an error in the usage example of the [`has`][npm-has] package in the [„Object Rest Spread“][docs-r-obj#rest_spr] section.

### Packages

#### `@arcticicestudio/eslint-config-base`

**No additional new line at end of file** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Ported from airbnb/javascript#1794, airbnb/javascript#2017 (⊶ airbnb/javascript@2d977990, airbnb/javascript@60b96d32)
↠ Changed the `maxEOF` option of the [`no-multiple-empty-lines`][esl-r-no-multiple-empty-lines] rule to `0` since ESLint by default [swallows the final newline, as some editors add it automatically][gh-esl-b-7ad86de-r-empty_line:63]. This prevents an additional new line at the end of files next to the default _EOF_ handling.

# 0.5.0

![Release Date: none](https://img.shields.io/static/v1.svg?style=flat-square&label=Release%20Date&message=-&colorA=4c566a&colorB=88c0d0) ![Milestone](https://img.shields.io/static/v1.svg?style=flat-square&label=Milestone&message=0.5.0&logo=github&logoColor=eceff4&colorA=4c566a&colorB=88c0d0)

↳ Release date of transferred `eslint-config` package: _2019-08-19_
↳ Release date of transferred `eslint-config-base` package: _2018-11-17_

## Features

### Packages

#### `@arcticicestudio/eslint-config`

**Entry point for Prettier plugin integration** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Transferred from ~~arcticicestudio/eslint-config-arcticicestudio#12 ⇄ arcticicestudio/eslint-config-arcticicestudio#15~~ (⊶ ~~arcticicestudio/eslint-config-arcticicestudio@8935d75a~~)
↠ All _Arctic Ice Studio_ projects using [Prettier][] for a smooth and uncomplicated developer experience as well as keeping the code style consistent across own and third-party projects.
Almost all projects have added the [eslint-plugin-prettier][gh-esl-p-prettier] plugin to run Prettier as an ESLint rule and report differences as individual ESLint issues.

Therefore a new entry point has been added that

- enables the `prettier` plugin.
- enables the `prettier/prettier` rule to `error` level in order to enable the linting output.
- extends the official Prettier ESLint configuration from the [ `eslint-config-prettier` package][gh-esl-c-prettier] to ensure the best compatibility with Prettier as well as reducing required maintenance overhead to keep up-to-date with new Prettier releases. It also extends the following shared configurations to include support for other ESLint plugins:
  - `eslint-plugin-react` through the shared `prettier/react` configuration

The new entry point is available as `@arcticicestudio/eslint-config/prettier` and can be composed with the default entry point to inherit the rules and include all existing integrations like for „React“ and „JSX A11Y“.

## Improvements

### Packages

#### `@arcticicestudio/eslint-config`

**ESLint v6.0.0 Support** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Transferred from ~~arcticicestudio/eslint-config-arcticicestudio#13 ⇄ arcticicestudio/eslint-config-arcticicestudio#14 (⊶ ~~arcticicestudio/eslint-config-arcticicestudio@6948a181~~)
↠ [ESLint v6 has been released][esl-b-rl-6.0.0] including the official [v6 migration guide][esl-d-mg-6.0.0].
To stay up-to-date with the latest security and stability changes as well as new rules, this configuration migrated to v6 while also dropping support for v4 and lower.

##### Updated (dev,peer)dependencies for ESLint v6.0.0 support

To stay up-to-date with the latest security and stability changes as well as new rules, all outdated (dev,peer)dependencies have been updated.

##### Updated React plugin settings

The version has been changed to be automatically detected by using the `detect` value and the `pragma` key has been removed since it will be handled by Babel.

##### Added new React and JSX A11Y plugin rules and adapted new default values

The `react` and `jsx-a11y` plugins introduced new rules as well as updating default values and configurations of existing ones.
The missing rules have been added while the default values have been compared and adjusted to the current configurations of this package.

##### Removed deprecated plugin rules

The following rules have been deprecated and therefore removed or replaced:

- [`jsx-a11y/label-has-for`][gh-esl-p-jsx-a11y/label-has-for.md] - Replaced by [`label-has-associated-control`][gh-esl-p-jsx-a11y/label-has-associated-control].

#### `@arcticicestudio/eslint-config-base`

**No `quote-props` for numbers and keywords** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Transferred from ~~arcticicestudio/eslint-config-arcticicestudio-base#29 (⊶ ~~arcticicestudio/eslint-config-arcticicestudio@bbb6d35a~~)
↠ Disabled the [keywords][esl-r-quote-props#keywords] and [numbers][esl-r-quote-props#numbers] options of the `quote-props` rule. Both are not necessary anymore since this preset does not target legacy ES3 environments and disabling prevents unnecessary and noisy warnings.

# 0.4.0

![Release Date: none](https://img.shields.io/static/v1.svg?style=flat-square&label=Release%20Date&message=-&colorA=4c566a&colorB=88c0d0) ![Milestone](https://img.shields.io/static/v1.svg?style=flat-square&label=Milestone&message=0.4.0&logo=github&logoColor=eceff4&colorA=4c566a&colorB=88c0d0)

↳ Release date of transferred `eslint-config` package: _2018-11-16_
↳ Release date of transferred `eslint-config-base` package: _2018-11-15_

## Improvements

### Packages

#### `@arcticicestudio/eslint-config`

**Loosen JSX props ordering** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Transferred from ~~arcticicestudio/eslint-config-arcticicestudio#10 (⊶ ~~arcticicestudio/eslint-config-arcticicestudio@cf8a9744~~)
↠ Disabled the [gh-esl-p-react/boolean-prop-naming][] rule because it was actually too noisy and prevented the usage of useful shortcut props like `outlined` or `loaded`.

**No more consistent naming validation for JSX boolean props** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Transferred from ~~arcticicestudio/eslint-config-arcticicestudio#11 (⊶ ~~arcticicestudio/eslint-config-arcticicestudio@27e75c91~~)
↠ The `callbacksLast` and `shorthandFirst` options of the [gh-esl-p-react/jsx-sort-props][] rule caused multiple warnings when formatted with [Prettier][] and conflicted with the alphabetically ordering and have therefore been **disabled**.

#### `@arcticicestudio/eslint-config-base`

**No more JSDoc comment validation** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Transferred from ~~arcticicestudio/eslint-config-arcticicestudio-base#28 (⊶ ~~arcticicestudio/eslint-config-arcticicestudio-base@eab37dd2~~)
↠ Disabled the [`valid-jsdoc`][esl-r-valid-jsdoc] core rule because it is actually too noisy and not suitable in most cases when used with JSX/React and some of the latest ES6 (or higher) features/proposals when the return type is not known. When using [TypeScript][] or [Flow][] the return type and parameters are typed.

# 0.3.0

![Release Date: none](https://img.shields.io/static/v1.svg?style=flat-square&label=Release%20Date&message=-&colorA=4c566a&colorB=88c0d0) ![Milestone](https://img.shields.io/static/v1.svg?style=flat-square&label=Milestone&message=0.3.0&logo=github&logoColor=eceff4&colorA=4c566a&colorB=88c0d0)

↳ Release date of transferred `eslint-config` package: _2018-05-20_
↳ Release date of transferred `eslint-config-base` package: _2018-05-20_

## Improvements

### Packages

#### `@arcticicestudio/eslint-config`

**Prevent _SemVer Major Zero Caveat_** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Transferred from ~~arcticicestudio/eslint-config-arcticicestudio#8 ⇄ arcticicestudio/eslint-config-arcticicestudio#9~~ (⊶ ~~arcticicestudio/eslint-config-arcticicestudio@daa1ea3e~~)
↠ Raised the version range for the [base package][gh-t-pkg-esl-base] to `>=0.2.0 <1.0.0` in order to avoid the _SemVer Major Zero Caveat_.

This prevents that only the exact version specified will match. By allowing all versions `<1.0.0` this package resolves to the latest development version when a new version of the base package is released without the need to manually update to the version.

#### `@arcticicestudio/eslint-config-base`

**No more minimum amount of properties for `object-curly-newline`** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Transferred from ~~arcticicestudio/eslint-config-arcticicestudio-base#26 ⇄ arcticicestudio/eslint-config-arcticicestudio-base#27~~ (⊶ ~~arcticicestudio/eslint-config-arcticicestudio-base@1c4ee04b~~)
↠ Removed the minimum amount of properties for the [`object-curly-newline`][esl-r-object-curly-newline] rule so the `consistent` option ensures that the style is consistent for every case.

Previously it was configured to require a line break when there are 4 or more properties within the object curly braces on the same line. This resulted in noisy errors because the names can also be very short and fit perfectly into one line e.g. when used with React prop [destructuring][mdn-js-op-destruct].

<p align="center"><img src="https://user-images.githubusercontent.com/7836623/63180525-c107b280-c04e-11e9-8a88-9577be9b93c9.png" width="66%"/></p>

Because [Prettier][] is used in all project development workflows, the indentation is automatically handled when the length of the properties exceeds the maximum line length or reduces the readability. Therefore the decision to use a line break or not should be handled by Prettier instead of using a hard coded amount value.

This improvement also added the `ImportDeclaration` and `ExportDeclaration` configurations, introduced in [ESLint version 4.18.0][gh-esl-rl-4.18.0], to avoid different behavior when updating to this version.

# 0.2.0

![Release Date: none](https://img.shields.io/static/v1.svg?style=flat-square&label=Release%20Date&message=-&colorA=4c566a&colorB=88c0d0) ![Milestone](https://img.shields.io/static/v1.svg?style=flat-square&label=Milestone&message=0.2.0&logo=github&logoColor=eceff4&colorA=4c566a&colorB=88c0d0)

↳ Release date of transferred `eslint-config` package: _2018-05-14_
↳ Release date of transferred `eslint-config-base` package: _2018-05-12_

## Features

### Packages

#### `@arcticicestudio/eslint-config`

**New React rule `react/jsx-max-depth`** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Transferred from ~~arcticicestudio/eslint-config-arcticicestudio#6 ⇄ arcticicestudio/eslint-config-arcticicestudio#7~~ (⊶ ~~arcticicestudio/eslint-config-arcticicestudio@356292cd~~)
↠ Added new rule [`react/jsx-max-depth`][gh-esl-p-react/jsx-max-depth] to validate the maximum JSX depth. Introduced in [eslint-plugin-react][gh-esl-p-react] version [7.7.0][gh-esl-p-react-clog-7.7.0].

#### `@arcticicestudio/eslint-config-base`

**New import rule `import/no-self-import`** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Transferred from ~~arcticicestudio/eslint-config-arcticicestudio-base#13 ⇄ arcticicestudio/eslint-config-arcticicestudio-base#22~~ (⊶ ~~arcticicestudio/eslint-config-arcticicestudio-base@ff353600~~)
↠ Added and **enabled** rule [`import/no-self-import`][gh-esl-p-import/no-self-import] to prevent a module from importing itself. Introduced in [eslint-plugin-import][gh-esl-p-import] version [2.9.0][gh-esl-p-import-clog-2.9.0].

<p align="center"><img src="https://user-images.githubusercontent.com/7836623/63177504-5784a580-c048-11e9-9f63-3f6572815a34.png" width="66%"/></p>

**New import rule `import/no-useless-path-segments`** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Transferred from ~~arcticicestudio/eslint-config-arcticicestudio-base#14 ⇄ arcticicestudio/eslint-config-arcticicestudio-base#23~~ (⊶ ~~arcticicestudio/eslint-config-arcticicestudio-base@4f0744b7~~)
↠ Added and **enabled** rule [`import/no-useless-path-segments`][gh-esl-p-import/no-useless-path-segments] to prevent unnecessary path segments in import and require statements. Introduced in [eslint-plugin-import][gh-esl-p-import] version [2.9.0][gh-esl-p-import-clog-2.9.0].

**New import rule `import/no-default-export`** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Transferred from ~~arcticicestudio/eslint-config-arcticicestudio-base#15 ⇄ arcticicestudio/eslint-config-arcticicestudio-base#24~~ (⊶ ~~arcticicestudio/eslint-config-arcticicestudio-base@4b3dcdab~~)
↠ Added and **disabled** rule [`import/no-default-export`][gh-esl-p-import/no-default-export] to forbid default exports. Introduced in [eslint-plugin-import][gh-esl-p-import] version [2.9.0][gh-esl-p-import-clog-2.9.0].

**New import rule `import/no-cycle`** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Transferred from ~~arcticicestudio/eslint-config-arcticicestudio-base#16 ⇄ arcticicestudio/eslint-config-arcticicestudio-base#25~~ (⊶ ~~arcticicestudio/eslint-config-arcticicestudio-base@273430b9~~)
↠ Added and **enabled** rule [`import/no-cycle`][gh-esl-p-import/no-cycle] to prevent a module from importing a module with a dependency path back to itself. Introduced in [eslint-plugin-import][gh-esl-p-import] version [2.10.0][gh-esl-p-import-clog-2.10.0].

<p align="center"><img src="https://user-images.githubusercontent.com/7836623/63178032-79325c80-c049-11e9-9dad-e33906408dca.png" width="66%"/></p>

<p align="center"><img src="https://user-images.githubusercontent.com/7836623/63178034-79325c80-c049-11e9-85ad-7fe95aa0d72e.png" width="66%"/></p>

## Improvements

### Packages

#### `@arcticicestudio/eslint-config`

**New and deprecated React 16.3 lifecycle methods** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Transferred from ~~arcticicestudio/eslint-config-arcticicestudio#4 ⇄ arcticicestudio/eslint-config-arcticicestudio#5~~ (⊶ ~~arcticicestudio/eslint-config-arcticicestudio@0a444a20~~)
↠ Added the new React 16.3 lifecycle method [`getSnapshotBeforeUpdate`][react-d-comp#lc_gsbu] and the now deprecated (“async unsafe“) lifecycle `React.Component` methods, prefixed with `UNSAFE_`, to the except methods of the [`class-methods-use-this`][esl-r-class-methods-use-this] core rule.
Previously this resulted in a warning when no `this` keyword was used within the method.

<p align="center"><img src="https://user-images.githubusercontent.com/7836623/63180045-b26ccb80-c04d-11e9-8073-06fb52ca88d9.png" width="66%"/></p>

**New and deprecated React 16.3 lifecycle methods** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Transferred from ~~arcticicestudio/eslint-config-arcticicestudio#3 (⊶ ~~arcticicestudio/eslint-config-arcticicestudio@9ea7d770~~)
↠ Updated to the latest [base package][gh-t-pkg-esl-base] version [0.2.0][gh-clog#0.2.0] that added support for new ESLint core and plugin rules as well as many other improvements and bug fixes.

#### `@arcticicestudio/eslint-config-base`

**Import-related rule refactoring** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Transferred from ~~arcticicestudio/eslint-config-arcticicestudio-base#6 ⇄ arcticicestudio/eslint-config-arcticicestudio-base#12~~ (⊶ ~~arcticicestudio/eslint-config-arcticicestudio-base@8395e07d~~)
↠ Refactored rules related to imports that caused many style based warnings regarding ordering and sorting of `import` statements.

###### Import Order Conflict

The [`import/first`][gh-esl-p-import/first] and [`import/order`][gh-esl-p-import/order] rules were conflicting. While `import/first` disallowed

```js
import "../config";
import fs from "fs"; // <-- Error: Absolute imports should come before relative imports
import App from "../App";
```

`import/order` on the other hand was fine with this as mentioned in the rule documentation:

> Unassigned imports are ignored, as the order they are imported in may be important.

This has been improved by allowing unassigned imports anywhere, **but still above all other non-import statements**.

Also the import groups have been specified more accurate by splitting them into three main groups:

1. _builtin_ and _external_ modules
2. _internal_ modules (e.g. if configured via webpack to handle internal paths differently)
3. _parent_, _sibling_ and _index_ modules

These three groups must be separated by a blank line.

###### Import Sort Conflict

The [`sort-imports`][esl-r-sort-imports] rule conflicted with both of the other mentioned rules described above. It is not that important how imports are sorted within groups so this rule has been disabled until there's a way to make it work regarding the compatibility with other rules.

<p align="center"><img src="https://user-images.githubusercontent.com/7836623/63178408-45a40200-c04a-11e9-840b-a4f214690d61.png" width="66%"/></p>

**Allow line break for arrow function implicit returns** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Transferred from ~~arcticicestudio/eslint-config-arcticicestudio-base#7 ⇄ arcticicestudio/eslint-config-arcticicestudio-base#17~~ (⊶ ~~arcticicestudio/eslint-config-arcticicestudio-base@fa3d6e8c~~)
↠ Line breaks are now allowed for implicit returns of arrow functions.
Previously it was configured to enforce the implicit return statement to be beside the arrow. This prevented longer statements to be placed on the next line to improve the readability and compliance with the maximum line length. These restrictions have now been lifted.

<p align="center"><img src="https://user-images.githubusercontent.com/7836623/63178529-84d25300-c04a-11e9-9aca-b64f43123b36.png" width="66%"/></p>

**No default case for switch block** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Transferred from ~~arcticicestudio/eslint-config-arcticicestudio-base#9 ⇄ arcticicestudio/eslint-config-arcticicestudio-base#19~~ (⊶ ~~arcticicestudio/eslint-config-arcticicestudio-base@1d9ad4ef~~)
↠ _switch-case_ blocks no longer require a `default` case. The [`default-case`][esl-r-default-case] rule has been disabled, because most of the time a `default` case is not necessary and should be handled by the developer depending on the use case and code scope.

**Use line breaks after operators** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Transferred from ~~arcticicestudio/eslint-config-arcticicestudio-base#10 ⇄ arcticicestudio/eslint-config-arcticicestudio-base#20~~ (⊶ ~~arcticicestudio/eslint-config-arcticicestudio-base@9894f0d8~~)
↠ Line breaks are now placed **after** operators instead **before** them. Previously the [`operator-linebreak`][esl-r-operator-linebreak] core rule was configured to enforce line breaks to be placed before operators which could lead to confusions when indenting lines because of the [maximum line length][esl-r-max-len]. It now enforces line breaks after operators, but exceptions for the [conditional (ternary) operators][mdn-js-op-cond] `?` and `:` are configured to use line breaks before.

<p align="center"><img src="https://user-images.githubusercontent.com/7836623/63178982-69b41300-c04b-11e9-9662-42dba926015b.png" width="66%"/></p>

**Gatsby configuration file pattern for `devDependencies` imports** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Transferred from ~~arcticicestudio/eslint-config-arcticicestudio-base#11 ⇄ arcticicestudio/eslint-config-arcticicestudio-base#21~~ (⊶ ~~arcticicestudio/eslint-config-arcticicestudio-base@581fd812~~)
↠ The [`import/no-extraneous-dependencies`][gh-esl-p-import/no-extraneous-dependencies] rule now allows the import of `devDependencies` in [Gatsby][] configuration, currently including the following pattern:

```raw
gatsby-browser.js
gatsby-config.js
gatsby-node.js
gatsby-ssr.js
```

These pattern should match all of the listed files as well as new files that might possibly be added in the future.

<p align="center"><img src="https://user-images.githubusercontent.com/7836623/63179061-9e27cf00-c04b-11e9-87e9-f2f9e78bff3e.png" width="66%"/></p>

## Bug Fixes

### Packages

#### `@arcticicestudio/eslint-config-base`

**Consistent line break usage within function parentheses** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Transferred from ~~arcticicestudio/eslint-config-arcticicestudio-base#8 ⇄ arcticicestudio/eslint-config-arcticicestudio-base#18~~ (⊶ ~~arcticicestudio/eslint-config-arcticicestudio-base@f4af5ecf~~)
↠ Line breaks within function parentheses are now consistent.
Previously the [`function-paren-newline`][esl-r-function-paren-newline] core rule was configured with `multiline` that only allowed a line break after the opening brace when the parameter also contains a line break, otherwise it disallows any line break within the parentheses.

This was [not conform with the styleguide][docs-r-func#sig_invoc_indent] and has been changed to the `consistent` option. This requires consistent usage of line breaks for each pair of parentheses. It reports an error if one parenthesis in the pair has a line break inside it and the other parenthesis does not.

<p align="center"><img src="https://user-images.githubusercontent.com/7836623/63179464-72f1af80-c04c-11e9-80b3-b5c39b109e98.png" width="66%"/></p>

##### Toolbox

**No peer dependency installation for CI/CD builds** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Transferred from ~~arcticicestudio/eslint-config-arcticicestudio-base#3 ⇄ arcticicestudio/eslint-config-arcticicestudio-base#4~~ (⊶ ~~arcticicestudio/eslint-config-arcticicestudio-base@fe418ec4~~)
↠ The installation of peer dependencies for CI/CD build (Circle CI) has been removed from the build configuration.

It was set up to run the `npx` command to install the peer dependencies that is only required for users of the package, but not the package itself. The same dependencies are defined in `devDependencies` and therefore installed by default on `npm install`.

# 0.1.0

![Release Date: 2018-01-27](https://img.shields.io/static/v1.svg?style=flat-square&label=Release%20Date&message=2018-01-27&colorA=4c566a&colorB=88c0d0) [![Project Board](https://img.shields.io/static/v1.svg?style=flat-square&label=Project%20Board&message=0.1.0&logo=github&logoColor=eceff4&colorA=4c566a&colorB=88c0d0)](https://github.com/arcticicestudio/styleguide-javascript/projects/2) [![Milestone](https://img.shields.io/static/v1.svg?style=flat-square&label=Milestone&message=0.1.0&logo=github&logoColor=eceff4&colorA=4c566a&colorB=88c0d0)](https://github.com/arcticicestudio/styleguide-javascript/milestone/1)

↳ Release date of transferred `eslint-config` package: _2018-02-05_
↳ Release date of transferred `eslint-config-base` package: _2018-02-04_

> Detailed information can be found in the [project documentation][docs].

## Features

### Style Guide

**Base Rules** — #1 ⇄ #2 (⊶ dee0441a)
↠ Added the initial style guide with chapters to learn about the [comprehensive base rules][docs-r].

**Base Rules** — #3 ⇄ #4 (⊶ cee71142)
↠ Added the initial style guide for [React][docs-r-react] specific rules like [Higher-Order Components][docs-r-react-hoc], the [component methods & properties ordering][docs-r-react-order#meth_props] and [props][docs-r-react-props].

### Packages

#### `@arcticicestudio/eslint-config`

**Base Rules** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Transferred from ~~arcticicestudio/eslint-config-arcticicestudio#1 ⇄ arcticicestudio/eslint-config-arcticicestudio#2~~ (⊶ ~~arcticicestudio/eslint-config-arcticicestudio@c46bf556~~)
↠ Added all rules of the [eslint-plugin-react][gh-esl-p-react] and [eslint-plugin-jsx-a11y][gh-esl-p-jsx-a11y] plugins based on the [React][docs-r-react] and [Accessibility A11Y][docs-r-react-a11y] style guidelines as shareable ESLint config.
More details can also be found in the initially published ~~[project documentation][noop]~~.

#### `@arcticicestudio/eslint-config-base`

**Base Rules** — #8 ⇄ #16 (⊶ ac611f7e)
↳ Transferred from ~~arcticicestudio/eslint-config-arcticicestudio-base#1 ⇄ arcticicestudio/eslint-config-arcticicestudio-base#2~~ (⊶ ~~arcticicestudio/eslint-config-arcticicestudio-base@9ba25a53~~)
↠ Added all [ESLint core rules][esl-r] and [eslint-plugin-import][gh-esl-p-import] plugin rules.
More details can also be found in the initially published ~~[project documentation][noop]~~.

<p align="center"><img src="https://raw.githubusercontent.com/arcticicestudio/nord-docs/develop/assets/images/nord/repository-footer-separator.svg?sanitize=true" /></p>

<p align="center">Copyright &copy; 2018-present <a href="https://www.arcticicestudio.com" target="_blank">Arctic Ice Studio</a> and <a href="https://www.svengreb.de" target="_blank">Sven Greb</a></p>

<p align="center"><a href="https://github.com/arcticicestudio/styleguide-javascript/blob/develop/LICENSE.md" target="_blank"><img src="https://img.shields.io/static/v1.svg?style=flat-square&label=License&message=MIT&logoColor=eceff4&logo=github&colorA=4c566a&colorB=88c0d0"/></a></p>

<!--
+------------------+
+ Symbol Reference +
+------------------+
↠ (U+21A0): Start of a log section description
— (U+2014): Separator between a log section title and the metadata
⇄ (U+21C4): Separator between a issue ID and pull request ID in a log metadata
⊶ (U+22B6): Icon prefix for the short commit SHA checksum in a log metadata
-->

<!--lint disable final-definition-->

<!-- Base -->

[cra]: https://create-react-app.dev
[docs-r-react]: https://arcticicestudio.github.io/styleguide-javascript/rules/react/index.html
[docs-r]: https://arcticicestudio.github.io/styleguide-javascript/rules/index.html
[docs]: https://arcticicestudio.github.io/styleguide-javascript
[esl-r]: https://eslint.org/docs/rules
[eslint]: https://eslint.org
[flow]: https://flow.org
[gatsby]: https://gatsbyjs.org
[gh-esl-c-prettier]: https://github.com/prettier/eslint-config-prettier
[gh-esl-p-import]: https://github.com/benmosher/eslint-plugin-import
[gh-esl-p-jsx-a11y]: https://github.com/evcohen/eslint-plugin-jsx-a11y
[gh-esl-p-prettier]: https://github.com/prettier/eslint-plugin-prettier
[gh-esl-p-react]: https://github.com/yannickcr/eslint-plugin-react
[gh-t-pkg-esl-base]: https://github.com/arcticicestudio/styleguide-javascript/tree/develop/packages/@arcticicestudio/eslint-config-base
[gh-t-pkg-esl]: https://github.com/arcticicestudio/styleguide-javascript/tree/develop/packages/@arcticicestudio/eslint-config
[jest]: https://jestjs.io
[mdn-js-op-cond]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_Operator
[mdn-js-op-destruct]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment
[noop]: #
[prettier]: https://prettier.io
[remark]: https://remark.js.org
[semver]: https://semver.org
[shields.io]: https://shields.io
[trbdev-monorepo]: https://trunkbaseddevelopment.com/monorepos
[typescript]: https://www.typescriptlang.org

<!-- Shared -->

[docs-r-func#sig_invoc_indent]: https://arcticicestudio.github.io/styleguide-javascript/rules/functions.html#signature-invocation-indentation
[docs-r-react-order#meth_props]: https://arcticicestudio.github.io/styleguide-javascript/rules/react/ordering.html#component-methods-and-properties
[esl-b-rl-6.0.0]: https://eslint.org/blog/2019/06/eslint-v6.0.0-released
[esl-d-mg-6.0.0]: https://eslint.org/docs/user-guide/migrating-to-6.0.0
[styleguide-markdown]: https://arcticicestudio.github.io/styleguide-markdown

<!-- v0.1.0 -->

[docs-r-react-a11y]: https://arcticicestudio.github.io/styleguide-javascript/rules/react/accessibility_a11y.html
[docs-r-react-hoc]: https://arcticicestudio.github.io/styleguide-javascript/rules/react/higher_order_components.html
[docs-r-react-props]: https://arcticicestudio.github.io/styleguide-javascript/rules/react/props.html

<!-- v0.2.0 -->

[esl-r-class-methods-use-this]: https://eslint.org/docs/rules/class-methods-use-this
[esl-r-function-paren-newline]: https://eslint.org/docs/rules/function-paren-newline
[esl-r-max-len]: https://eslint.org/docs/rules/max-len
[esl-r-operator-linebreak]: https://eslint.org/docs/rules/operator-linebreak
[esl-r-sort-imports]: https://eslint.org/docs/rules/sort-imports
[gh-clog#0.2.0]: https://github.com/arcticicestudio/styleguide-javascript/blob/develop/CHANGELOG.md#020
[gh-esl-p-import-clog-2.10.0]: https://github.com/benmosher/eslint-plugin-import/blob/master/CHANGELOG.md#2100---2018-03-29
[gh-esl-p-import-clog-2.9.0]: https://github.com/benmosher/eslint-plugin-import/blob/master/CHANGELOG.md#290---2018-02-21
[gh-esl-p-import/first]: https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/first.md
[gh-esl-p-import/no-cycle]: https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/no-cycle.md
[gh-esl-p-import/no-default-export]: https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/no-default-export.md
[gh-esl-p-import/no-extraneous-dependencies]: https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/no-extraneous-dependencies.md
[gh-esl-p-import/no-self-import]: https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/no-self-import.md
[gh-esl-p-import/no-useless-path-segments]: https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/no-useless-path-segments.md
[gh-esl-p-import/order]: https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/order.md
[gh-esl-p-react-clog-7.7.0]: https://github.com/yannickcr/eslint-plugin-react/releases/tag/v7.7.0
[gh-esl-p-react/jsx-max-depth]: https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-max-depth.md
[react-d-comp#lc_gsbu]: https://reactjs.org/docs/react-component.html#getsnapshotbeforeupdate

<!-- v0.3.0 -->

[esl-r-default-case]: https://eslint.org/docs/rules/default-case
[esl-r-object-curly-newline]: https://eslint.org/docs/rules/object-curly-newline
[gh-esl-rl-4.18.0]: https://github.com/eslint/eslint/releases/tag/v4.18.0

<!-- v0.4.0 -->

[esl-r-valid-jsdoc]: https://eslint.org/docs/rules/valid-jsdoc
[gh-esl-p-react/boolean-prop-naming]: https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/boolean-prop-naming.md
[gh-esl-p-react/jsx-sort-props]: https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-sort-props.md

<!-- v0.5.0 -->

[esl-r-quote-props#keywords]: https://eslint.org/docs/rules/quote-props.html#keywords
[esl-r-quote-props#numbers]: https://eslint.org/docs/rules/quote-props.html#numbers
[gh-esl-p-jsx-a11y/label-has-associated-control]: https://github.com/evcohen/eslint-plugin-jsx-a11y/blob/master/docs/rules/label-has-associated-control.md
[gh-esl-p-jsx-a11y/label-has-for.md]: https://github.com/evcohen/eslint-plugin-jsx-a11y/blob/master/docs/rules/label-has-for.md

<!-- v0.6.0 -->

[docs-r-arr#clb_ret]: https://arcticicestudio.github.io/styleguide-javascript/rules/arrays.html#callback-return
[docs-r-comp_op_eq#mix_ops]: https://arcticicestudio.github.io/styleguide-javascript/rules/comparison_operators_and_equality.html#no-mixed-operators
[docs-r-ctrl_statm#selec_op]: https://arcticicestudio.github.io/styleguide-javascript/rules/control_statements.html#selection_operators
[docs-r-destrc#obj]: https://arcticicestudio.github.io/styleguide-javascript/rules/destructuring.html#objects
[docs-r-hoisting]: https://arcticicestudio.github.io/styleguide-javascript/rules/hoisting.html
[docs-r-name_conv#acrs_inits]: https://arcticicestudio.github.io/styleguide-javascript/rules/naming_conventions.html#acronyms-and-initialisms
[docs-r-name_conv#const]: https://arcticicestudio.github.io/styleguide-javascript/rules/naming_conventions.html#constants
[docs-r-name_conv#undsc]: https://arcticicestudio.github.io/styleguide-javascript/rules/naming_conventions.html#underscores
[docs-r-obj#prot_btin]: https://arcticicestudio.github.io/styleguide-javascript/rules/objects.html#prototype-builtins
[docs-r-obj#rest_spr]: https://arcticicestudio.github.io/styleguide-javascript/rules/objects.html#rest-spread
[docs-r-react-a11y#aria_roles]: https://arcticicestudio.github.io/styleguide-javascript/rules/react/accessibility_a11y.html#valid-aria-roles
[docs-r-react-meth]: https://arcticicestudio.github.io/styleguide-javascript/rules/react/methods.html
[docs-r-react-name_conv#jsx_fext]: https://arcticicestudio.github.io/styleguide-javascript/rules/react/naming_conventions.html#jsx-file-extension
[docs-r-react-props#no_idx_key]: https://arcticicestudio.github.io/styleguide-javascript/rules/react/props.html#no-index-as-key
[docs-r-vars#dec_sep]: https://arcticicestudio.github.io/styleguide-javascript/rules/variables.html#declaration-separation
[docs-r-vars#unused]: https://arcticicestudio.github.io/styleguide-javascript/rules/variables.html#unused
[docs-r-ws#commas]: https://arcticicestudio.github.io/styleguide-javascript/rules/whitespace.html#around-commas
[docs-r-ws#func_sig]: https://arcticicestudio.github.io/styleguide-javascript/rules/whitespace.html#around-function-signatures
[docs-r-ws#in_blocks]: https://arcticicestudio.github.io/styleguide-javascript/rules/whitespace.html#inside-blocks
[docs-r-ws#in_comp_props]: https://arcticicestudio.github.io/styleguide-javascript/rules/whitespace.html#inside-computed-properties
[docs-r-ws#in_obj_lit_props]: https://arcticicestudio.github.io/styleguide-javascript/rules/whitespace.html#inside-object-literal-properties
[docs-r-ws#mult_blk_line]: https://arcticicestudio.github.io/styleguide-javascript/rules/whitespace.html#multiple-empty-lines
[docs-r-ws#trail_eof]: https://arcticicestudio.github.io/styleguide-javascript/rules/whitespace.html#trailing-spaces-at-the-end-of-lines
[esl-d-mg-6.0.0#dep_obj_sprd]: https://eslint.org/docs/user-guide/migrating-to-6.0.0#-the-depreacted-experimentalobjectrestspread-option-has-been-removed
[esl-d-mg-6.0.0#recom]: https://eslint.org/docs/user-guide/migrating-to-6.0.0#eslint-recommended-changes
[esl-d-r#dep]: https://eslint.org/docs/rules/#deprecated
[esl-r-function-call-argument-newline]: https://eslint.org/docs/rules/function-call-argument-newline
[esl-r-no-mixed-operators]: https://eslint.org/docs/rules/no-mixed-operators
[esl-r-no-multiple-empty-lines]: https://eslint.org/docs/rules/no-multiple-empty-lines
[esl-r-no-param-reassign]: https://eslint.org/docs/rules/no-param-reassign
[esl-r-no-prototype-builtins]: https://eslint.org/docs/rules/no-prototype-builtins
[esl-r-no-shadow]: https://eslint.org/docs/rules/no-shadow
[esl-r-no-underscore-dangle]: https://eslint.org/docs/rules/no-underscore-dangle
[gh-confusing-browser-globals]: https://github.com/facebook/create-react-app/tree/master/packages/confusing-browser-globals
[gh-esl-b-7ad86de-r-empty_line:63]: https://github.com/eslint/eslint/blob/7ad86dea02feceb7631943a7e1423cc8a113fcfe/lib/rules/no-multiple-empty-lines.js#L63
[gh-esl-p-react/forbid-prop-types]: https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/forbid-prop-types.md
[gh-esl-p-react/jsx-filename-extension]: https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-filename-extension.md
[gh-esl-p-react/no-array-index-key]: https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/no-array-index-key.md
[gh-esl-rl-v6.2.0]: https://github.com/eslint/eslint/releases/tag/v6.2.0
[gh-eslint-restricted-globals]: https://github.com/sidoshi/eslint-restricted-globals
[mdn-js-kw-let#tmp_dead_zone]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let#Temporal_dead_zone
[npm-has]: https://www.npmjs.com/package/has
[react-router]: https://reacttraining.com/react-router
[w3-aria_roles#intro]: https://www.w3.org/TR/wai-aria/#usage_intro

<!-- v0.7.0 -->

[esl-d-dev-share_conf#scope]: https://eslint.org/docs/developer-guide/shareable-configs#npm-scoped-modules
[gh-blog-intro-issue-templ]: https://blog.github.com/2016-02-17-issue-and-pull-request-templates
[gh-blog-multi-issue-templ]: https://blog.github.com/2018-01-25-multiple-issue-and-pull-request-templates
[gh-help-issue-templ-depr]: https://help.github.com/articles/manually-creating-a-single-issue-template-for-your-repository
[gh-help-issue-templ-repo]: https://help.github.com/articles/creating-issue-templates-for-your-repository
[gh-help-issue-templ]: https://help.github.com/articles/about-issue-and-pull-request-templates
[gh-help-pr-templ]: https://help.github.com/articles/creating-a-pull-request-template-for-your-repository
[gh-husky]: https://github.com/typicode/husky
[gh-lint-staged]: https://github.com/okonet/lint-staged
[gh-remark-cli]: https://github.com/remarkjs/remark/tree/master/packages/remark-cli
[gh-remark-lint]: https://github.com/remarkjs/remark-lint
[gh-remark-preset-lint-arcticicestudio]: https://github.com/arcticicestudio/remark-preset-lint-arcticicestudio
[git-d-gitattributes]: https://git-scm.com/docs/gitattributes
[git-d-gitignore]: https://git-scm.com/docs/gitignore
[git-d-mailmap]: https://git-scm.com/docs/git-shortlog#_mapping_authors
[npm-cli-dep]: https://docs.npmjs.com/cli/deprecate
[npm-d-scope]: https://docs.npmjs.com/about-scopes
[yarn-d-ws]: https://yarnpkg.com/en/docs/workspaces