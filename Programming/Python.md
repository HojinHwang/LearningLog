dict.fromkeys(seq, value)
- 딕셔너리 생성할 때, seq의 key와 Value로 설정된 값으로 생성함

[사용 예시]
```python
seq = ('First Name', 'Last Name')
d = dict.fromkeys(seq, 'A')
print(d) # {'First Name': 'A', 'Last Name': 'A'}
```
---
request.urlretrieve
- URL에서 파일을 다운로드하여 로컬 파일로 저장하는 기능을 제공함
urllib.request.urlretrieve(url, filename=None, reporthook=None, data=None)
[주요 매개변수]
- url: 다운로드할 파일의 URL
- filename (선택 사항): 저장할 파일의 경로 및 이름 지정하지 않으면 임시 파일로 저장
- reporthook (선택 사항): 다운로드 중 진행 상황을 모니터링하기 위한 콜백 함수. 다운로드할 때 호출됨
- data (선택 사항): POST 요청과 함께 보낼 데이터

[사용 예시]
```python
import urllib.request

# 다운로드할 파일 URL과 로컬에 저장할 파일 이름
url = 'https://www.example.com/sample.txt'
filename, headers = urllib.request.urlretrieve(url, 'downloaded_sample.txt')

# 다운로드된 파일 경로와 헤더 정보 출력
print(f"File saved as: {filename}")
print(f"Headers: {headers}")
```
[출력 예시]
```python
File saved as: downloaded_sample.txt
Headers: <http.client.HTTPMessage object at 0x7f9e8473d7b8>
```
