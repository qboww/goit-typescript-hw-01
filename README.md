# Завдання

В рамках домашнього завдання до модуля 1 потрібно встановити та налаштувати середовище розробки. Усі детальні кроки описані в темах 3-5.

Короткий опис твоїх дій:
- Створи репозиторій на GitHub під назвою 'goit-typescript-hw-01'.
- Налаштуй середовище розробки (Модуль 1.3 “Встановлення та налаштування середовища розробки”).
- Налаштуй компілятор (Модуль 1.4 “Налаштування компілятора”).

Опціональне завдання: 
- Встанови source maps в tsconfig.json у проєкті TypeScript для налагодження коду у браузері (Модуль 1.5 “Debugging”).

Якщо ви вже розпочали встановлення та налаштування середовища під час вивчення модуля, то воно має бути готове. У такому випадку повторне виконання цих кроків не потрібне.

Для успішного зарахування завдання необхідно надіслати ментору посилання на твій репозиторій для перевірки.

## Встановлення та налаштування середовища розробки
Для ефективної роботи з TypeScript нам потрібно зробити кілька кроків для встановлення та налаштування середовища розробки. У цьому випадку ми будемо використовувати Node.js і Visual Studio Code (VS Code).

Спочатку потрібно встановити Node.js, якщо у вас його немає. Ви можете завантажити його з офіційного сайту за [адресою](https://nodejs.org/en/) . 
Рекомендується вибрати версію LTS (Long Term Support), оскільки вона є найстабільнішою.

## Наступним кроком буде встановлення TypeScript. 
Це можна зробити за допомогою Node Package Manager (npm), який автоматично встановлюється з Node.js. 

Відкрийте термінал і виконайте наступну команду:
```
npm install -g typescript
```

Ця команда встановлює TypeScript глобально на ваш комп'ютер, що дозволяє використовувати його в будь-якому проєкті.

Visual Studio Code (VS Code) — чудовий вибір для роботи з TypeScript. Якщо ви ще не встановили VS Code, ви можете завантажити його з офіційного сайту: https://code.visualstudio.com/.

Після встановлення VS Code рекомендується встановити наступні розширення, які спростять розробку:
- ESLint
- Prettier - Code formatter
- Path Intellisense
Тепер у вас є все необхідне для початку роботи з TypeScript! Ви можете створити новий файл TypeScript з розширенням .ts і почати писати код.

Ми створили файл test.ts і тепер перекинемо в нього код з попереднього прикладу, але давайте виправимо помилку:

``` typescript
function add(num1: number, num2: number) {
  return num1 + num2;
}

add(1, 1);
```

І ми зробимо його компіляцію в консолі за допомогою команди:
```
tsc test.ts
```

У нас з’явився файл js поруч з файлом ts:

![alt text](./public/image.png)

Давайте подивимося, що всередині файлу js.

![alt text](./public/image-1.png)

Як бачимо, в js зникли всі типи після компіляції, і це стало звичайним JavaScript.

Ми також можемо стежити за зміною файлу в режимі реального часу, виконавши команду:
```
tsc test.ts -w
```

Повна команда виглядає так:
```
tsc test.ts -watch
```

Щоразу, коли ви зберігаєте файл, він буде компілюватися знову, якщо виникне помилка, ви відразу побачите її в консолі.

Посилання на документацію: 

https://www.typescriptlang.org/docs/handbook/compiler-options.html

## Налаштування компілятора
Ми навчилися компілювати один файл, але що робити, якщо є декілька файлів? Нам буде не дуже зручно запускати компілятор для кожного файлу окремо. Замість цього ми можемо створити проєкт TypeScript.

Давайте створимо нову папку (наприклад, ts_courses), перейдемо до неї та виконаємо в консолі команду:
```
tsc --init
```

Ця команда створить файл tsconfig.json, який містить стандартні налаштування TypeScript.

Файл tsconfig.json містить багато налаштувань. 

Розглянемо деякі з найважливіших:
- baseUrl: Якщо ваш проєкт має складну структуру, і ви не хочете прописувати повний шлях, як app/javascript/react/Component під час імпорту, ви можете використовувати baseUrl для спрощення імпорту, наприклад, react/Component. У цьому разі baseUrl буде app/javascript.
- outDir: Каталог, де зберігаються скомпільовані файли.
- rootDir: Коренева папка проєкту, у якій знаходиться основний файл.
- target: Визначає версію ECMAScript, яка використовується для генерації вихідного коду. 

Наприклад, якщо вказати es5, компільований файл не матиме команд const і let та інших нових 
функцій, які були додані до es6, але код буде підтримуватися старими браузерами.
ESNext генерує код, який відповідає останній версії ECMAScript.

У сучасному світі можна починати з версії es2019 і вище.

- module: Визначає систему модулів для використання. commonjs — стандартна система модулів для Node.js. Але ES2020 або ES2022 краще підходить для розробки на клієнтській стороні.
- strict: Включає всі суворі перевірки типів у TypeScript. Це допомагає уникнути багатьох поширених помилок коду.
- lib: Визначає, які бібліотеки слід використовувати. Якщо передати порожній масив у lib, у нашому коді буде недоступний навіть console.log. У lib потрібно вказати мінімально необхідну версію JavaScript, наприклад ["ES2021"].
- allowJs: Дозволяє компілятору TypeScript обробляти файли JavaScript. Це може бути корисно, якщо ви мігруєте проєкт, написаний на JavaScript і переписується на TypeScript. Після завершення міграції це налаштування зазвичай ставлять у false.
- esModuleInterop: Дозволяє імпортувати модулі CommonJS так, ніби вони були б ES6-модулями. Це означає, що якщо у нас є якась бібліотека, яка використовує CommonJS, нам доведеться писати так:

``` javascript
import * as express from 'express';
```

З esModuleInterop ми можемо імпортувати модулі більш природним для ES6 способом:

``` javascript
import express from 'express';
```

- allowSyntheticDefaultImports: Працює у зв’язці з esModuleInterop і дозволяє запобіганню помилок, які виникають під час збірки через несумісності SystemJS і CommonJS. Це налаштування стосується типів.
- experimentalDecorators: Якщо увімкнути цю опцію, TypeScript дозволятиме використання декораторів у вашому коді.
- emitDecoratorMetadata: Це налаштування, що використовується у зв’язці з experimentalDecorators, додає метадані до декораторів.
- isolatedModules: Гарантує, що кожен файл буде розглядатися як окремий модуль, буде неможливо створити файл і щось експортувати з нього. Увімкнено за замовчуванням під час створення проєкту через Create React App. Якщо увімкнено — ви не зможете використовувати const enum у коді.
- preserveConstEnums: Якщо preserveConstEnums встановлено в true, TypeScript зберігає константні перерахування у згенерованому коді JavaScript, коли увімкнено isolatedModules.
- moduleResolution: Визначає стратегію розділення модулів. Доступні два значення: "node" і "classic". Оскільки наші пакети встановлені через npm, найкращим вибором є node.
- skipLibCheck: Вимикає перевірку типів у бібліотеках node_modules. Зазвичай встановлюється в true для пришвидшення компіляції.
- strictNullChecks: TypeScript не дозволить вам використовувати значення null або undefined, де очікується об'єкт. Це допомагає запобігти багатьом поширеним помилкам, оскільки null і undefined є основними джерелами помилок у JavaScript.
- types: Дозволяє задати власні глобальні типи.
- sourceMap: Чи створювати файли source map.
- jsx: Відповідає за обробку синтаксису JSX. Вам знадобиться значення "react" або "react-jsx", додане в TypeScript 4.1 для підтримки нового JSX Transform, введеного в React 17.

І декілька параметрів, які записуються поза блоком compilerOptions:
- include: Визначає, які файли слід включити до процесу компіляції. Наприклад, ви можете включити всі файли TypeScript за допомогою ["**/*.ts", "**/*.tsx"].
- exclude: За замовчуванням, якщо значення не задано, до нього включається "node_modules". Якщо потрібно виключити певні файли чи каталоги, потрібно вручну додати "node_modules". Якщо ви бажаєте виключити певні типи файлів з усіх папок, наприклад тести, ви можете вказати "**/*.spec.ts". Тоді буде ["./node_modules", "**/*.spec.ts"].

Це основні налаштування, які можна змінювати залежно від потреб вашого проєкту.

Може здатися, що налаштувань занадто багато, але з досвідом ви, можливо, скажете, що їх не вистачає :)

Давайте налаштуємо tsconfig.json самостійно.

``` javascript
{
  "compilerOptions": {
    "allowJs": false,
    "allowSyntheticDefaultImports": true,
    "emitDecoratorMetadata": true,
    "esModuleInterop": true,
    "experimentalDecorators": true,
    "lib": ["ES2021"],
    "module": "es2020",
    "moduleResolution": "node",
    "preserveConstEnums": true,
    "skipLibCheck": true,
    "strictNullChecks": true,
    "target": "es2019"
  },
  "include": ["**/*.ts"]
}
```

Давайте створимо файл index.html у корені проєкту, а також додамо каталог src, який буде містити два файли: index.ts і concatenation.ts.

У вас має вийти наступна структура проєкту:

![alt text](./public/image-2.png)

Оскільки у нас є проєкт, ми можемо просто виконати команду:
```
tsc
```

Давайте подивимося, що вийшло:

![alt text](./public/image-3.png)

У каталозі src з'явилися два файли: index.js і concatenation.js. Ми досягли того, що хотіли. Ми скомпілювали весь проєкт однією командою.

Але що в цьому незручно? Справа в тому, що файли js і ts знаходяться поруч один до одного. Якщо файлів буде багато, нам, як мінімум, буде важко знайти потрібні. Давайте встановимо два параметри в налаштуваннях: outDir і rootDir.

Додамо ці параметри в tsconfig.json:

``` javascript
{
  "compilerOptions": {
    "rootDir": "./src", // new
    "outDir": "./dist", // new
    "allowJs": false,
    "allowSyntheticDefaultImports": true,
    "emitDecoratorMetadata": true,
    "esModuleInterop": true,
    "experimentalDecorators": true,
    "lib": ["ES2021"],
    "module": "es2020",
    "moduleResolution": "node",
    "preserveConstEnums": true,
    "skipLibCheck": true,
    "strictNullChecks": true,
    "target": "es2019"
  },
  "include": ["**/*.ts"]
}
```

І знову виконаємо команду:
```
tsc
```

![alt text](./public/image-4.png)

Тепер наш проєкт розділено на дві частини: у dist зберігаються файли js, а в src - файли ts.

Давайте тепер напишемо код, почнемо з index.html:

``` html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Simple TypeScript page</title>
    <script type="module" src="./dist/index.js" defer></script>
  </head>
  <body>
    <input />
    <button>Concat!</button>
  </body>
</html>
```

Зверніть увагу, ми встановили type="module" для script. Це пов'язане з тим, що ми хочемо використовувати команду import у коді, і браузер буде підтримувати його, тільки якщо використовуються модулі.

А тепер давайте опишемо concatenation.ts і index.ts:

``` typescript
function concatenation(firstWord: string, secondWord: string) {
  console.log(`${firstWord} ${secondWord}`);
}

export { concatenation };
```

``` typescript
import { concatenation } from './concatenation';

const button = document.querySelector('button')!;
const input = document.querySelector('input')!;

if (button && input) {
  button.addEventListener('click', () => {
    concatenation(input.value, 'hello!');
  });
}
```

Здається, ми все написали правильно, але все одно бачимо помилки, пов'язані з console і document. Якщо ми наведемо курсор на ці помилки, ми побачимо:

Cannot find name 'document'. Do you need to change your target library? Try changing the 'lib' compiler option to include 'dom'.

Отже, нам потрібно додати 'dom' в налаштування 'lib' файлу tsconfig.json:

``` typescript
{
  "compilerOptions": {
    "rootDir": "./src",
    "outDir": "./dist",
    "allowJs": false,
    "allowSyntheticDefaultImports": true,
    "emitDecoratorMetadata": true,
    "esModuleInterop": true,
    "experimentalDecorators": true,
    "lib": ["dom", "ES2021"], // new
    "module": "es2020",
    "moduleResolution": "node",
    "preserveConstEnums": true,
    "skipLibCheck": true,
    "strictNullChecks": true,
    "target": "es2019"
  },
  "include": ["**/*.ts"]
}
```

Подивимося, чи вирішилася проблема?

``` typescript
import { concatenation } from './concatenation';

const button = document.querySelector('button')!;
const input = document.querySelector('input')!;

if (button && input) {
  button.addEventListener('click', () => {
    concatenation(input.value, 'hello!');
  });
}
```

Але якщо ми зараз відкриємо файл index.js в браузері, то отримаємо помилку CORS.

![alt text](./public/image-5.png)

На жаль, ми не можемо використовувати модулі, а отже, команду import, локально. Нам знадобиться сервер. 

Давайте швидко встановимо сервер @web/dev-server. Але для початку ініціалізуємо проєкт через npm:
```
npm init -y
```

Тепер встановимо сам сервер:
```
npm i --save-dev @web/dev-server
```

Перейдемо до файлу package.json, де нам потрібно додати команду start:

``` typescript
{
  "name": "courses_ts",
  "version": "1.0.0",
  "description": "",
  "scripts": {
    "start": "web-dev-server --node-resolve --open --watch"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "@web/dev-server": "^0.2.1"
  }
}
```

А тепер просто запускаємо:
```
npm start
```

Якщо ви все зробили правильно, ви маєте отримати такий результат: 

![alt text](./public/image-6.png)

Ми створили невеликий застосунок. Давайте ще трохи поговоримо про зручність розробки. Щоб не виконувати команду 'tsc' щоразу, коли ми змінюємо код, ми можемо використовувати наступну команду:

```
tsc -w
```

Вона автоматично слідкуватиме за файлами проєкту і компілювати файли, які були змінені. Для того, щоб не зупиняти виконання npm start щоразу, можна відкрити tsc -w в окремій консолі.