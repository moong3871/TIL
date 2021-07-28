# zip(*list)

> 동일한 개수로 이루어진 자료형을 묶어주는 역할을 하는 python 내장함수

`*` = `unpack a list`(or other iterable)

```python
li = [[1,2,3], [4,5,6]]

zip(li) #= zip([[1,2,3], [4,5,6]])
list(zip(li))#=> [([1,2,3],),([4,5,6],) ]

zip(*li) #= zip([1,2,3], [4,5,6])
list(zip(*li))#=> [(1,4),(2,5),(3,6)]
```

