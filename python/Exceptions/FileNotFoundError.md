## Exception

```python
data = open("file", "r")
```
**Error**
```bash
FileNotFoundError: [Errno 2] No such file or directory: '__file__'
```

### Solution 1

```python
open(r"__relative_path__", "r")
```