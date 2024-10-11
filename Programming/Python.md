dict.fromkeys(seq, value)

- 딕셔너리 생성할 때, seq의 key와 Value로 설정된 값으로 생성함

[사용 예시]
```python
seq = ('First Name', 'Last Name')
d = dict.fromkeys(seq, 'A')
print(d) # {'First Name': 'A', 'Last Name': 'A'}
```

