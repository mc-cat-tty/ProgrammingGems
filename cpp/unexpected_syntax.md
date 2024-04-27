# Unexpeced syntax
## Mutable attibutes
Not only lambda bodies can be mutable, but also object attributes.

```C++
struct Foo {
	mutable int count;
	void test() const { count = 10; }
} 
```

Mutable attributes can be modified by constant member functions, as well as from an external writing access.

## Global scope access operator
`::f()` allows to exit from current namespace/class and invoke a method defined in the global scope. It is needed in case matching function-method names (the whole signature is not taken into account), like in the following snippet:
```C++
void run(const Instruction &i) { ... }

PreservedAnalyses TestPass::run(Function &f, FunctionAnalysisManager &am) {
  [...]

  outs() << "PRINTING UD-DU CHAINS\n";
  for (const auto &bb : f) {
    bbCounter++;
    for (const auto &i : bb) {
      ::run(i);  // Look here
      instrCounter++;
      if (dyn_cast<CallInst>(&i)) {
        callInstrCounter++;
      }
    }
  }

  [...]
}

PreservedAnalyses TestPass::run(Module &m, ModuleAnalysisManager &am) { ... }
```
