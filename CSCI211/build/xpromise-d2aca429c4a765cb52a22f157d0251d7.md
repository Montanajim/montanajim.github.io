1. # Chapter: Understanding JavaScript Promises

   ## Introduction

   Modern JavaScript depends heavily on asynchronous programming. A program may need to wait for a timer, a web request, a file operation, or a database transaction, yet the rest of the application must continue running. JavaScript cannot afford to freeze every time it waits. It needs a way to represent work that has started now but will finish later.

   Promises provide that mechanism. A Promise is a built-in JavaScript object that represents the eventual result of an operation. That result may be a success value, or it may be a failure reason. Before Promises became standard, JavaScript developers often managed asynchronous work with callbacks alone. That method worked, but as programs grew, callback-based code became increasingly difficult to read, test, debug, and maintain.

   Promises improved the situation by giving JavaScript a standard, structured model for future results. They made asynchronous code more readable, made error handling more consistent, and laid the foundation for modern features such as `async` and `await`. This chapter explains why Promises matter, how they work, how to use them correctly, and where students most often go wrong.

   ------

   ## Chapter at a Glance

   This chapter introduces JavaScript Promises as the standard way to represent future results in asynchronous programming. It explains why Promises were adopted, how their states work, how `.then()` and `.catch()` are used, and how `async` and `await` build on the same foundation.

   Students who understand this chapter should be able to read Promise-based code without confusing the Promise object with its eventual result. That sounds small, but it is the hinge on which most beginner understanding turns.

   ## Learning Goals

   By the end of this chapter, you should be able to:

   - explain why Promises were adopted in JavaScript
   - identify the three Promise states
   - distinguish between a Promise and its eventual result
   - use `.then()` and `.catch()` correctly
   - explain how `async` and `await` relate to Promises
   - recognize common Promise mistakes in beginner code

   ------

   ## 1. Why JavaScript Needed Promises

   JavaScript is event-driven by nature. In a browser, programs respond to clicks, keyboard input, timers, animations, server responses, and client-side storage systems such as IndexedDB. Many of these activities do not complete immediately. A request may take milliseconds or seconds, and JavaScript must continue doing other work in the meantime.

   Before Promises, callbacks were the main way to deal with delayed results. A callback is a function passed into another function so it can be called later. That idea is simple, but when multiple asynchronous steps depend on one another, callback-based code can become deeply nested.

   Consider the following style:

   ```javascript
   getUser(function(user) {
       getOrders(user.id, function(orders) {
           getLastOrder(orders, function(order) {
               sendReceipt(order, function(result) {
                   console.log("Done");
               }, function(error) {
                   console.log(error);
               });
           }, function(error) {
               console.log(error);
           });
       }, function(error) {
           console.log(error);
       });
   }, function(error) {
       console.log(error);
   });
   ```

   This pattern is difficult to read because the logic becomes increasingly indented and error handling must be repeated at nearly every step. The code drifts to the right, the flow becomes harder to follow, and maintenance becomes unpleasant. This problem is often called *callback hell*.

   ### Key Point

   Promises were adopted because they make asynchronous workflows easier to organize, easier to read, and easier to maintain.

   ------

   ## 2. What Problems Promises Solve

   Promises solve several practical problems in real JavaScript programs.

   They improve readability by allowing asynchronous operations to be organized in a more linear and predictable style. Instead of deeply nesting functions, developers can chain operations together.

   They improve error handling because failures can be funneled into a `.catch()` handler rather than requiring separate error logic at every step.

   They standardize delayed results. Different APIs and libraries can follow the same Promise-based pattern rather than each inventing their own custom callback conventions.

   They also make asynchronous tasks easier to combine. JavaScript can wait for multiple Promises, race them, chain them, or process them as groups.

   ### Common Mistake

   Students sometimes think Promises exist because callbacks are “bad.” That is too simplistic. Callbacks are still valid. The problem is that callbacks alone do not scale gracefully in larger asynchronous workflows.

   ------

   ## 3. The Core Idea of a Promise

   A Promise is an object that represents the eventual outcome of one operation, often an asynchronous one.

   That outcome can exist in one of three states.

   A Promise begins as **pending**. This means the operation has started, but no final outcome has been produced yet.

   A Promise becomes **fulfilled** when the operation completes successfully.

   A Promise becomes **rejected** when the operation fails.

   Once a Promise is either fulfilled or rejected, it is said to be **settled**. A settled Promise does not change again. It cannot return to pending, and it cannot switch from fulfilled to rejected or from rejected to fulfilled.

   ### Figure 1.1: Promise Lifecycle

   ```text
               Promise Created
                     |
                     v
                  PENDING
                  /     \
                 /       \
                v         v
          FULFILLED   REJECTED
   ```

   ### Checkpoint 1

   What state is a Promise in before it has either succeeded or failed?

   ### Definition Box

   **pending** — the operation has started, but no final result is ready yet
   **fulfilled** — the Promise completed successfully
   **rejected** — the Promise failed
   **settled** — the Promise is either fulfilled or rejected

   ------

   ## 4. Promise Terminology

   ### Margin Note

   Students often memorize the words `resolve` and `reject` without understanding what they do. Memorization is not enough here. The point is not the names. The point is that the Promise object represents a future outcome, and those functions determine how that outcome is settled.

   Students often confuse the Promise object with the functions surrounding it, so the vocabulary needs to be exact.

   In code such as this:

   ```javascript
   return new Promise((resolve, reject) => {
       // work here
   });
   ```

   `Promise` is the built-in JavaScript constructor.

   The function `(resolve, reject) => { ... }` is called the **executor function**. JavaScript runs the executor immediately when the Promise is created.

   `resolve` is a function supplied by JavaScript. Calling it settles the Promise with a successful outcome.

   `reject` is also supplied by JavaScript. Calling it rejects the Promise with a failure reason.

   Later, when `.then()` or `.catch()` is used, the functions passed into those methods are **handlers** or **callbacks**. Those handlers run only after the Promise has settled.

   ### Key Distinction

   A Promise is not a callback. A Promise is the object representing the future result.

   ------

   ## 5. Demo Program

   ### Figure 1.2: Browser-Based Promise Demonstration

   The following program demonstrates a Promise in a simple browser-based example. A radio button lets the user decide whether the asynchronous job should succeed or fail. A button starts the process, and the log area shows what happens.

   ```html
   <!DOCTYPE html>
   <html>
   
   <head>
   <meta charset="UTF-8">
   <meta name="viewport" content="width=device-width, initial-scale=1.0">
   <title>Promise Demo</title>
   
   <style>
   .div1
   {
       width: 75%;
       background-color: cornsilk;
       margin-left: auto;
       margin-right: auto;
       margin-top: 50px;
       margin-bottom: 50px;
       padding: 20px;
   }
   </style>
   </head>
   
   <body>
   
   <div class="div1">
   
   <h1>Promise Demo</h1>
   
   <button onclick="runExample()">Run Example</button>
   
   <input type="radio" id="yes" name="rbg" value="true" checked>Success&nbsp;
   <input type="radio" id="no" name="rbg" value="false">Failure&nbsp;
   
   <br><br>
   
   <pre id="output"></pre>
   
   <br>
   
   <button onclick="clearLog()">Clear Log</button>
   
   </div>
   
   <script>
   
   function log(msg)
   {
       document.getElementById("output").textContent += msg + "\n";
   }
   
   function doAsyncJob()
   {
       log("Creating Promise object...");
   
       return new Promise((resolve, reject) =>
       {
           log("Job started...");
   
           const choice = document.querySelector('input[name="rbg"]:checked');
   
           if (!choice)
           {
               reject(new Error("Please select Success or Failure before running the example."));
               return;
           }
   
           const success = choice.value === "true";
   
           setTimeout(() =>
           {
               if (success)
               {
                   resolve("Job finished successfully");
               }
               else
               {
                   reject(new Error("Job failed"));
               }
           }, 2000);
       });
   }
   
   function runExample()
   {
       log("Calling doAsyncJob()...");
   
       doAsyncJob()
           .then((result) =>
           {
               log("SUCCESS: " + result);
           })
           .catch((error) =>
           {
               log("ERROR: " + error.message);
           });
   
       log("Promise returned to caller.");
       log("Handlers attached with .then() and .catch().");
       log("This line runs immediately.");
   }
   
   function clearLog()
   {
       document.getElementById("output").textContent = "";
   }
   
   </script>
   
   </body>
   </html>
   ```

   ------

   ## 6. Reading the Demo Carefully

   When the user clicks **Run Example**, the `runExample()` function starts immediately. It logs the message `Calling doAsyncJob()...` and calls `doAsyncJob()`.

   Inside `doAsyncJob()`, a new Promise is created and returned. The executor function runs right away, so `Job started...` appears immediately in the log.

   The program checks which radio button is selected. If the `Success` option is selected, the variable `success` becomes `true`. If `Failure` is selected, it becomes `false`.

   Then `setTimeout()` simulates a delayed operation by waiting two seconds.

   After the delay, one of two things happens. If `success` is `true`, the Promise resolves:

   ```javascript
   resolve("Job finished successfully");
   ```

   If `success` is `false`, the Promise rejects:

   ```javascript
   reject(new Error("Job failed"));
   ```

   Back in `runExample()`, the Promise is used in a chain. The `.then()` method attaches a handler for success, and `.catch()` attaches a handler for failure.

   Meanwhile, the line `This line runs immediately.` is logged before the Promise settles. That is the central lesson: JavaScript does not stop the entire program while the Promise is pending.

   ### Teaching Note

   Beginners often expect the program to “wait” at the Promise line. It does not. The function keeps running, and the Promise handler executes later.

   ### Checkpoint 2

   In the demo, which lines run immediately, and which lines wait for the Promise to settle?

   ------

   ## 7. How `.then()` and `.catch()` Work

   The most common way to work with a Promise is through `.then()` and `.catch()`.

   ```javascript
   doAsyncJob()
       .then((result) => {
           console.log(result);
       })
       .catch((error) => {
           console.log(error);
       });
   ```

   `.then()` is most commonly used to handle fulfillment.

   `.catch()` is commonly used to handle rejection.

   More precisely, `.then()` can accept both a fulfillment handler and a rejection handler, but most real code uses `.catch()` for rejection because it reads more clearly and fits naturally into Promise chains.

   These handlers do not run immediately. They run asynchronously after the current synchronous code finishes and after the Promise settles.

   ### Common Mistake

   Calling `resolve()` does **not** mean JavaScript instantly jumps into `.then()`. The current synchronous code finishes first.

   ### Checkpoint 3

   Why is it incorrect to say that a Promise "contains the answer right now"?

   ------

   ## 8. What Happens Behind the Scenes

   The sequence of events in the demo matters.

   1. `runExample()` begins.
   2. `Calling doAsyncJob()...` is logged.
   3. `doAsyncJob()` creates a Promise.
   4. The executor function runs immediately.
   5. `Job started...` is logged.
   6. The radio button selection is read.
   7. A two-second timer begins.
   8. `.then()` and `.catch()` handlers are attached.
   9. `Promise returned to caller.` is logged.
   10. `Handlers attached with .then() and .catch().` is logged.
   11. `This line runs immediately.` is logged.
   12. Two seconds later, the timer callback runs.
   13. The Promise is resolved or rejected.
   14. The appropriate Promise handler is queued and then runs asynchronously.

   ### Instructor’s Note

   If students struggle here, the issue is usually not syntax. It is timing. Promise code is easy to read badly because the logical order and the execution order are not always the same thing.

   ------

   ## 9. A Promise Is Not the Final Result

   Students often assume that the Promise itself is the final value. That is incorrect.

   ```javascript
   const result = doAsyncJob();
   console.log(result);
   ```

   This prints a Promise object, not the finished result. Depending on the environment, it may appear as something like a pending Promise or another engine-specific representation.

   To get the actual resolved value, code must use `.then()`, `.catch()`, or `await`.

   ### Definition Box

   A Promise is a container for a future result.
   It is **not** the result itself.

   ### Figure 1.3: Promise vs. Final Value

   A Promise represents future availability.
   The fulfilled value represents the final outcome.

   ------

   ## 10. Common Mistakes and Gotchas

   ### Chapter Warning

   This section matters more than students think. Promise syntax is not usually the real problem. The real problem is faulty mental models about timing, flow, and what data is actually available at a given moment.

   ### 10.1 Forgetting to Return the Promise

   Bad code:

   ```javascript
   function doWork() {
       new Promise((resolve, reject) => {
           setTimeout(() => resolve("done"), 1000);
       });
   }
   ```

   Correct code:

   ```javascript
   function doWork() {
       return new Promise((resolve, reject) => {
           setTimeout(() => resolve("done"), 1000);
       });
   }
   ```

   Without the `return`, the Promise is created and then discarded. The caller cannot use it.

   ### 10.2 Forgetting Error Handling

   If a Promise can fail, the program should handle that failure.

   With Promise chaining, failures are usually handled with `.catch()`.

   With `await`, rejections can be handled with `try/catch` inside an `async` function.

   ### 10.3 Rejecting with a Plain String

   Rejecting with an `Error` object is usually better:

   ```javascript
   reject(new Error("Job failed"));
   ```

   An `Error` object carries better debugging information and leads to more consistent failure handling.

   ### 10.4 Assuming the Promise Pauses the Entire Program

   A Promise does not pause all JavaScript execution. Other work can continue while the Promise remains pending.

   ### 10.5 Using Shared Global State Carelessly

   Shared global state makes asynchronous code harder to reason about because multiple operations may read or change the same value at different times.

   ### Checkpoint 4

   Why is shared mutable state especially dangerous in asynchronous code?

   ------

   ## 11. Promises and `async/await`

   Modern JavaScript often uses `async` and `await`, which are built on top of Promises.

   ```javascript
   async function runExample()
   {
       log("Calling doAsyncJob()...");
   
       try
       {
           const result = await doAsyncJob();
           log("SUCCESS: " + result);
       }
       catch (error)
       {
           log("ERROR: " + error.message);
       }
   
       log("This line runs after the Promise settles inside this async function.");
   }
   ```

   This style is often easier to read because it resembles ordinary step-by-step code.

   However, `await` does not freeze the entire program. It pauses only the surrounding `async` function until the Promise settles. Other JavaScript outside that function can continue running.

   ### Comparison Box

   ### Figure 1.4: Two Ways to Work with the Same Promise

   **Promise chaining** emphasizes explicit asynchronous flow.
   **`async/await`** emphasizes readability.
   Both rely on Promises underneath.

   ------

   ## 12. Key Terms

   **asynchronous programming** — programming in which some operations finish later rather than immediately

   **Promise** — a built-in JavaScript object representing the eventual result of an operation

   **pending** — the Promise has started but has not finished

   **fulfilled** — the Promise completed successfully

   **rejected** — the Promise failed

   **settled** — the Promise is either fulfilled or rejected

   **resolve** — settle the Promise with a successful outcome

   **reject** — reject the Promise with a failure reason

   **executor function** — the function passed into `new Promise(...)`

   **handler** — a function attached with methods such as `.then()` or `.catch()`

   **callback** — a function passed into another function to be run later

   ------

   ## 13. Chapter Summary

   ### Chapter Takeaway

   Promises do not make asynchronous programming simple. They make it manageable.

   Promises were adopted because JavaScript needed a cleaner and more standardized way to manage asynchronous work. Callback-based approaches were possible, but they became messy and hard to maintain as programs grew.

   A Promise represents an eventual result. It begins in the pending state and later settles as either fulfilled or rejected.

   Handlers such as `.then()` and `.catch()` allow code to respond to that outcome after the current synchronous work finishes.

   ### Final Takeaway

   **A Promise is not the result. It represents the future result.**

   ------

   ## 14. Review Questions

   ### Quick Self-Test

   Before answering the multiple-choice questions, see whether you can explain the following in one sentence each:

   1. What problem do Promises solve?
   2. What are the three Promise states?
   3. Why is a Promise not the same thing as its final value?
   4. What is the practical difference between `.then()` and `await`?

   ### Review Questions

   ### Multiple-Choice Questions

   **1. What is the main reason Promises were adopted into JavaScript?**

   A. To replace variables with objects
   B. To make asynchronous code easier to organize and manage
   C. To eliminate functions from JavaScript
   D. To make HTML pages load faster

   **2. Which of the following is not a state of a Promise?**

   A. pending
   B. fulfilled
   C. rejected
   D. delayed

   **3. In the expression `new Promise((resolve, reject) => { ... })`, what is `(resolve, reject) => { ... }` called?**

   A. callback handler
   B. executor function
   C. Promise state
   D. event listener

   **4. What is `.then()` most commonly used for?**

   A. syntax errors only
   B. Promise fulfillment
   C. browser resizing
   D. HTML rendering

   **5. What does `.catch()` handle?**

   A. Promise rejection
   B. variable declarations
   C. browser resizing
   D. Promise creation

   **6. In the demo program, why does `This line runs immediately.` appear before the final success or failure message?**

   A. Because `.then()` always runs first
   B. Because the Promise pauses the program
   C. Because the asynchronous work finishes later while JavaScript continues running
   D. Because the radio buttons are checked after the result

   **7. Which statement about a settled Promise is correct?**

   A. It can become pending again
   B. It may switch from rejected to fulfilled
   C. It has already finished as either fulfilled or rejected
   D. It can only be used once per page

   **8. What is wrong with this code?**

   ```javascript
   function doWork() {
       new Promise((resolve, reject) => {
           setTimeout(() => resolve("done"), 1000);
       });
   }
   ```

   A. It uses `setTimeout()` incorrectly
   B. It forgets to return the Promise
   C. It resolves too quickly
   D. It should use HTML instead

   **9. Which statement is most accurate about `await`?**

   A. It pauses all JavaScript in the program
   B. It pauses only the surrounding `async` function until the Promise settles
   C. It replaces `.catch()` permanently
   D. It makes Promises unnecessary

   **10. Why is rejecting with an `Error` object usually better than rejecting with a plain string?**

   A. Strings are not allowed in JavaScript
   B. Error objects provide better debugging information
   C. Error objects make the program synchronous
   D. They prevent `.catch()` from running

   ### Answer Key

   1. **B**
   2. **D**
   3. **B**
   4. **B**
   5. **A**
   6. **C**
   7. **C**
   8. **B**
   9. **B**
   10. **B**

   ------

   ## 15. End-of-Chapter Glossary

   **Asynchronous** — not completed immediately; finishes later

   **Callback** — a function passed to another function to be executed later

   **Executor Function** — the function passed into the Promise constructor

   **Fulfilled** — the Promise succeeded

   **Handler** — a function attached to a Promise with `.then()` or `.catch()`

   **Pending** — the Promise has started but not finished

   **Promise** — an object representing a future result

   **Rejected** — the Promise failed

   **Resolve** — settle the Promise with a successful result

   **Settle** — complete the Promise as either fulfilled or rejected
