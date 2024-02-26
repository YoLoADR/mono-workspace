# MonoWorkspace

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 16.0.1.

## Development server

Run `ng serve` for a dev server. Navigate to `http://localhost:4200/`. The application will automatically reload if you change any of the source files.

## Code scaffolding

Run `ng generate component component-name` to generate a new component. You can also use `ng generate directive|pipe|service|class|guard|interface|enum|module`.

## Build

Run `ng build` to build the project. The build artifacts will be stored in the `dist/` directory.

## Running unit tests

Run `ng test` to execute the unit tests via [Karma](https://karma-runner.github.io).

## Running end-to-end tests

Run `ng e2e` to execute the end-to-end tests via a platform of your choice. To use this command, you need to first add a package that implements end-to-end testing capabilities.

## Further help

To get more help on the Angular CLI use `ng help` or go check out the [Angular CLI Overview and Command Reference](https://angular.io/cli) page.


# Tutorial

## Create a new workspace without app
ng new mono-workspace --no-create-application

## Create host or shell app
ng g application host-app --routing --style=scss

## Create mde
ng g application mfe-app --routing --style=scss

## Install Webpack, Webpack CLI and concurrently ( to run multiple scripts concurrently )
npm i webpack webpack-cli concurrently --save-dev


### A
changer les fichier app.component.html
    projects/host-app/src/app/app.component.html
    <div><span>This is Shell App</span></div>

    projects/mfe-app/src/app/app.component.html
    <div><span>This is remote MFE app</span></div>

"host-app": "ng serve host-app --configuration development --port 4200 -o",
    "mfe-app": "ng serve mfe-app --configuration development --port 4300 -o",
    "start": "concurrently \"npm run host-app\" \"npm run mfe-app\"",

### B

ng add @angular-architects/module-federation@16 --project mfe-app --port 4300
ng add @angular-architects/module-federation@16 --project host-app --port 4200


### C
projects/host-app/webpack.config.js
name: "hostApp",
remotes: {
            "mfeApp": "http://localhost:4200/remoteEntry.js",

projects/mfe-app/webpack.config.js
name: "mfeApp",
        filename: "remoteEntry.js",
        exposes: {
            './Component': './projects/mfe-app/src/app/app.component.ts',
        },     
