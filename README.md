# generic-nodejs-toolchain v0.0.6
> A boilerplate for *Node.js* projects.



## Installation

Clone the repository

	git clone --depth=1 https://github.com/lud77/generic-nodejs-toolchain.git projectFolder

## Why?

This project contains the basic setup for a Node.js module or app. It includes opinionated tools and configuration for linting, transpilation, testing, code coverage, logging, automatic documentation, and packaging.



# Features / Usage

## Code quality

This project includes [ESLint](https://github.com/eslint/eslint) for linting, [Mocha](https://github.com/mochajs/mocha) and [Chai](https://github.com/chaijs/chai) for testing, [Istanbul](https://github.com/gotwarlost/istanbul) for test coverage. 
All of the modules are already configured and come with NPM scripts to have them work right out of the box.

The following scripts are available:

	npm run lint

to execute linting on JS files inside the /src folder;

	npm run test

to run all the tests included in the /test folder;

	npm run coverage

to run Istanbul on the tests, thus providing test coverage statistics and a coverage report (in the /coverage folder).



## Automation

The [Husky](https://github.com/typicode/husky) module is included to manage Git hooks, with callbacks provided for precommit and prepush. 
Both precommit and prepush are currently configured to lint and test the code before every commit and push operation.

A command to bump the Patch version is included:

	npm run update:version

this will add 1 to the Patch version number, rebuild the README.md and "git add" everything that changed. Minor and Major versions must be updated manually.



### Templated README

This package provides a system to simplify the generation of README files. The system makes use of the [Handlebars](https://github.com/wycats/handlebars.js/) template engine to allow you to pull values from the package.json automatically and include external partial templates. It also makes use of the [HbsRender](https://github.com/lud77/hbs-render) CLI rendering tool.

The templates (including the source of this README) are kept in the /pkg/readme folder. 

You can even define your own entries in the package.json file to make them available in the template files. You can see an example of this in action for the "badges" and "documentation" entries in this project's package.json file.

You can rebuild the README by executing:
	
	npm run build:readme

and you can modify the "build:readme" entry in the "scripts" section of the package.json file to make more or less partials available for the rendering.

More partials can be made available by adding a "-p" option for each of them in the "build:readme" script. The syntax is as follows:

	-p name_of_partial:path/to/partial.hbs

adding this option to the command line will allow you to use the partial "name_of_partial" inside your README.

To actually use a partial in the template use the standard Handlebars notation:

	{{#> name_of_partial}}


You can also provide inline default content for a partial by doing:

	{{#> name_of_partial}}

		...default content...

	{{/name_of_partial}}

E.g. at the bottom of the source of this README, you will find a {{#> license}} section. The default content of this section is a link to the https://opensource.org page relative to the license specified in the package.json. However, you can include your own license in your project by just adding the option

	-p license:/path/to/license.txt

in the "build:readme" command. You don't even need to change anything in the source of the README.md.hbs file in order to do this.



## Additional utilities

Includes a utility Batch file invoke.bat in the root folder to allow you to easily invoke modules providing a CLI tool. For instance, if you want to execute a cross-OS command using the Shx module, you can just type something like:

	invoke shx cp /folder1/original_file /folder2/backup_file

I'll add a Bash version of the script very soon, look at the roadmap for more features I'm planning to add.



## Automatic documentation

This project includes the JSDoc module to automatically generate documentation from the comments in the code using JavaDoc syntax.

To rebuild the documentation execute:

	npm run build:docs

and you'll find the documentation files in the /docs folder.

If you want to link to the documentation from the README, you just need to open up the README.md.hbs file and uncomment the {{#> documentation}} section.


## Logging

The package includes [Winston](http://github.com/winstonjs/winston) for the logging. 








## Roadmap

I plan to improve this package and its brother package [express-nodejs-toolchain](https://github.com/lud77/express-nodejs-toolchain) with the addition of many features. Among those:

- invoke.sh script (Bash equivalent of the invoke.bat script)
- automated download of feeds from activity streams of project management software to generate HISTORY.md files

Since the main focus is on avoiding feature bloat, many aspects will be left out of this package, including facilities for transpilation and modules managing Promises. Some of those aspects however, especially transpilation, will be addressed in [express-nodejs-toolchain](https://github.com/lud77/express-nodejs-toolchain).




## Licensing

This package is released under the [MIT License](https://opensource.org/licenses/MIT)

