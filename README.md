# SampleTinymceAngularHybrid

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 12.2.13.

The goal of this project is to serve as a template for projects using a self-hosted version of TinyMCE while loading premium plugins from the cloud.

To load premium plugins we need to "patch" the TinyMCE instance with the plugins from the cloud. We want to avoid the `tinymce-angular` wrapper creating new instance from the cloud so we generate the instance on the application `index.html` file.

## Bundling the Self-hosted hybrid configuration

1. First install TinyMCE and the `tinymce-angular` wrapper from npm

```
yarn add tinymce
yarn add @tinymce/tinymce-angular
```

2. After installing, we need to allow access to the TinyMCE code. In our `angular.json` file (lines 28 to 32 from this repo) we will specify the tinymce folder 

```
{ "glob": "**/*", "input": "./node_modules/tinymce/", "output": "/assets/" }
```

3. Next, we will load the TinyMCE script and the premium plugins in our application by adding the following lines in our `index.html` file (lines 9 and 10 in src/app/index.html). Don't forget to use your api key in the second line.

```
  <script src="assets/tinymce.min.js" type="application/javascript"></script> 
  <script src="https://cdn.tiny.cloud/1/<your_api_key>/tinymce/5/plugins.min.js" referrerpolicy="origin"></script> 
```

4. Finally, we can use the component by importing the `EditorModule` into our app (line 3 and 13 in src/app/app.module.ts).

```
import { EditorModule } from '@tinymce/tinymce-angular';

...
imports: [BrowserModule, EditorModule]
...
```

5. Now we can use the editor in our components (line 2 to 6 in src/app/app.component.html) and have access to our premium plugins from cloud!

```
<editor [init]="{
  toolbar: 'undo redo | spellchecker link | help',
  plugins: 'tinymcespellchecker advcode help link',
  spellchecker_dialog: true
}"></editor>
```


## Development server

Run `ng serve` for a dev server. Navigate to `http://localhost:4200/`. The app will automatically reload if you change any of the source files.

## Build

Run `ng build` to build the project. The build artifacts will be stored in the `dist/` directory.