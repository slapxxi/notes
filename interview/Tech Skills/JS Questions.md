** Q:  What's the difference between `var`, `let`, and `const`? **
> `var` is function-scoped with an initial value of `undefined`. `let` and `const` are block-scoped and not accessible before declaration due to the temporal dead zone. The main difference between `let` and `const` is that `const` prevents reassignment, though it doesn't make objects immutable.

** Q:  Explain the concept of closures **
> A closure happens when an inner function remembers variables from its outer function even after that outer function has finished executing. It's used for data privacy, memoization, and maintaining state between function calls.

** Q:  What's the event loop? **
> The event loop is the mechanism that allows JavaScript to handle asynchronous tasks in a single-threaded environment. It executes tasks from the call stack, then processes microtasks and macrotasks in order.
>
> In more detail.
> 
> The mechanism that allows async operations to be handled in a single-threaded environment. Since JS runs on one thread, it can't actually execute multiple pieces of code at the same time. It uses the event loop to manage tasks.
> 
> All sync code goes into the call stack and runs immediately. Meanwhile, async tasks - like `setTimeout`, promises, event listeners - are sent to Web APIs. Once those tasks are completed, their callbacks are placed in either the callback queue or the microtask queue.
>
> The event loop constantly checks whether the call stack is empty. If it is, it pushes tasks from the microtask queue first then from the callback queue.
> 
> It is what lets JS appear multitask by queuing  and scheduling work, even though it's single threaded.

** Q:  What's the difference between `==` and `===`? **
> `==` performs type coercion before comparison, while `===` compares both value and type directly. Using `===` is a best practice because it avoids unexpected type conversions.

** Q:  How does `this` works in JavaScript? **
> The value of `this` depends on how a function is called - in the global context it refers to `window` (or `undefined` in strict mode), in object methods it refers to that object, and in event listeners it usually refers to the element. Arrow functions don't bind their own `this`; they inherit it *lexically*.