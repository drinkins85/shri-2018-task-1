## Задание 1

#### Приложение не запускается
Ошибка: throw new Error('Dialect needs to be explicitly supplied as of v4.0.0');
```
Неверная сигнатура вызова new Sequelize(null, null, {params}) в файле models/index.js, требуется четыре параметра.
Исправлено на new Sequelize(null, null, null, {params})
```
Документация: [http://docs.sequelizejs.com](http://docs.sequelizejs.com/manual/installation/getting-started.html)

После исправления ошибки приложение запустилось

#### http://localhost:3000/graphql/
При обращении к http://localhost:3000/graphql/ возникает ошибка "Cannot GET /graphql/"
```
Опечатка в роуте, в файле index.js: app.use('/graphgl', graphqlRoutes); 
Исправлено на app.use('/graphql', graphqlRoutes);
```
Запустилась GraphQL IDE

#### Query

**events**

argumets is not defined
```
/graphql/resolvers/query.js
Неверный параметр arguments: return models.Event.findAll(argumets, context)
Исправлено на args.
```

Поля users и room выводятся как null
```
/graphql/resolvers/index.js 
Нужен return для вызовов users() и room() 
```

**rooms**

Не выводится первая запись
```
Удален параметр offset в методе models.Room.findAll({ offset: 1 }, context);
```

**findAll**

Неверная сигнатура
```
/graphql/resolvers/query.js
Метод findAll принимает один аргумент - объект параметров.
Все вызовы исправлены на findAll(args)
```

#### Mutation

**createUser**

При добавлении пользователя не задается поле avatarUrl, при этом в схеме указано, что поле не может быть null
```
/graphql/typeDefs.js
Для UserInput добавлено поле avatarUrl
В схеме User для поля avatarUrl убран флаг ! "not null" 
```

**changeEventRoom**

Неверно меняет комнату
```
/graphql/resolvers/mutation.js
В метод setRoom передается неверный setRoom(id)
Исправлено на setRoom(roomId)
```


После выполнения не возвращает объект события
```
В методе changeEventRoom стрелочная функция не возвращает значение:
event => {
            event.setRoom(id);
         }
         
Исправлено на event => event.setRoom(roomId)
```

**addUserToEvent**

Не определен метод addUserToEvent
```
 addUserToEvent (root, { id, userId }, context) {
     return models.Event.findById(id)
        .then(event => {
            return event.addUser(userId)
                .then(() => event)
        });
},
```






# Приложение для создания и редактирования информации о встречах сотрудников

Написано для Node.js 8 и использует библиотеки:
* express
* sequelize
* graphql

## Задание
Код содержит ошибки разной степени критичности. Некоторых из них стилистические, а некоторые даже не позволят вам запустить приложение. Вам необходимо найти и исправить их.

Пункты для самопроверки:
1. Приложение должно успешно запускаться
2. Должно открываться GraphQL IDE - http://localhost:3000/graphql/
3. Все запросы на получение или изменения данных через graphql должны работать корректно. Все возможные запросы можно посмотреть в вкладке Docs в GraphQL IDE или в схеме (typeDefs.js)
4. Не должно быть лишнего кода
5. Все должно быть в едином codestyle

## Запуск
```
npm i
npm run dev
```

Для сброса данных в базе:
```
npm run reset-db
```



# Приложение для создания и редактирования информации о встречах сотрудников

Написано для Node.js 8 и использует библиотеки:
* express
* sequelize
* graphql

## Задание
Код содержит ошибки разной степени критичности. Некоторых из них стилистические, а некоторые даже не позволят вам запустить приложение. Вам необходимо найти и исправить их.

Пункты для самопроверки:
1. Приложение должно успешно запускаться
2. Должно открываться GraphQL IDE - http://localhost:3000/graphql/
3. Все запросы на получение или изменения данных через graphql должны работать корректно. Все возможные запросы можно посмотреть в вкладке Docs в GraphQL IDE или в схеме (typeDefs.js)
4. Не должно быть лишнего кода
5. Все должно быть в едином codestyle

## Запуск
```
npm i
npm run dev
```

Для сброса данных в базе:
```
npm run reset-db
```
