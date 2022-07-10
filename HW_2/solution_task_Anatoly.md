ДЗ от Толи Supermassive black hole, [Jun 27, 2022 at 11:15:36 PM]: собственно домашка

Supermassive black hole, [17/05/2022 02:08] Ну и небольшая домашка от меня:) ❤️
___

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


### Variant 1 С помощью одного запроса, только мы можм менять в BODY ключи, тем самым делая позитивный или негативный тест. 

```js
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
### Variant 2 Написать каждый запрос в отдельности посмотреть 25 запросов можно в JSON файле [здесь](https://github.com/AndreiBra/Postman/blob/main/HW_2/HW_2%20_Anatoliy_1_var_2.postman_collection.json)

___

### Задание 1****. Преобразовать задание 1 таким образом, чтобы вы отправляли параметры через CSV файл. У вас будет ровно 1 запрос в коллекции, который будет повторяться столько раз, сколько строк в CSV файле. Также должна быть написана функция в тестах, которая проверяет валидность входящих данных, и в зависимости от этого проверяет на статус 200 или НЕ 200.

Запуск осущесствляем через `run collection`, если реквестов много снимаем галки со всех кроме нужного запроса, `select file` выбираем наш csv файл и запускаем коллекцию `run ...`

```js
const reqData = request.data;
let name = reqData.name;
let age = reqData.age;
let salary = reqData.salary;

function nameTest(value) {
    return value != ''
        && value.length >= 3 && value.length <= 40
        && value.trim() == value;
}

function salaryTest(value) {
    return value != ''
        && Number.isInteger(+value)
        && value >= 1 && value <= 1000000;
}

function ageTest(value) {
    return value != ''
        && Number.isInteger(+value)
        && value >= 18 && value <= 120;
}

function validTest() {
    return nameTest(name) && ageTest(age) && salaryTest(salary);
}

if (validTest()) {
    pm.test(`Status code is 200: name = "${name}", age = "${age}" and salary = "${salary}"`, 
    function () {
        pm.response.to.have.status(200);
    });
} else {

    pm.test(`Status code isn't 200: name = "${name}", age = "${age}" and salary = "${salary}"`, 
    function () {
        pm.response.to.have.not.status(200);
    });
}
```
Variant 2 от Anatoliya

```js
const age = pm.iterationData.get('age');
const name = pm.iterationData.get('name');
const salary = pm.iterationData.get('salary');

function ageValidation(value) {
    return value && !isNaN(value) && value>17 && value<121 && Number.isInteger(+value)
}
    
function salaryValidation(value) {
    return value && !isNaN(value) && value>0 && value<1000001 && Number.isInteger(+value)
}    

function nameValidation(value) {
    return value && value>17 && value.lenght >2 && value.lenght<41 && value.trim() ===value
}

function validate(name, age, salary) {
    return ageValidation(age) && salaryValidation(salary) && nameValidation(name)
}

if (validate(name, age, salary)) {
    pm.test(`200 code with name == ${name}, age == ${age} and salary == ${salary} `, () => {
        pm.response.to.have.status(200);
    })
} else {
     pm.test(`NOT 200 code with name == ${name}, age == ${age} and salary == ${salary}`, () => {
        pm.response.to.not.have.status(200);
    })
}    
```

___

### 2 задание http://162.55.220.72:5007/object_info_4
Преобразовать пункты 12-13-14 (salary из реквеста и респонса равны) таким образом, чтобы проверка производилась циклом, в котором будет всего ОДИН тест. Имя теста должно меняться в зависимости от значения в Salary
12. Проверить, что 0-й элемент параметра salary равен salary из request (salary забрать из request.)
13. Проверить, что 1-й элемент параметра salary равен salary*2 из request (salary забрать из request.)
14. Проверить, что 2-й элемент параметра salary равен salary*3 из request (salary забрать из request.)

```js
const respSalary = pm.response.json().salary

const reqSalary = +pm.request.url.query.get('salary')

respSalary.forEach((salary, index) => {
    pm.test(`${reqSalary} * ${index+1} === ${salary}`, () => {
        pm.expect(reqSalary*(index+1)).to.eql(+salary)
    })
})
```
___

### 3 задание http://162.55.220.72:5005/object_info_3 Преобразовать задания 5-7 (сравнить идентичные поля в реквесте и респонсе) таким образом, чтобы это делалось ЗА ОДИН ТЕСТ (сразу все 3 поля) БЕЗ ЦИКЛОВ! (глубокое сравнение объектов)
5. Проверить, что name в ответе равно name s request (name забрать из request.)
6. Проверить, что age в ответе равно age s request (age забрать из request.)
7. Проверить, что salary в ответе равно salary s request (salary забрать из request.)

### Variant 1
```js
const reqObject = pm.request.url.query.toObject()
const respObject = {
    age: String(pm.response.json().age),
    name: pm.response.json().name,
    salary: String(pm.response.json().salary)
}

pm.test('Compare request object and response object', () => {
    pm.expect(reqObject).to.deep.eql(respObject)
})
```
### Variant 2

```js
const jsonData = pm.response.json()

const resp = {};
for(const key in reqObject) {
    resp[key] = isNaN(jsonData[key]) ? jsonData[key] : +jsonData[key]
    reqObject[key] = isNaN(reqObject[key]) ? reqObject[key] : +reqObject[key]
}

pm.test('2.0 Compare request object and response object', () => {
    pm.expect(reqObject).to.deep.eql(resp)
})
```
___

### 4 задание
//4.  http://162.55.220.72:5005/user_info_2

//4.1.  Преобразовать задания 8 - 13 (проверить что в json имеется нужный параметр) таким образом, чтобы все проверки делались в цикле (1 проверка в цикле, в которую попадают нужные параметры). Название теста должно видоизменяться исходя из подаваемых данных. ( ${} или другим способом)
// 8. Проверить, что json response имеет параметр start_qa_salary
// 9. Проверить, что json response имеет параметр qa_salary_after_6_months
// 10. Проверить, что json response имеет параметр qa_salary_after_12_months
// 11. Проверить, что json response имеет параметр qa_salary_after_1.5_year
// 12. Проверить, что json response имеет параметр qa_salary_after_3.5_years
// 13. Проверить, что json response имеет параметр person
```js
const keyisInJson = ['start_qa_salary', 'qa_salary_after_6_months', 'qa_salary_after_12_months', 'qa_salary_after_1.5_year', 'qa_salary_after_3.5_years', 'person']
let resp = pm.response.json()

keyisInJson.forEach(key => {
    pm.test(`Response has ${key}`, () => {
        pm.expect(resp).to.have.property(key)
    })
})
```
//4.2.  ** Преобразовать задания 14 - 18 (проверить что параметр равен salary умножить на коэффициент) таким образом, чтобы все проверки делались в цикле (1 проверка в цикле, в которую попадают нужные параметры). Название теста должно видоизменяться исходя из подаваемых данных. ( ${} или другим способом)
// 14. Проверить, что параметр start_qa_salary равен salary из request (salary забрать из request.)
// 15. Проверить, что параметр qa_salary_after_6_months равен salary*2 из request (salary забрать из request.)
// 16. Проверить, что параметр qa_salary_after_12_months равен salary*2.7 из request (salary забрать из request.)
// 17. Проверить, что параметр qa_salary_after_1.5_year равен salary*3.3 из request (salary забрать из request.)
// 18. Проверить, что параметр qa_salary_after_3.5_years равен salary*3.8 из request (salary забрать из request.)
```js
const salary = pm.environment.get('salary')
const counters = {
  "start_qa_salary": 1,
  "qa_salary_after_6_months": 2,
  "qa_salary_after_3.5_years": 3.8,
  "qa_salary_after_12_months": 2.7,
  "qa_salary_after_1.5_year": 3.3
}

for(const key in counters) {
    pm.test(`${key} from response = salary from request * ${counters[key]}`, () => {
        pm.expect(+resp[key]).to.eql(salary*counters[key])
    })
}
```
//4.3.  *** Преобразовать описанные выше задания 1 и 2 для данного эндпоинта в ОДИН ЦИКЛ, в котором будут проходить ОБА теста.
```js
counters['person'] = ''

for(const key in counters) {
       pm.test(`response has ${key}`, () => {
         pm.expect(resp).to.have.property(key)
             })
    if(key != 'person'){
        pm.test(`${key} from response = salary from request * ${counters[key]}`, () => {
        pm.expect(+resp[key]).to.eql(salary*counters[key])
        })
    }         
}
```
