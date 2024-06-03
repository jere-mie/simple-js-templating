# Simple JS Templating System

A relatively small and simple templating system for small websites that want templating capabilities without setting up a build system or JavaScript framework like Svelte or React.

Created by Isaac Kilbourne ([@kilbouri](https://github.com/kilbouri)). Hosted on GitHub by Jeremie Bornais, because Isaac didn't want to create a separate repository for it. You can find Isaac's original GitHub Gist for it [here](https://gist.github.com/kilbouri/c76df10a416ee8a7e0462da69f7a27fc).

## Features

- Stand-alone source file with no dependencies
- Easy to use with small websites
- Provides templating capabilities similar to larger frameworks

## Installation

Simply download include the JS file in your project. By default, this file is a JS module. To use it as a regular JS script, remove the export line near the beginning of the file.

### CDN

You can also include the JS file via CDN, like so:

```html
<script type="module" src="https://jere-mie.github.io/simple-js-templating/templating.js"></script>
```

Or for the minified version (no docs but smaller file size):

```html
<script type="module" src="https://jere-mie.github.io/simple-js-templating/templating.min.js"></script>
```

It's recommended to download and install the file locally, however, as it's more stable and gives you ownership of your code.

## Usage

### Importing the Module

If using as a module, import the functions in your JS file:

```javascript
import { findTemplate, findContainer, instantiateTemplate } from './path/to/templating.js';
```

### Functions

#### `findTemplate(templateName)`

Finds a `<template>` element with the `data-templateName` attribute containing the provided template name.

- **Parameters:**
  - `templateName` (string): The name of the template to find.
- **Returns:** 
  - The first `<template>` DOM element with matching template name, if it exists.

#### `findContainer(containerName)`

Finds any element with the `data-containerName` attribute containing the provided container name.

- **Parameters:**
  - `containerName` (string): The name of the container to find.
- **Returns:** 
  - The first DOM element with matching container name, if it exists.

#### `instantiateTemplate(templateElement, fillParams)`

Clones the provided `<template>` element's content and replaces the contained elements with a `data-fieldName` attribute based on the `fillParams`.

- **Parameters:**
  - `templateElement` (HTMLTemplateElement): The template to clone.
  - `fillParams` (TemplateFillParams): A mapping of fieldNames to attribute values.
- **Returns:** 
  - A `DocumentFragment` which can be inserted anywhere in the DOM to display the instantiated template on the page.

### Example

Below is a simple example to demonstrate how to use the templating system.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Templating Example</title>
</head>
<body>
  <template data-templateName="exampleTemplate">
    <div>
      <h1 data-fieldName="title"></h1>
      <p data-fieldName="content"></p>
    </div>
  </template>

  <div data-containerName="exampleContainer"></div>

  <script type="module">
    import { findTemplate, findContainer, instantiateTemplate } from './templating.js';

    const template = findTemplate('exampleTemplate');
    const container = findContainer('exampleContainer');
    const fillParams = {
      title: [['innerHTML', 'Hello, World!']],
      content: [['innerHTML', 'This is an example content.']]
    };

    if (template && container) {
      const instance = instantiateTemplate(template, fillParams);
      container.appendChild(instance);
    }
  </script>
</body>
</html>
```

In this example, the template is defined in the HTML file, and JavaScript is used to instantiate and fill the template, then append it to the container.

#### Live Demo

Check out a live demo of the example site [here](example.html)

## Author

Isaac Kilbourne
