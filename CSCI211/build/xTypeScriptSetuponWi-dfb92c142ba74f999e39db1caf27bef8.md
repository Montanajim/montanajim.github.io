# TypeScript Setup on Windows

### A Classroom Handout for Beginning JavaScript Students

## Overview

TypeScript is **not built into the browser**. Browsers run **JavaScript**, not raw TypeScript. To use TypeScript, you write code in `.ts` files, use the TypeScript compiler to convert that code into JavaScript, and then run the resulting `.js` file. The official TypeScript documentation describes TypeScript as compiling to JavaScript, and the official installation instructions use npm to install the compiler. ([TypeScript Download](https://www.typescriptlang.org/download/))

## What You Need

To begin working with TypeScript on Windows, you need three things.

You need **Visual Studio Code** or another code editor so you can write and edit your files. Microsoft provides the standard Windows installer for VS Code. ([VS Code Download](https://code.visualstudio.com/download))

You need **Node.js**, which includes both the Node runtime and **npm**, the package manager used to install TypeScript. The official Node.js site provides Windows installers and identifies its LTS releases. ([Node.js Download](https://nodejs.org/en/download))

You need the **TypeScript compiler**, which is installed through npm. The official TypeScript site documents the installation command and the use of `tsc`. ([TypeScript Download](https://www.typescriptlang.org/download/))

## Step 1: Install Visual Studio Code

Download and install **Visual Studio Code for Windows** from Microsoft’s official website. This gives you a clean editor for writing `.ts` and `.js` files. ([VS Code Download](https://code.visualstudio.com/download))

## Step 2: Install Node.js

Download and install **Node.js for Windows** from the official Node.js website. For student use, the best choice is usually the **LTS** version because it is more stable and is the normal classroom recommendation unless you have a specific reason to use the newest release. ([Node.js Download](https://nodejs.org/en/download))

After installation, open **Command Prompt** or **PowerShell** and test whether Node and npm are available:

```bash
node -v
npm -v
```

If both commands display version numbers, the installation worked.

## Step 3: Install TypeScript

Open **Command Prompt** or **PowerShell** and run this command:

```bash
npm install -g typescript
```

This installs the TypeScript compiler globally so you can use the `tsc` command from any folder. The official TypeScript installation page documents this exact command. ([TypeScript Download](https://www.typescriptlang.org/download/))

Then verify the installation:

```bash
tsc -v
```

If a version number appears, TypeScript is installed correctly.

## Step 4: Create a Project Folder

Create a folder for your work and move into it:

```bash
mkdir ts-demo
cd ts-demo
```

This is where you will store your TypeScript files.

## Step 5: Create Your First TypeScript File

Create a file named `app.ts` and place this code inside it:

```typescript
function greet(name: string): string {
  return `Hello, ${name}`;
}

console.log(greet("James"));
```

This program defines a function named `greet`. The parameter `name` is declared as a `string`, and the function is declared to return a `string`.

## Step 6: Compile the TypeScript File

Run the TypeScript compiler:

```bash
tsc app.ts
```

This command generates a JavaScript file named `app.js`.

That point matters. The browser does **not** run `app.ts`. It runs `app.js`. TypeScript checks the types, removes the TypeScript-only syntax, and outputs plain JavaScript. ([TypeScript Download](https://www.typescriptlang.org/download/))

## Step 7: Run the JavaScript File

To run the compiled program with Node, type:

```bash
node app.js
```

You should see this output:

```text
Hello, James
```

## How the Process Works

The real workflow looks like this:

**Write TypeScript**
→ **Compile with `tsc`**
→ **Get JavaScript output**
→ **Run the JavaScript**

That is the mental model students need to keep straight. TypeScript is the source language you write. JavaScript is the language that actually runs.

## Key Point

TypeScript is a **development tool and language extension**. JavaScript is the **runtime language**.

## A Better Setup for Real Projects

Once you move beyond a single file, create a TypeScript configuration file:

```bash
tsc --init
```

This generates a `tsconfig.json` file. The TypeScript documentation presents this as the standard way to manage project-wide compiler settings. ([TypeScript Docs](https://www.typescriptlang.org/docs/))

A beginner-friendly example looks like this:

```json
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "ES2020",
    "strict": true,
    "outDir": "dist"
  }
}
```

This file tells TypeScript how to compile the project. For example, `outDir` places the output in a folder named `dist`, and `strict` enables stronger type checking.

Once you have a `tsconfig.json`, you can usually compile the project with:

```bash
tsc
```

## Common Mistake

A very common beginner error is to think that VS Code alone is enough to run TypeScript.

It is not.

VS Code is the editor. Node.js provides the environment and npm. TypeScript provides the compiler. Remove any one of those pieces and the workflow breaks.

## Common Mistake

Another common mistake is trying to place a `.ts` file directly into an HTML page like this:

```html
<script src="app.ts"></script>
```

That is wrong. Browsers do not understand TypeScript syntax such as `: string`. They expect JavaScript. The code must be compiled first.

## Debugging Note

If `tsc` is “not recognized” in the terminal, one of two things is usually wrong.

Either TypeScript was not installed successfully, or Node/npm is not installed correctly.

That problem is not mysterious. It is almost always a missing installation step.

## Quick Start Version

For students who want the bare minimum, the process is this:

```bash
node -v
npm -v
npm install -g typescript
tsc -v
mkdir ts-demo
cd ts-demo
tsc app.ts
node app.js
```

That is enough to get started.

## Final Takeaway

TypeScript is not built into the browser, and it does not replace JavaScript. It sits in front of JavaScript. You write TypeScript, the compiler checks it and converts it, and then the browser or Node runs the JavaScript output. If students understand that chain clearly, the rest of the setup stops feeling magical and starts feeling logical.

## Official References

TypeScript installation: https://www.typescriptlang.org/download/
TypeScript documentation: https://www.typescriptlang.org/docs/
Node.js download: https://nodejs.org/en/download
VS Code download: https://code.visualstudio.com/download

