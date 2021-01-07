---
layout: post
title:      "How to CreateYour First Project with TypeScript"
date:       2021-01-07 03:21:28 +0000
permalink:  how_to_createyour_first_project_with_typescript
---


## What is TypeScript?
TypeScript is a superset of the JavaScript language, developed and maintained by Microsoft. It utilizes a type system to assist in error handling increase development efficiency.

Have you been studying TypeScript?

Not sure how to implement it into an actual project?

This tutorial is for you!

## To Begin
Create your project folder, then navigate inside.

```
mkdir first-typescript-project
cd first-typescript-project
```

Create a package.json file.

`npm init --yes`

## Install Node Packages

Add TypeScript as a dev dependency.

```
npm install --save-dev typescript
```

Install tsc-watch. This program watches for changes to your TypeScript files and reloads upon on detection.

```
npm install --save-dev tsc-watch
```

Both packages will be saved into a node_modules folder.

## Create a tsconfig.json File

This is where the TypeScript compiler options will be defined. To create a tsconfig.json, run the following:

```
npx tsc --init --rootDir src --outDir build \
--esModuleInterop --resolveJsonModule --lib es6 \
--module commonjs --allowJs true --noImplicitAny true
```

The command is courtesy of Khalil Stemmler's TypeScript tutorial, which also provides an excellent breakdown of all the flags:

> **rootDir**: This is where TypeScript looks for our code. We've configured it to look in the src/ folder. That's where we'll write our TypeScript.
> 
> **outDir**: Where TypeScript puts our compiled code. We want it to go to a build/ folder.
> 
> **esModuleInterop**: If you were in the JavaScript space over the past couple of years, you might have recognized that modules systems had gotten a little bit out of control (AMD, SystemJS, ES Modules, etc). For a topic that requires a much longer discussion, if we're using commonjs as our module system (for Node apps, you should be), then we need this to be set to true.
> 
> **resolveJsonModule**: If we use JSON in this project, this option allows TypeScript to use it.
> 
> **lib**: This option adds ambient types to our project, allowing us to rely on features from different Ecmascript versions, testing libraries, and even the browser DOM api. We'd like to utilize some es6 language features. This all gets compiled down to es5.
> 
> **module**: commonjs is the standard Node module system in 2019. Let's use that.
> 
> **allowJs**: If you're converting an old JavaScript project to TypeScript, this option will allow you to include .js files among .ts ones.
> 
> **noImplicitAny**: In TypeScript files, don't allow a type to be unexplicitly specified. Every type needs to either have a specific type or be explicitly declared any. No implicit anys.

For the sake of this tutorial, we'll need to add "DOM" to "lib", like so:

```
"lib": ["es6", "DOM"],
```

## Create the src Folder and First TypeScript File
Now, let's create the ./src folder that will house the main TypeScript file.

```
mkdir src
```

Create the index.ts file inside the src folder.

```
touch src/index.ts
```

Then, add the following code to the src/index.ts file.

```
document.addEventListener("DOMContentLoaded", function() {
    sayGreeting();
});

const sayGreeting = (): void => {
    setTimeout(function() {
        let greeting: HTMLElement = document.createElement("p");
        greeting.innerText = "I'm using TypeScript!";
        document.getElementById('info')?.appendChild(greeting);
    }, 3000)
}
```

Let's write some quick code to make sure our program is working. Navigate to the root directory and create an index.html file. Copy and paste the following code:

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <h2>Hello World</h2>
    <div id="info">

    </div>
    <script src="build/index.js"></script>
</body>
</html>
```

## Compiling Your Code
To compile your code simple run:

```
npx tsc
```

Open index.html in the browser. Wait 3 seconds. When you see "I'm using TypeScript" you'll know your program is working!

The compiled code can be found inside ./build/index.js.

You did it!

