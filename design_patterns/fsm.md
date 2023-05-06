# Design patterns about finite state machines

## Neat implementation
```c
typedef enum FsmState {
    ENTRY,
    FIRST,
    SECOND,
    EXIT,
} FsmState;

FsmState currentState;

// Each method does sth and returns the next state
FsmState entry(void *params);
FsmState first(void *params);
FsmState second(void *params);
FsmState exit(void *params);

FsmState nextState(void *params);  // constains the switch case

void fsmRun(void *params) {
    currentState = nextState(params);
}

FsmState nextState(void *params) {
    switch (currentState) {
        case ENTRY: return entry(params);
        case FIRST: return first(params);
        ...
    }
}
```
