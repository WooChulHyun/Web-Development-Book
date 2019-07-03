# Angular CLI

## What is Angular CLI?

Angular CLI is command line interface for Angular. 

The Angular CLI is a command-line interface that allows you to create Angular project scaffolding, run, and build. It has built-in development server, so you can easily check the operation by running the project.

The following functions are supported by Angular CLI.

* Create Angular Project 
* Add components such as components, directives, pipes, services, classes, and interfaces to your Angular project 
* Launch Angular project with built-in development server that supports LiveReload 
* Unit / E2E \(end-to-end\) test environment support 
* Packaging the Angular project for deployment

{% embed url="https://cli.angular.io/" %}



## Install Angular CLI

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



## Create project

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



## Run the project

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



## Create project components

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



## The prefix of selector property value and the component class name

```typescript
// src/app/home/home.component.ts
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-home',  // <------------- app is prefix
  templateUrl: './home.component.html',
  styleUrls: ['./home.component.css']
})
export class HomeComponent implements OnInit {

  constructor() { }

  ngOnInit() { }
}
```

In `angular.json` file,

```text
{
  "$schema": "./node_modules/@angular/cli/lib/config/schema.json",
  "version": 1,
  "newProjectRoot": "projects",
  "projects": {
    "my-app": {
      "root": "",
      "sourceRoot": "src",
      "projectType": "application",
      "prefix": "app", // <------------- prefix
      ...
}
```

If you modify the prefix property value of `angular.json`, the selector prefix of create component changes to the modified value. If you want to change the default selector prefix of a component from the project creation step, add the `--prefix` option when creating the project with `ng new`.

```bash
$ ng new my-app --prefix <prefix-name>
```



## templateUrl, styleUrls property, template, styles property

The `templateUr`l and `styleUrls` properties are used to load external files.

```typescript
...
@Component({
  selector: 'app-home',
  templateUrl: './home.component.html',
  styleUrls: ['./home.component.css']
})
...
```

You can write code inside of `@component` using the `template` and `styles` properties.

```typescript
...
@Component({
  selector: 'app-home',
  template: `
    <p>home works!</p>
  `,
  styles: [`
    p { color: red; }
  `]
})
...
```

If you want to use the inline template and CSS without creating the HTML template and CSS as an external file when you use the `ng generate component` command to create the component, use the following command.

```bash
# When using inline templates
$ ng generate component about --inline-template
# abbreviation ng g c about -t

# When using inline CSS
$ ng generate component about --inline-style
# abbreviation ng g c about -s

# When using inline templates and CSS
$ ng generate component about --inline-template --inline-style
# abbreviation ng g c about -t -s
```



## Build the project

After you have finished developing the project, use the `ng build` command for deployment.

```bash
$ ng build
```

When the build is complete, a `dist` folder is created in project root which containing the build output.

#### 

### Production Build and Deployment

`ng build` command executes the build by referring to the `src / environments / environments.ts` file.

```typescript
// src/environments/environments.ts
export const environment = {
  production: false
};
```

At this time, the executed build is a development environment build and is not optimized for production use. To run the production build, run the following command:

```bash
$ ng build --prod
```

At the time of the production build, refer to the `src / environments / environment.prod.ts` file and perform the build. The differences between the default build options for production builds and development environments are listed below.

| Flag | --dev | --prod |
| :--- | :--- | :--- |
| --aot | false | true |
| --environment | dev | prod |
| --output-hashing | media | all |
| --sourcemaps | true | false |
| --extract-css | false | true |



## Reference

Ungmo, L. \(2018\). _Angular Essentials._ Gyeonggido Bucheon-si: Rubypaper

