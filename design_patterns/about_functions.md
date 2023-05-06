# Design patterns about functions

## Idempotence
> Idempotent function referes to a function whose behaviour don't change across different calls (except for the first one).

Useful for data initialization inside a library.

```c
void function() {
    static bool first_execution = true;

    if (!first_execution) reutrn;

    ...  // Do something

    first_execution = false;
}
```
