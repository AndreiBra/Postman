 
###  http://162.55.220.72:5005/first
  
``` 
Creating  'new collection' "HW_2"
  
"Add a request" name - "hw_2"
  
GET  http://162.55.220.72:5005/first  
```
  
**1. Отправить запрос**  
  
run `Send`  

response `This is the first responce from server!`
  
**2. Статус код 200**   
  
В поле `Tests`  из списка `SNIPPETS` выбираем *"Status code; Code is 200"* -> run `Send`

в поле ввода кода появляется: 
  
```js
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```
Во вкладке *Test Results*  
```
PASS Status code is 200
```
3. Проверить, что в body приходит правильный string  
  
ответ в *body*  

```js
'This is the first responce from server!'
```
Во вкладке *Test Results*  
```
PASS Status code is 200
```   

___

### http://162.55.220.72:5005/user_info_3

"Add a request" name - "hw_2"
  
```
Данные взять или сделать дубликат из коллекции HW_1 'Post EP_2"
POST, http://162.55.220.72:5005/user_info_3 
Method: POST
EndPoint: /user_info_3
request form data: 
 name: Andrei
 age: 47
 salary: 1000
 ```

**1. Отправить запрос**  
  
run `Send`  

**2. Статус код 200**   
  
В поле тест выбираем из списка SNIPPETS *Status code is 200*, в поле ввода кода появляется: 

```js
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```
run `Send`

Во вкладке *Test Results*  
```
PASS Status code is 200
```
**3. Спарсить response body в json**  
  
В окне *Tests* пишем:
```js
let responseData = pm.response.json();  
console.log('response data:', responseData)
```
run `Send` 

В консольной строке появится ответ:  
```
response data: {age: "47", family: {…}, name: "Andrei"…}
```
**4. Проверить, что name в ответе равно name s request (name вбить руками.)**  
  
В окне *Tests* пишем:  
```js
pm.test("Test name", function () {
    pm.expect(responseData.name).to.eql("Andrei");
});
```
run `Send` 

Во вкладке *Test Results*  
```
PASS Test name
```
**5. Проверить, что age в ответе равно age s request (age вбить руками.)**  
   
В окне *Tests* пишем:  
```js
pm.test("Test age", function () {
    pm.expect(responseData.age).to.eql("47");
});
```
run `Send`

Во вкладке *Test Results*  
```
PASS  Test Age
```
**6. Проверить, что salary в ответе равно salary s request (salary вбить руками.)**  
  
В окне *Tests* пишем:  
```js
pm.test("Test salary", function () {
    pm.expect(responseData.salary).to.eql(1000);
});
```
run `Send`

Во вкладке *Test Results*  
```
PASS Test salary
```
**7. Спарсить request**  
  
В окне *Tests* пишем:  
```js
let requestData = request.data;  
console.log('request data:', requestData)
```
run `Send`

В консольной строке смотрим ответ:  
```
 request data: {name: "Andrei", age: "47", salary: "1000"}
 ```
**8. Проверить, что name в ответе равно name s request (name забрать из request.)**  
  
В окне *Tests* пишем:  
```js
pm.test("Your test name", function () {
    pm.expect(responseData.name).to.eql(requestData.name);
});
```
run`Send`

Во вкладке *Test Results*  
```
PASS  Your test name
```
**9. Проверить, что age в ответе равно age s request (age забрать из request.)**  
  
В окне *Tests* пишем:  
```js
pm.test("Your test age", function () {
    pm.expect(responseData.age).to.eql(requestData.age);
});
```
run `Send`

Во вкладке *Test Results*  
```
PASS Your test age
```
**10. Проверить, что salary в ответе равно salary s request (salary забрать из request.)**  
  
В окне *Tests* пишем:  
```js
pm.test("Your test salary", function () {
    pm.expect(responseData.salary).to.eql(Number(requestData.salary));
});
```
run `Send`

Во вкладке *Test Results*  
```
PASS Your test salary
```
**11. Вывести в консоль параметр family из response**  
  
В окне *Tests* пишем:    
```js
console.log('Family: ', responseData.family)
```
run `Send`

В консольной строке смотрим ответ:  
```
Family: {children: [2], u_salary_1_5_year: 4000}
```
**12.  Проверить что u_salary_1_5_year в ответе равно salary*4 (salary забрать из request)**  
  
В окне *Tests* пишем:  
```js
pm.test("Test u_salary_1_5_year", function () {
    pm.expect(responseData.family.u_salary_1_5_year).to.eql(requestData.salary*4);
});
```
run `Send`

Во вкладке *Test Results* 
```
PASS Your test u_salary_1_5_year
```
___

  ***  
### http://162.55.220.72:5005/object_info_3	

``` 
"Add a request" name - "hw_2" 
GET, http://162.55.220.72:5005/object_info_3

или продублировать EP_5 из HW_1

Method: GET
EndPoint: /object_info_3
request url params: 
 name: Andrei
 age: 47
 salary: 1000
```  
  
**1. Отправить запрос**  
  
run `Send`  
  
**2. Статус код 200**   
  
В поле 'Tests' выбираем из списка SNIPPETS *Status code is 200*, в поле ввода кода появляется:    
```js
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```
run `Send`

Во вкладке *Test Results*  
```
PASS Status code is 200
```
**3. Спарсить response body в json**  
  
В окне *Tests* пишем:
```js
let responseData = pm.response.json();  
console.log('response data:', responseData)
```
run `Send`

В консольной строке смотрим ответ:
```
response data: {age: "47", family: {…}, name: "Andrei"…}
```
**4. Спарсить request**  
  
В окне *Tests* пишем::
```js
let requestData = pm.request.url.query.toObject();
console.log('request data:', requestData)
```
run `Send`

В Console смотрим ответ:
```
request data: {name: "Andrei", age: "47", salary: "1000"}
```
**5. Проверить, что name в ответе равно name s request (name забрать из request.)**  
  
В окне *Tests* пишем:  
```js
pm.test("Your test name", function () {
    pm.expect(responseData.name).to.eql(requestData.name);
});
```
run `Send`

Во вкладке *Test Results*  
```
PASS  Your test name
```
**6. Проверить, что age в ответе равно age s request (age забрать из request.)**  
  
В окне *Tests* пишем:  
```js
pm.test("Your test age", function () {
    pm.expect(responseData.age).to.eql(requestData.age);
});
```
run `Send`

Во вкладке *Test Results*  
```
PASS Your test age
```
**7. Проверить, что salary в ответе равно salary s request (salary забрать из request.)**  
  
В окне *Tests* пишем:  
```js
pm.test("Test salary", function () {
    pm.expect(responseData.salary).to.eql(Number(requestData.salary));
});
```
run `Send`

Во вкладке *Test Results*  
```
PASS Test salary
```
**8. Вывести в консоль параметр family из response**  
    
В окне *Tests* пишем:  
```js
console.log('Family: ', responseData.family)
```
run `Send`

В консольной строке смотрим ответ:  
```
Family: {children: [2], pets: {…}, u_salary_1_5_year: 4000}
```
**9. Проверить, что у параметра dog есть параметры name**  
  
В окне *Tests* пишем:  
```js
pm.test("Test dog has name", function () {
    pm.expect(responseData.family.pets.dog).to.haveOwnProperty('name')
});
```
run `Send`

Во вкладке *Test Results*  
```
PASS Your test dog has name
```
**10. Проверить, что у параметра dog есть параметры age**  
  
В окне *Tests* пишем:  
```js
pm.test("Test dog has age", function () {
    pm.expect(responseData.family.pets.dog).to.haveOwnProperty('age')
});
```
run `Send`

Во вкладке *Test Results*  
```
PASS Test dog has age
```
**11. Проверить, что параметр name имеет значение Luky**  
  
В окне *Tests* пишем:  
```js
pm.test("Test dog's name is Luky", function () {
    pm.expect(responseData.family.pets.dog.name).to.eql('Luky')
});
```
Во вкладке *Test Results*  
```
PASS Test dog's name is Luky
```
**12. Проверить, что параметр age имеет значение 4**  
  
В окне *Tests* пишем:  
```js
pm.test("Test dog have age 4", function () {
    pm.expect(responseData.family.pets.dog.age).to.eql(4)
});
```
Во вкладке *Test Results*  
```
PASS Test dog have age 4
```
___
```
Cоздаем New Request, данные берем из EP_1_6  из HW_1
или 
Метод GET, http://162.55.220.72:5005/object_info_4 
Method: GET
EndPoint: /object_info_4
request url params: 
 name: Andrei
 age: 47
 salary: 3333  
 ```
 
**1. Отправить запрос**  
   
run `Send`  
  
**2. Статус код 200**   
  
В поле тест выбираем из списка SNIPPETS *Status code is 200*, в поле ввода кода появляется:    
```js
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```
run `Send`

Во вкладке *Test Results*  
```
PASS Status code is 200
```
  
**3. Спарсить response body в json**  
  
В окне *Tests* пишем:
```js
let responseData = pm.response.json();  
console.log('response data:', responseData)
```
run `Send`

В консольной строке смотрим ответ:
```
response data: {age: 47, name: "Andrei", salary: [3333]}
```
  
**4. Спарсить request**  
  
В окне *Tests* пишем:  
```
let requestData = pm.request.url.query.toObject();
console.log('request data:', requestData)
```
run `Send`

В консольной строке смотрим ответ:
```
request data: {name: "Andrei", age: "47", salary: "3333"}
```
  
**5. Проверить, что name в ответе равно name s request (name забрать из request.)**  
  
В окне *Tests* пишем:  
```js
pm.test("Test name", function () {
    pm.expect(responseData.name).to.eql(requestData.name);
});
```
run `Send`

Во вкладке *Test Results*  
```
PASS Test name
```
**6. Проверить, что age в ответе равно age из request (age забрать из request.)**
  
В окне *Tests* пишем:  
```js
pm.test("Test age", function () {
    pm.expect(responseData.age).to.eql(Number(requestData.age));
});
```
run `Send`

Во вкладке *Test Results*  
```
PASS Test age
```  
**7. Вывести в консоль параметр salary из request**  
  
В окне *Tests* пишем:  
```js
console.log(requestData.salary);
```
run `Send`

В консольной строке смотрим ответ:
```
3333
```

**8. Вывести в консоль параметр salary из response**  
  
В окне *Tests* пишем:  
```js
console.log(responseData.salary);
```
run `Send`

В консольной строке смотрим ответ:
```
(3) [3333, "6666", "9999"]
```
**9. Вывести в консоль 0-й элемент параметра salary из response**  
  
В окне *Tests* пишем:  
```js
console.log(responseData.salary[0]);
```
run `Send`

В консольной строке смотрим ответ:
```
3333
```
**10. Вывести в консоль 1-й элемент параметра salary параметр salary из response**  
  
В окне *Tests* пишем:  
```js
console.log(responseData.salary[1]);
```
run `Send`

В консольной строке смотрим ответ:
```
6666
```
**11. Вывести в консоль 2-й элемент параметра salary параметр salary из response**  
  
В окне *Tests* пишем:  
```js
console.log(responseData.salary[2]);
```
run `Send`

В консольной строке смотрим ответ:
```
9999
```
**12. Проверить, что 0-й элемент параметра salary равен salary из request (salary забрать из request.)**  
  
В окне *Tests* пишем:  
```js
pm.test("Test salary zero element", function () {
    pm.expect(responseData.salary[0]).to.eql(Number(requestData.salary));
});
```
run `Send`

Во вкладке *Test Results*  
```
PASS Test salary zero element
```
**13. Проверить, что 1-й элемент параметра salary равен salary*2 из request (salary забрать из request.)**  
  
В окне *Tests* пишем:  
```js
pm.test("Test salary first element", function () {
    pm.expect(Number(responseData.salary[1])).to.eql(Number(requestData.salary*2));
});
```
Во вкладке *Test Results*  
```
PASS Test salary firsrt element
```
**14. Проверить, что 2-й элемент параметра salary равен salary*3 из request (salary забрать из request.)**  
  
В окне *Tests* пишем:  
```js
pm.test("Test salary second element", function () {
    pm.expect(Number(responseData.salary[2])).to.eql(Number(requestData.salary*3));
});
```
Во вкладке *Test Results*  
```
PASS Test salary second element
```
**15. Создать в окружении переменную name**  
  
в меню слева выбирать *Environment*, далее жмем *New*
Переименовываем в HW_2 В строку *Variable* вносим название переменной name, в *Current value* пишем Andrei  
  
**16. Создать в окружении переменную age**  
  
в меню слева выбирать *Environment*, далее выбираем HW_2.  
В строку *Variable* вносим название переменной age, в *Current value* пишем 47  
  
**17. Создать в окружении переменную salary**  
  
в меню слева выбирать *Environment*, далее выбираем HW_2.  
В строку *Variable* вносим название переменной salary, в *Current value* пишем 3333 
  
**18. Передать в окружение переменную name**  
  
В окне *Tests* пишем:  
```js
pm.environment.set('name', responseData.name)
```
**19. Передать в окружение переменную age**  
  
В окне *Tests* пишем:  
```js
pm.environment.set('age', responseData.age)
```
**20. Передать в окружение переменную salary**  
  
В окне *Tests* пишем:  
```js
pm.environment.set('salary', responseData.salary[0])
```
**21. Написать цикл который выведет в консоль по порядку элементы списка из параметра salary**  
  
В окне *Tests* пишем:  
```js
for (let i = 0; i < 3; i=i+1) {
    console.log('My salary:', responseData.salary[0+i])
}
```
В консольной строке смотрим ответ:
```
My salary: 3333
 
My salary: 6666
 
My salary: 9999
```
___


  
## **EP_2_5**<a name="2.5"><a>  
Создаем New Request, выбираем метод POST,  
пишем в *Enter request URL* http://162.55.220.72:5005/user_info_2 (EP_1_7 из HW_Postman_1)  
  
**1. Вставить параметр salary из окружения в request**  
  
перейти во вкладку *Body*, выбрать *from-data* в столбце *Value* напротив *salary* написать {{salary}}  
  
**2. Вставить параметр age из окружения в age**  
  
перейти во вкладку *Body*, выбрать *from-data* в столбце *Value* напротив *age* написать {{age}}  
  
**3. Вставить параметр name из окружения в name**  
  
перейти во вкладку *Body*, выбрать *from-data* в столбце *Value* напротив *name* написать {{name}}   
  
**4. Отправить запрос.**  
  
Жмем *Send*  

**5. Статус код 200**   
  
В поле тест выбираем из списка SNIPPETS *Status code is 200*, в поле ввода кода появляется:  
```js
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```
Во вкладке *Test Results*  
```
PASS Status code is 200
```
**6. Спарсить response body в json**  
  
В окне *Tests* пишем:
```js
let responseData = pm.response.json();  
console.log('response data:', responseData)
```
В консольной строке смотрим ответ:
```
response data: {person: {…}, qa_salary_after_1.5_year: 198000, qa_salary_after_12_months: 162000…}
```
**7. Спарсить request**  
  
В окне *Tests* пишем:
```js
let requestData = request.data;  
console.log('request data:', requestData)
```
В консольной строке смотрим ответ:
```
request data: {name: "Sergey", age: "36", salary: "60000"}
```
**8. Проверить, что json response имеет параметр start_qa_salary**  
  
В окне *Tests* пишем:
```js
pm.test("EP_2_5. Your test salary have start_qa_salary", function () {
    pm.expect(responseData).to.haveOwnProperty('start_qa_salary')
});
```
Во вкладке *Test Results*  
```
PASS EP_2_5. Your test salary have start_qa_salary
```
**9. Проверить, что json response имеет параметр qa_salary_after_6_months**  
  
В окне *Tests* пишем:
```js
pm.test("EP_2_5. Your test salary have qa_salary_after_6_months", function () {
    pm.expect(responseData).to.haveOwnProperty('qa_salary_after_6_months')
});
```
Во вкладке *Test Results*  
```
PASS EP_2_5. Your test salary have qa_salary_after_6_months
```
**10. Проверить, что json response имеет параметр qa_salary_after_12_months**  
  
В окне *Tests* пишем:
```js
pm.test("EP_2_5. Your test salary have qa_salary_after_12_months", function () {
    pm.expect(responseData).to.haveOwnProperty('qa_salary_after_12_months')
});
```
Во вкладке *Test Results*  
```
PASS EP_2_5. Your test salary have qa_salary_after_12_months
```
**11. Проверить, что json response имеет параметр qa_salary_after_1.5_year**  
  
В окне *Tests* пишем:
```js
pm.test("EP_2_5. Your test salary have qa_salary_after_1.5_year", function () {
    pm.expect(responseData).to.haveOwnProperty('qa_salary_after_1.5_year')
});
```
Во вкладке *Test Results*  
```
PASS EP_2_5. Your test salary have qa_salary_after_1.5_year
```
**12. Проверить, что json response имеет параметр qa_salary_after_3.5_years**  
  
В окне *Tests* пишем:
```js
pm.test("EP_2_5. Your test salary have qa_salary_after_3.5_years", function () {
    pm.expect(responseData).to.haveOwnProperty('qa_salary_after_3.5_years')
});
```
Во вкладке *Test Results*  
```
PASS EP_2_5. Your test salary have qa_salary_after_3.5_years
```
**13. Проверить, что json response имеет параметр person**  
  
В окне *Tests* пишем:
```js
pm.test("EP_2_5. Your test have person", function () {
    pm.expect(responseData).to.haveOwnProperty('person')
});
```
Во вкладке *Test Results*  
```
PASS EP_2_5. Your test have person
```
**14. Проверить, что параметр start_qa_salary равен salary из request (salary забрать из request.)**  
  
В окне *Tests* пишем:
```js
pm.test("EP_2_5. Your test start_qa_salary", function () {
    pm.expect(responseData.start_qa_salary).to.eql(Number(requestData.salary));
});
```
Во вкладке *Test Results*  
```
PASS EP_2_5. Your test start_qa_salary
```
**15. Проверить, что параметр qa_salary_after_6_months равен salary*2 из request (salary забрать из request.)**  
  
В окне *Tests* пишем:
```js
pm.test("EP_2_5. Your test qa_salary_after_6_months", function () {
    pm.expect(responseData.qa_salary_after_6_months).to.eql(Number(requestData.salary*2));
});
```
Во вкладке *Test Results*  
```
PASS EP_2_5. Your test qa_salary_after_6_months
```
**16. Проверить, что параметр qa_salary_after_12_months равен salary*2.7 из request (salary забрать из request.)**  
  
В окне *Tests* пишем:
```js
pm.test("EP_2_5. Your test qa_salary_after_12_months", function () {
    pm.expect(responseData.qa_salary_after_12_months).to.eql(Number(requestData.salary*2.7));
});
```
Во вкладке *Test Results*  
```
PASS EP_2_5. Your test qa_salary_after_12_months
```
**17. Проверить, что параметр qa_salary_after_1.5_year равен salary*3.3 из request (salary забрать из request.)**  
  
В окне *Tests* пишем:
```js
pm.test("EP_2_5. Your test qa_salary_after_1.5_year", function () {
    pm.expect(responseData['qa_salary_after_1.5_year']).to.eql(Number(requestData.salary*3.3));
});
```
Во вкладке *Test Results*  
```
PASS EP_2_5. Your test qa_salary_after_1.5_year
```
**18. Проверить, что параметр qa_salary_after_3.5_years равен salary*3.8 из request (salary забрать из request.)**  
  
В окне *Tests* пишем:
```js
pm.test("EP_2_5. Your test qa_salary_after_3.5_years", function () {
    pm.expect(responseData['qa_salary_after_3.5_years']).to.eql(Number(requestData.salary*3.8));
});
```
Во вкладке *Test Results*  
```
PASS EP_2_5. Your test qa_salary_after_3.5_years
```
**19. Проверить, что в параметре person, 1-й элемент из u_name равен salary из request (salary забрать из request.)**  
  
В окне *Tests* пишем:
```js
pm.test("EP_2_5. Your test u_name", function () {
    pm.expect(responseData.person.u_name[1]).to.eql(Number(requestData.salary));
});
```
Во вкладке *Test Results*  
```
PASS EP_2_5. Your test u_name
```
**20. Проверить, что что параметр u_age равен age из request (age забрать из request.)**  
  
В окне *Tests* пишем:
```js
pm.test("EP_2_5. Your test u_age", function () {
    pm.expect(responseData.person.u_age).to.eql(Number(requestData.age));
});
```
Во вкладке *Test Results*  
```
PASS EP_2_5. Your test u_age
```
**21. Проверить, что параметр u_salary_5_years равен salary*4.2 из request (salary забрать из request.)**  
  
В окне *Tests* пишем:
```js
pm.test("EP_2_5. Your test u_salary_5_years", function () {
    pm.expect(responseData.person.u_salary_5_years).to.eql(Number(requestData.salary*4.2));
});
```
Во вкладке *Test Results*  
```
PASS EP_2_5. Your test u_salary_5_years
```
__22. ***Написать цикл который выведет в консоль по порядку элементы списка из параметра person__  
  
В окне *Tests* пишем:
```js
for (let i in responseData.person) {  
console.log(i +': ' + responseData.person[i]);  
	}
```
В консольной строке смотрим ответ:
```
u_age: 36
 
u_name: Sergey,60000,36
 
u_salary_5_years: 252000
```
