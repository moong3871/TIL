# 4834

- counting sort

- 뒤에서 세기

- ```python
  numbers_int = list(map(int, list(input())))
  ```

# Flatten

.index

```python
while dump > 0:
        blocks[blocks.index(max(blocks))] -= 1
        blocks[blocks.index(min(blocks))] += 1
        dump -= 1
        if max(blocks) - min(blocks) <= 1:
            break
            
    res = max(blocks) - min(blocks)
```

