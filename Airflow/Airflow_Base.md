### **kwargs
- **: 인수를 Dictionary 형태로 묶는다는 의미
- kwargs: 명칭일 뿐 (Key arguments), 임의로 지정해도 상관없음
    - kwargs → <name>
```python
# **kwargs 사용 예시
def print_args(**kwargs):
	for key, value in kwargs.items():
		print(f'{key}: {value}')
names = {'name': 'hojin'}		
print_args(names)
```
---
### Xcom
- **XCom (Cross-Communication)**: **Task 간에 데이터를 교환하는 데 사용**되는 Airflow의 내부 메커니즘
- **Push and Pull**: XCom을 통해 데이터를 전송할 때는 “push”, 데이터를 가져올 때는 “pull”이라고 표현
    - `xcom_push` 메서드를 사용하여 데이터를 저장
    - `xcom_pull` 메서드를 사용하여 저장된 데이터를 가져옴
- **Key-Value Pairs**: XCom은 기본적으로 키-값 쌍의 형태로 데이터를 저장. 키는 데이터를 식별하는 데 사용되고, 값은 실제 데이터
- XCom에 저장된 데이터는 Airflow UI에서 확인할 수 있으므로, DAG 실행 중에 데이터를 추적하고 디버깅하는 데 유용함
- XCom은 작은 양의 데이터를 주고받는 데 최적화되어 있습니다. 큰 파일이나 데이터셋을 전달하는 데는 적합하지 않으며, 이 경우 데이터를 외부 스토리지에 저장하고 참조하는 것이 좋음
- Xcom은 JSON() 형태로 데이터를 주고 받으며, Dataframe을 주고 받을 때는 JSON 형태로 변환 후, 전달하는 것이 좋음
```python
# XCOM 사용 예시
from airflow import DAG
from airflow.operators.python import PythonOperator
from datetime import datetime

def push_function(**kwargs):
    value_to_push = "Hello, Airflow!"
    kwargs['ti'].xcom_push(key='greeting', value=value_to_push)

def pull_function(**kwargs):
    greeting = kwargs['ti'].xcom_pull(task_ids='push_task', key='greeting')
    print(f"Pulled Value: {greeting}")

with DAG(dag_id='xcom_example',
         start_date=datetime(2024, 8, 15),
         schedule_interval='@daily',
         catchup=False) as dag:
    
    push_task = PythonOperator(
        task_id='push_task',
        python_callable=push_function,
        provide_context=True
    )
    
    pull_task = PythonOperator(
        task_id='pull_task',
        python_callable=pull_function,
        provide_context=True
    )

push_task >> pull_task
```
