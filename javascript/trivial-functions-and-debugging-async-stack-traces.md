It can be _very_ difficult to debug an issue when a given module/file whose context can help you understand the source of the issue is using functions from other modules/files but no functions of its own. 

Why? 

Because the other modules/files are where the problem becomes manifest, but the stack trace will not necessarily clearly show you in what context (file, page, module) the problem occurred, especially when you're dealing with asynchronous functionality or libraries that wrap your code (e.g. frameworks with nasty digest cycles like AngularJS, analytics tools like [New Relic](https://newrelic.com/), error tracking tools like [Sentry](https://getsentry.com/welcome/), etc.)

So what's one way to remedy this problem?

Create "trivial" functions that wrap the functions of the other modules/files you really care about just to get more context in the stack trace.

For a contrived, abstract example that probably won't clarify anything...

Let's say Module A represents a component that manages your view (e.g. an AngularJS controller). Module A imports Module B and Module C. Module B is a 3rd-party data service library with at least one asynchronous web request function that's promise based called `fetch`. Module C is a 3rd-party utility library with all sorts of fancy _pure_ functions (Yay! No side effects! FTW!).

```javascript
// Module A
// Ignore that there is no function wrapper or defined class--just assume it's an appropriately scoped module.

import b from './moduleB';
import c from './moduleC';

const data = [...];

b.fetch(data)
  .then(c.filterAndSortItems);
```

Now let's say that `c.filterAndSortItems` throws an error: `Cannot read property 'name' of undefined`. Well, assuming `filterAndSortItems` is a single, pure function, that error will be caught or thrown by Module B since Module B's `then` is the caller of Module C's `filterAndSortItems`. And this is where it gets tricky and interesting.

At this point, your call stack is probably broken up in your dev tools because, as mentioned above, Module B's `fetch` function makes an asynchronous web request and the stack dev tools will probably pick up the stack trace where the response is received and if you have other libraries wrapping your code, it can be very difficult to see what module/file called `b.fetch` in the first place. Not frustrating at all. 

Furthermore, Module B's `then` function is a black box. You may know _what_ it does, that's why you're using it, but you may NOT know _how_ it does what it does. It may be calling _dozens_ of other methods internally that are all added to your stack trace just amplifying the noise you have to ignore when looking for the module/file that you own and have control over and that caused the problem (let's assume) because `data` had some bad data!

*Takes deep breath.*

Soooo. This example is probably far too contrived to follow and it's significantly abstract (no concrete real world libs or common uses effectively presented as of yet, only briefly mentioned), so you're probably lost and wondering if this has ever happened to you or ever will. Maybe, maybe not.

But there's an easy fix to the problem.

> Create "trivial" functions that wrap the functions of the other modules/files you really care about just to get more context in the stack trace.

```javascript
b.fetch(data)
  .then((response) => c.filterAndSortItems(response));
```

That's it. All that does is add another place in the stack trace where a function is called from Module A (i.e. your module) so that when Module C's (i.e. a third party lib or separate file) function fails, you know what file to look in for potential problems.

Is it uglier? Yes.

Is it less succinct? Yes.

Does it feel redundanct? Yes.

Will it affect performance *gasp*? Maybe. Will that matter? Do I dare say...probably not? Depends on your scenario.

Has this helped me have async stack traces that are oodles more helpful? Yes, yes, a thousand times yes!

Are there significant problems or gotchas with this? Not that I know of.

Can it be improved further? Perhaps. If you don't like anonymous functions, you could used a named function declaration (e.g. function doFilterAndSortItems() {...}).

Are there other ways to avoid this problem of "hard to read stack traces"? Probably are. In fact there may be something else I'm missing that might help and be a better solution! Let me know in the comments *pretty* please!
