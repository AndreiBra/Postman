# Создать запросы в Postman.
___


Protocol: http
IP: 162.55.220.72
Port: 5005
___

- EP_1
```
Method: GET
EndPoint: /get_method
request url params: 
 name: Andrei
 age: 47

response: 
[
    “Str”,
    “Str”
]
```



- EP_2
```
Method: POST
EndPoint: /user_info_3
request form data: 
 name: Andrei
 age: 47
 salary: 1499

response: 
{'name': name,
          'age': age,
          'salary': salary,
          'family': {'children': [['Alex', 24], ['Kate', 12]],
                     'u_salary_1_5_year': salary * 4}}

```


- EP_3
```
Method: GET
EndPoint: /object_info_1
request url params: 
 name: Andrei
 age: 47
 weight: 74

response: 
{'name': name,
          'age': age,
          'daily_food': weight * 0.012,
          'daily_sleep': weight * 2.5}

```


- EP_4
```
Method: GET
EndPoint: /object_info_2
request url params: 
 name: Andrei
 age: 47
 salary: 1000

response: 
{'start_qa_salary': salary,
          'qa_salary_after_6_months': salary * 2,
          'qa_salary_after_12_months': salary * 2.7,
          'qa_salary_after_1.5_year': salary * 3.3,
          'qa_salary_after_3.5_years': salary * 3.8,
          'person': {'u_name': [user_name, salary, age],
                     'u_age': age,
                     'u_salary_5_years': salary * 4.2}
          }

```

- EP_5
```
Method: GET
EndPoint: /object_info_3
request url params: 
 name: Andrei
 age: 47
 salary: 999

response: 
{'name': name,
          'age': age,
          'salary': salary,
          'family': {'children': [['Alex', 24], ['Kate', 12]],
                     'pets': {'cat':{'name':'Sunny',
                                     'age': 3},
                              'dog':{'name':'Luky',
                                     'age': 4}},
                     'u_salary_1_5_year': salary * 4}
          }
```


- EP_6
```
Method: GET
EndPoint: /object_info_4
request url params: 
 name: Andrei
 age: 47
 salary: 3333

response: 
{'name': name,
          'age': int(age),
          'salary': [salary, str(salary * 2), str(salary * 3)]}

```

- EP_7

```
Method: POST
EndPoint: /user_info_2
request form data: 
 name: Andrei
 age: 47
 salary: 1000

response: 
{'start_qa_salary': salary,
          'qa_salary_after_6_months': salary * 2,
          'qa_salary_after_12_months': salary * 2.7,
          'qa_salary_after_1.5_year': salary * 3.3,
          'qa_salary_after_3.5_years': salary * 3.8,
          'person': {'u_name': [user_name, salary, age],
                     'u_age': age,
                     'u_salary_5_years': salary * 4.2}
          }
```
___
# Решение задачи можно посмотреть в файле HW_1.postman_collection.json, либо перейти по [ссылке](https://github.com/AndreiBra/Postman/blob/main/HW_1/HW_1.postman_collection.json)

## Так же решение можно посмотреть в [видео формате](https://youtu.be/sCMbDXs50aM)
