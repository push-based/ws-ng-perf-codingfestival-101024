# JS Event Loop Exercise

The goal of this exercise is to deepen your knowledge about the javascript event loop,
the difference between micro- and macrotasks and the execution timings of different
scheduling APIs.

Please write a function that results in the following flamechart.

You can use this plain javascript example as a starting point for your exercise.
[exercise template](https://stackblitz.com/edit/js-v6rset?file=index.js).

> [!NOTE]
> It's also possible to run this exercise by checking out the [js playground project.](https://github.com/push-based/js-playground)
> Use that one if you have problems with stackblitz

![img.png](images/event-loop/event-loop-exercise.png)


<details>
  <summary>Scheduling APIs</summary>

```ts
// scheduling APIs

setTimeout();
Promise.resolve();
queueMicrotask();
window.requestIdleCallback();
requestAnimationFrame();
```

</details>


<details>
  <summary>Solution</summary>

```ts

// doesn't matter where
requestIdleCallback(() => {
  doWork();
})

requestAnimationFrame(() => {
  queueMicrotask(() => {
    doWork();
  })
  doWork();
})
requestAnimationFrame(() => {
  doWork();
})

setTimeout(() => {
  doWork();
  queueMicrotask(() => {
    doWork();
  })
  // move the rAF after the settimeout
  requestAnimationFrame(() => {
    doWork();
  })
})

```
</details>

