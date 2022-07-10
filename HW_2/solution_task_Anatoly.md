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
