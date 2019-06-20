# Angular CLI

### What is Angular CLI?

Angular CLI is command line interface for Angular. 

The Angular CLI is a command-line interface that allows you to create Angular project scaffolding, run, and build. It has built-in development server, so you can easily check the operation by running the project.

The following functions are supported by Angular CLI.

* Create Angular Project 
* Add components such as components, directives, pipes, services, classes, and interfaces to your Angular project 
* Launch Angular project with built-in development server that supports LiveReload 
* Unit / E2E \(end-to-end\) test environment support 
* Packaging the Angular project for deployment

{% embed url="https://cli.angular.io/" %}



### Install Angular CLI

```bash
$ npm install -g @angular/cli
```

To update to the latest version of Angular CLI, delete old version and install latest version as follows.

```bash
# Delete Angular CLI
$ npm uninstall -g @angular/cli
# Check cache verification
$ npm cache verify
# Install Angular CLI
$ npm install -g @angular/cli@latest
```

Check Angular CLI Version

```bash
$ ng version
```



### Create project

To create an Angular project, use the `ng new` command.

```bash
$ ng new <project-name>
```

Example

```bash
$ ng new my-app
```

When the project is created, a scaffolding of the following file structure is created.

```text
my-app/
├── .git/
├── e2e/
├── node_modules/
├── src/
├── .editorconfig
├── .gitignore
├── angular.json
├── package-lock.json
├── package.json
├── README.md
├── tsconfig.json
└── tslint.json
```



### Run the project

To preview the project locally, use the `ng serve` command.

```bash
$ ng serve
```

The `ng serve` command bundles source code and dependent modules using Webpack and runs the development server with built-in Angular CLI.

Open a browser and enter http: // localhost: 4200 in the address bar to connect to the development server. Note that if you add the --open \(abbreviated -o\) option when you run your project, it will automatically launch your browser.

```bash
$ ng serve --open
$ ng serve -o
```

If you are already using port 4200, you cannot run the built-in Angular CLI server. To change the port number and run it, add the --port \(shortened -p option\) as follows:

```bash
$ ng serve --port 4201
```



### Create project components

| target components | command | abbreviation |
| :--- | :--- | :--- |
| component | `ng generate component component-name` | `ng g c component-name` |
| directive | `ng generate directive directive-name` | `ng g d directive-name` |
| pipe | `ng generate pipe pipe-name` | `ng g p pipe-name` |
| service | `ng generate service service-name` | `ng g s service-name` |
| module | `ng generate module module-name` | `ng g m module-name` |
| guard | `ng generate guard guard-name` | `ng g g guard-name` |
| class | `ng generate class class-name` | `ng g cl class-name` |
| interface | `ng generate interface interface-name` | `ng g i interface-name` |
| Enum | `ng generate enum enum-name` | `ng g e enum-name` |



