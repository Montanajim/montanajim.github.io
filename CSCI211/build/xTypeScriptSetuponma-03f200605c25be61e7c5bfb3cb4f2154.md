# TypeScript Setup on macOS and iPadOS

### A Classroom Handout for Beginning JavaScript Students

## Overview

TypeScript is **not built into Safari or any other browser**. Browsers run **JavaScript**, not raw TypeScript. To use TypeScript, you write code in `.ts` files, use the TypeScript compiler to convert that code into JavaScript, and then run the resulting `.js` file. The official TypeScript documentation describes the normal setup as installing TypeScript through npm and using the `tsc` compiler. ([TypeScript](https://www.typescriptlang.org/download/?utm_source=chatgpt.com))

## What You Need on a Mac

For a normal macOS setup, students need three things:

You need **a code editor**, such as Visual Studio Code. Microsoft provides a macOS download and a macOS setup page. ([Visual Studio Code](https://code.visualstudio.com/download?utm_source=chatgpt.com))

You need **Node.js**, which provides both the Node runtime and **npm**, the package manager used to install TypeScript. The official Node.js download page currently offers macOS downloads and lists LTS releases. ([Node.js](https://nodejs.org/en/download?utm_source=chatgpt.com))

You need the **TypeScript compiler**, installed through npm with the standard global install command documented on the official TypeScript site. ([TypeScript](https://www.typescriptlang.org/download/?utm_source=chatgpt.com))

## Step 1: Install Visual Studio Code on macOS

Download and install **Visual Studio Code for macOS** from Microsoft’s official site. Microsoft’s macOS setup documentation describes the normal install path and notes that you can add additional components such as Node.js and TypeScript after installing VS Code. ([Visual Studio Code](https://code.visualstudio.com/download?utm_source=chatgpt.com))

## Step 2: Install Node.js on macOS

Download and install **Node.js for macOS** from the official Node.js site. For student use, the smart default is an **LTS** release rather than the newest current release, unless you have a specific reason to live dangerously. The current official Node download page lists LTS releases and macOS installers. ([Node.js](https://nodejs.org/en/download?utm_source=chatgpt.com))

After installation, open **Terminal** and verify Node and npm:

```bash
node -v
npm -v
```

If both commands print version numbers, the installation worked.

## Step 3: Install TypeScript on macOS

In Terminal, run:

```bash
npm install -g typescript
```

The official TypeScript installation page documents this command as the standard way to install TypeScript globally so that `tsc` is available anywhere in Terminal. ([TypeScript](https://www.typescriptlang.org/download/?utm_source=chatgpt.com))

Then verify the installation:

```bash
tsc -v
```

If a version number appears, TypeScript is installed correctly.

## Step 4: Create a Project Folder

In Terminal, create a folder and move into it:

```bash
mkdir ts-demo
cd ts-demo
```

## Step 5: Create Your First TypeScript File

Create a file named `app.ts` and add this code:

```typescript
function greet(name: string): string {
  return `Hello, ${name}`;
}

console.log(greet("James"));
```

## Step 6: Compile the TypeScript File

Run:

```bash
tsc app.ts
```

This generates a JavaScript file named `app.js`.

That is the point students need to keep straight: **Safari does not run `app.ts`; it runs JavaScript**. TypeScript checks the code, removes the TypeScript-only syntax, and emits JavaScript. ([TypeScript](https://www.typescriptlang.org/download/?utm_source=chatgpt.com))

## Step 7: Run the JavaScript File

To run the compiled code with Node:

```bash
node app.js
```

You should see:

```text
Hello, James
```

## How the Process Works

The real workflow is:

**Write TypeScript**
→ **Compile with `tsc`**
→ **Get JavaScript output**
→ **Run the JavaScript**

That is true on macOS just as it is on Windows. TypeScript is the source language. JavaScript is the runtime language. ([TypeScript](https://www.typescriptlang.org/download/?utm_source=chatgpt.com))

## Key Point

On a Mac, TypeScript is still **not a browser-native language**. You need Node.js and the TypeScript compiler.

## Optional Project Setup with `tsconfig.json`

For anything beyond a single demo file, create a TypeScript configuration file:

```bash
tsc --init
```

The TypeScript docs present `tsconfig.json` as the normal project-level configuration mechanism. ([TypeScript](https://www.typescriptlang.org/download/?utm_source=chatgpt.com))

A beginner-friendly example is:

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

Then compile the project with:

```bash
tsc
```

## iPadOS / iOS: The Blunt Truth

Here is the part most handouts dodge: **an iPhone or iPad is not the same as a Mac for local TypeScript development**.

On **macOS**, students can install Node.js, npm, and TypeScript locally in the normal way. That is the clean path. ([Node.js](https://nodejs.org/en/download?utm_source=chatgpt.com))

On **iPadOS or iOS**, the normal classroom setup is **not** to install a full local Node + TypeScript toolchain the same way you do on a Mac. The practical choices are usually:

Use a **web-based development environment** in the browser.

Use an **online TypeScript playground** for small examples. The official TypeScript site explicitly offers “Try TypeScript Now” online. ([TypeScript](https://www.typescriptlang.org/?utm_source=chatgpt.com))

Use a **remote development environment** or cloud IDE if the course supports it.

That means for serious coursework, **a Mac is the correct machine**. An iPad can be useful for light experiments, quick demos, or browser-based coding, but it is not the best primary platform for a first programming course that expects installation, terminal use, and local compilation.

## Common Mistake

A common beginner error is to assume that owning Apple hardware means the setup is the same on all Apple devices.

It is not.

**macOS** is a desktop operating system with a normal local development workflow.
**iPadOS/iOS** is a mobile operating system with a more limited local developer workflow.

Treating them as equivalent is how students end up annoyed, blocked, and blaming the wrong thing.

## Common Mistake

Another common mistake is trying to load a `.ts` file directly in HTML:

```html
<script src="app.ts"></script>
```

That is wrong on Mac, Windows, or anything else with a browser. Browsers expect JavaScript, not TypeScript syntax. ([TypeScript](https://www.typescriptlang.org/download/?utm_source=chatgpt.com))

## Debugging Note

If Terminal says `tsc: command not found`, one of the following is wrong:

Node.js was not installed correctly.

TypeScript was not installed correctly.

The terminal session does not see the installed npm global tools yet.

Most of the time, the problem is not mysterious. It is a missing installation step or a path issue.

## Quick Start Version for macOS

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

That is enough to get a student started on a Mac.

## Recommendation for Students

If a student has a **Mac**, use the normal local setup with VS Code, Node.js, and TypeScript.

If a student has only an **iPad or iPhone**, use the official online TypeScript playground or another browser-based environment for small assignments and demonstrations, but do not pretend that this is equivalent to a full local Mac workflow. That claim has holes big enough to drive a lab cart through. ([TypeScript](https://www.typescriptlang.org/?utm_source=chatgpt.com))

## Final Takeaway

For **macOS**, the TypeScript workflow is straightforward: install VS Code, install Node.js, install TypeScript, write `.ts` files, compile with `tsc`, and run the generated JavaScript.

For **iPadOS/iOS**, the realistic path is usually browser-based or remote, not a standard local desktop toolchain.

## Official References

TypeScript installation: https://www.typescriptlang.org/download/ ([TypeScript](https://www.typescriptlang.org/download/?utm_source=chatgpt.com))
TypeScript home and online playground: https://www.typescriptlang.org/ ([TypeScript](https://www.typescriptlang.org/?utm_source=chatgpt.com))
Node.js download: https://nodejs.org/en/download ([Node.js](https://nodejs.org/en/download?utm_source=chatgpt.com))
VS Code download: https://code.visualstudio.com/download ([Visual Studio Code](https://code.visualstudio.com/download?utm_source=chatgpt.com))
VS Code macOS setup: https://code.visualstudio.com/docs/setup/mac ([Visual Studio Code](https://code.visualstudio.com/docs/setup/mac?utm_source=chatgpt.com))

