Шаблон методу шаблонів надає план серії кроків для алгоритму. Об'єкти, які реалізують ці кроки, зберігають вихідну структуру алгоритму, але мають можливість перевизначити або налаштувати певні кроки. Ця модель розроблена, щоб запропонувати розширюваність клієнту-розробнику.

Шаблонні методи часто використовуються в фреймворках загального призначення або бібліотеках, які будуть використовуватися іншим розробником Прикладом є об'єкт, який запускає послідовність подій у відповідь на дію, наприклад, запит процесу. Об'єкт генерує подію «попереднього процесу», подію «процесу» та подію «постпроцесу». Розробник має можливість коригувати реакцію безпосередньо перед обробкою, під час обробки і відразу після обробки.
Простий спосіб придумати шаблонний метод - це алгоритм з дірками (див. Схему нижче). Розробник повинен заповнити ці діри відповідним функціоналом для кожного кроку.

![image](https://user-images.githubusercontent.com/46648541/227897767-d45f7fb7-31b2-4522-b8e5-93d151714921.png)

Учасники
#
Об'єктами, що беруть участь в цій закономірності, є:

AbstractClass -- У прикладі коду: сховище даних
пропонує інтерфейс для клієнтів для виклику шаблонуМетод
реалізує шаблонний метод, який визначає примітивні кроки для алгоритму
надає гачки (за допомогою методу перевизначення) для розробника-клієнта для реалізації Кроків

Конкретний клас -- У прикладі коду: mySql
реалізує примітивні кроки, визначені в AbstractClass

Це приклад, коли ми використовуємо прототипне успадкування JavaScript. Функція успадкування допомагає нам встановити зв'язок успадкування, присвоївши прототипу новоствореного об'єкта-нащадка базовий об'єкт.

Функція сховища даних представляє AbstractClass, а mySql - Конкретний клас. mySql замінює 3 методи шаблонів: підключення, вибір та відключення від конкретних реалізацій сховища даних.

Шаблонні методи дозволяють клієнту змінювати сховище даних (SQL Server, Oracle і т.д.) шляхом коригування (заповнення пропусків) тільки шаблонних методів. Решта, наприклад, порядок кроків, залишається незмінною для будь-якого сховища даних.

var datastore = {
    process: function () {
        this.connect();
        this.select();
        this.disconnect();
        return true;
    }
};

function inherit(proto) {
    var F = function () { };
    F.prototype = proto;
    return new F();
}

function run() {
    var mySql = inherit(datastore);

    // implement template steps

    mySql.connect = function () {
        console.log("MySQL: connect step");
    };

    mySql.select = function () {
        console.log("MySQL: select step");
    };

    mySql.disconnect = function () {
        console.log("MySQL: disconnect step");
    };

    mySql.process();
}

