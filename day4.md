A little update and reason why this is paused for a while. Had an interview recently and got the offer! But due to the reason my H1B is not activated yet and the offer cannot be extended to October, I must reject it😭. I really want to go, it pays also three times as what I have right now. Guess this is what all 1st generation immigrants must experience. Anyway, let's move on to dive into react source code.

First have a review what we have done so far.

## review
- before **React15**, render was synchronous and uninterruptible.
- Algebraic Effects is to split side effects from the function
    - in **React**, it is used in hooks to call synchronous functions in asynchronous styles
    - Pause anywhere in a program, send a request outside, and later resume cleanly, keeping logic and side effects separated
    - like when reading from database, in normal function call flow, we call function -> implement read database -> get data. But with algebraic effects we run function -> declare read database effects (no need to implement it) -> handlers capture the effect and return data to the function -> resume where the function is left.
- Fiber
    - Static instance of an element
    - Working information

