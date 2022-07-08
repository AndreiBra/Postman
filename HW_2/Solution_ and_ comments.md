 
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
### http://162.55.220.72:5005/object_info_4 

```
Cоздаем New Request, данные берем из EP_6 в HW_1
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

### http://162.55.220.72:5005/user_info_2

```
Method: POST
EndPoint: /user_info_2
request form data: 
 name: Andrei
 age: 47
 salary: 1000
```
или  дублируем из HW_1 EP_7 

  
**1. Вставить параметр salary из окружения в request**  
  
перейти во вкладку *Body*, выбрать *from-data* в столбце *Value* напротив *salary* написать {{salary}}  
  
**2. Вставить параметр age из окружения в age**  
  
перейти во вкладку *Body*, выбрать *from-data* в столбце *Value* напротив *age* написать {{age}}  
  
**3. Вставить параметр name из окружения в name**  
  
перейти во вкладку *Body*, выбрать *from-data* в столбце *Value* напротив *name* написать {{name}}   
  
**4. Отправить запрос.**  
  
run `Send`

**5. Статус код 200**   
  
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
**6. Спарсить response body в json**  
  
В окне *Tests* пишем скрипт:
```js
let responseData = pm.response.json();  
console.log('response data:', responseData)
```
run `Send`

В консоле ответ:
```
response data: {person: {…}, qa_salary_after_1.5_year: 18000, qa_salary_after_12_months: 24000…}
```
**7. Спарсить request**  
  
В окне *Tests* пишем скрипт:
```js
let requestData = request.data;  
console.log('request data:', requestData)
```
В консоле ответ:
```
request data: {name: "Andrei", age: "47", salary: "1000"}
```
**8. Проверить, что json response имеет параметр start_qa_salary**  
  
В окне *Tests* пишем скрипт:
```js
pm.test("Test salary start_qa_salary", function () {
    pm.expect(responseData).to.haveOwnProperty('start_qa_salary')
});
```
run `Send`

Во вкладке *Test Results*  
```
PASS Test salary start_qa_salary
```
**9. Проверить, что json response имеет параметр qa_salary_after_6_months**  
  
В окне *Tests* пишем:
```js
pm.test("Test salary qa_salary_after_6_months", function () {
    pm.expect(responseData).to.haveOwnProperty('qa_salary_after_6_months')
});
```
run `Send`

Во вкладке *Test Results*  
```
PASS Test salary qa_salary_after_6_months
```
**10. Проверить, что json response имеет параметр qa_salary_after_12_months**  
  
В окне *Tests* пишем:
```js
pm.test("Test salary qa_salary_after_12_months", function () {
    pm.expect(responseData).to.haveOwnProperty('qa_salary_after_12_months')
});
```
run `Send`

Во вкладке *Test Results*  
```
PASS Test salary qa_salary_after_12_months
```
**11. Проверить, что json response имеет параметр qa_salary_after_1.5_year**  
  
В окне *Tests* пишем скрипт:
```js
pm.test("Test salary have qa_salary_after_1.5_year", function () {
    pm.expect(responseData).to.haveOwnProperty('qa_salary_after_1.5_year')
});
```
run `Send`

Во вкладке *Test Results*  
```
PASS Test salary qa_salary_after_1.5_year
```
**12. Проверить, что json response имеет параметр qa_salary_after_3.5_years**  
  
В окне *Tests* пишем скрипт:
```js
pm.test("Test salary qa_salary_after_3.5_years", function () {
    pm.expect(responseData).to.haveOwnProperty('qa_salary_after_3.5_years')
});
```
run `Send`

Во вкладке *Test Results*  
```
PASS Test salary qa_salary_after_3.5_years
```
**13. Проверить, что json response имеет параметр person**  
  
В окне *Tests* пишем скрипт:
```js
pm.test("Test person", function () {
    pm.expect(responseData).to.haveOwnProperty('person')
});
```
run `Send`

Во вкладке *Test Results*  
```
PASS Test person
```
**14. Проверить, что параметр start_qa_salary равен salary из request (salary забрать из request.)**  
  
В окне *Tests* пишем скрипт:
```js
pm.test("Test start_qa_salary", function () {
    pm.expect(responseData.start_qa_salary).to.eql(Number(requestData.salary));
});
```
run `Send`

Во вкладке *Test Results*  
```
PASS Test start_qa_salary
```
**15. Проверить, что параметр qa_salary_after_6_months равен salary*2 из request (salary забрать из request.)**  
  
В окне *Tests* пишем скрипт:
```js
pm.test("Test qa_salary_after_6_months", function () {
    pm.expect(responseData.qa_salary_after_6_months).to.eql(Number(requestData.salary*2));
});
```
run `Send`

Во вкладке *Test Results*  
```
PASS Test qa_salary_after_6_months
```
**16. Проверить, что параметр qa_salary_after_12_months равен salary*2.7 из request (salary забрать из request.)**  
  
В окне *Tests* пишем скрипт:
```js
pm.test("Test qa_salary_after_12_months", function () {
    pm.expect(responseData.qa_salary_after_12_months).to.eql(Number(requestData.salary*2.7));
});
```
run `Send`

Во вкладке *Test Results*  
```
PASS Test qa_salary_after_12_months
```
**17. Проверить, что параметр qa_salary_after_1.5_year равен salary*3.3 из request (salary забрать из request.)**  
  
В окне *Tests* пишем скрипт:
```js
pm.test("Test qa_salary_after_1.5_year", function () {
    pm.expect(responseData['qa_salary_after_1.5_year']).to.eql(Number(requestData.salary*3.3));
});
```
run `Send`

Во вкладке *Test Results*  
```
PASS Test qa_salary_after_1.5_year
```
**18. Проверить, что параметр qa_salary_after_3.5_years равен salary*3.8 из request (salary забрать из request.)**  
  
В окне *Tests* пишем срипт:
```js
pm.test("Test qa_salary_after_3.5_years", function () {
    pm.expect(responseData['qa_salary_after_3.5_years']).to.eql(Number(requestData.salary*3.8));
});
```
run `Send`

Во вкладке *Test Results*  
```
PASS Test qa_salary_after_3.5_years
```
**19. Проверить, что в параметре person, 1-й элемент из u_name равен salary из request (salary забрать из request.)**  
  
В окне *Tests* пишем скрипт:
```js
pm.test("Test u_name", function () {
    pm.expect(responseData.person.u_name[1]).to.eql(Number(requestData.salary));
});
```
run `Send`

Во вкладке *Test Results*  
```
PASS Test u_name
```
**20. Проверить, что что параметр u_age равен age из request (age забрать из request.)**  
  
В окне *Tests* пишем скрипт:
```js
pm.test("Test u_age", function () {
    pm.expect(responseData.person.u_age).to.eql(Number(requestData.age));
});
```
run `Send`

Во вкладке *Test Results*  
```
PASS Test u_age
```
**21. Проверить, что параметр u_salary_5_years равен salary*4.2 из request (salary забрать из request.)**  
  
В окне *Tests* пишем:
```js
pm.test("Test u_salary_5_years", function () {
    pm.expect(responseData.person.u_salary_5_years).to.eql(Number(requestData.salary*4.2));
});
```
run `Send`

Во вкладке *Test Results*  
```
PASS Test u_salary_5_years
```
__22. ***Написать цикл который выведет в консоль по порядку элементы списка из параметра person__  
  
В окне *Tests* пишем скрипт:
```js
for (let i in responseData.person) {  
console.log(i +': ' + responseData.person[i]);  
	}
```
В консоле ответ:
```
u_age: 47
 
u_name: Andrei,3333,47
 
u_salary_5_years: 13998,6
```
___
```
ДЗ от Толи Supermassive black hole, [Jun 27, 2022 at 11:15:36 PM]: собственно домашка

Supermassive black hole, [17/05/2022 02:08] Ну и небольшая домашка от меня:) ❤️

(ОБЯЗАТЕЛЬНОЕ И ВАЖНЕЙШЕЕ ЗАДАНИЕ) http://162.55.220.72:5005/user_info_2 Необходимо провести тестирование API данного эндпоинта на валидацию входных параметров.
Суть задания: проверить валидации каждого поля, подаваемого в эндпоинт на возможные значения. 
Будем УСЛОВНО считать, что негативная проверка должна возвращать какой угодно статус НО НЕ 200!
Ваша задача написать тест кейсы в постмане таким образом, что одна негативная проверка - один запрос, позитивные проверки можно объединять в 1.
Ваша задача протестировать исходя из требований на все возможные аспекты.
В каждом запросе тест ТОЛЬКО НА СТАТУС КОД (200 - позитивное значение, не 200 - негативное). 
P.S. ЗАДАНИЕ НЕ ПОДРАЗУМЕВАЕТ, ЧТО ЭНДПОИНТ РАБОТАЕТ СОГЛАСНО НАПИСАННЫМ ТРЕБОВАНИЯМ. МЫ УЧИМСЯ ПИСАТЬ ТЕСТЫ НА API!
Требования:
1. Name: 3-40 символов включительно, запрещены префиксные и постфиксные пробелы. Поле обязательное
2. Age: только целые цифры в диапазоне 18-120 включительно. Поле обязательное
3. Salary: только целые цифры в диапазоне 1-1000000 включительно. Поле обязательное

```
### Variant 1 С помощью одного запроса, только мы можм менять в BODY ключи, тем самым делая позитивный или негативный тест. 
```
if(request.data.name.length >= 3 && request.data.name.length <= 40 && request.data.name[0] !== " " && request.data.name.slice(-1) !== " " && request.data.name !== "" && typeof(+request.data.age == 'number') && +request.data.age >= 18 && +request.data.age <= 120 && Number.isInteger(+request.data.age) && +request.data.age !== "" && typeof(+request.data.salary) == 'number' && +request.data.salary >= 1 && +request.data.salary <= 1000000 && Number.isInteger(+request.data.salary) && +request.data.salary !== ""){
    pm.test("Successful POST request", function () {
        pm.response.to.have.status(200);
    });
    } 

// Negative tests: 
else {
    if(!request.data.age.trim()){ 
        pm.test("Field age is required to fill", function () {
            pm.response.to.not.have.status(200);
        });
        }   
    else if(typeof(+request.data.age) !== 'number'){ 
        pm.test("It is not available type for age", function () {
            pm.response.to.not.have.status(200);
        });
        console.log(request.data.age);
        }  
    else if(!Number.isInteger(+request.data.age)){ 
        pm.test("This is fractional value of age", function () {
            pm.response.to.not.have.status(200);
        });
    } 
    else if(+request.data.age < 18){ 
        pm.test("You are younger", function () {
            pm.response.to.not.have.status(200);
        });
        }  
    else if(+request.data.age > 120){ 
        pm.test("You are older", function () {
            pm.response.to.not.have.status(200);
        });
        } 
    if(!request.data.name.trim()){ 
        pm.test("Field name is required to fill", function () {
            pm.response.to.not.have.status(200);
        }); 
     } 
    else if(request.data.name.length < 3){ 
        pm.test("This name is shoter", function () {
            pm.response.to.not.have.status(200);
        });
        }      
    else if(request.data.length > 40){ 
        pm.test("This name is longer", function () {
            pm.response.to.not.have.status(200);
        }); 
     } 
    else if(request.data.name[0] == " "){ 
        pm.test("It is not available to has space in front of name", function () {
            pm.response.to.not.have.status(200);
        });
        }
    else if(request.data.name.slice(-1) == " "){ 
        pm.test("It is not available to has space in end of name", function () {
            pm.response.to.not.have.status(200);
        });
        }  
    if(!+request.data.salary.trim()){ 
        pm.test("Field salary is required to fill", function () {
            pm.response.to.not.have.status(200);
        });
        }      
    else if(typeof(+request.data.salary) !== 'number'){ 
        pm.test("It is not available type for salary", function () {
            pm.response.to.not.have.status(200);
        });
        console.log(request.data.salary);
        }  
    else if(!Number.isInteger(+request.data.salary)){ 
        pm.test("This is fractional value of salary", function () {
            pm.response.to.not.have.status(200);
        });
    } 
    else if(+request.data.salary < 1){ 
        pm.test("You are broke", function () {
            pm.response.to.not.have.status(200);
        });
        }  
    else if(+request.data.salary > 1000000){ 
        pm.test("This salary is not possible for QA", function () {
            pm.response.to.not.have.status(200);
        });
        }       
}
```
