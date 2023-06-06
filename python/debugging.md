# Debugging

## Interactive mode
```bash
python3 -i script.py
```

## Disassembler
```python
import dis
dis.dis(function)
```

## Breakpoint
You might want to put a breakpoint to stop the execution of a script at a precise line of code. Just write this and then run the script as usual:
```python
breakpoint()
```

## Backtrace
```python
import traceback
traceback.print_stack()
traceback.print_exc()
```

## Reloading
```python
import importlib
importlib.reload(MODULE)
```

## Inspect
```python
import inspect

inspect.getsource(function)
inspect.signature(function)
```
