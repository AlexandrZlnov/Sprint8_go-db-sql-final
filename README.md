### Parcel tracker
Это простой сервис отслеживания посылок, написанный на Go с использованием СУБД SQLite, со следующий функционалом:
  * регистрация новой посылки
  * получение списка посылок клиента
  * изменение статуса посылки
  * изменение адреса доставки
  * удаление посылки
* * * *
#### Основные принцыпы работы:
  * Информация о посылках хранится в БД
  * Посылка может быть зарегистрирована, отправлена или доставлена
  * При регистрации посылки создаётся новая запись в БД
  * У только что зарегистрированной должен быть статус «зарегистрирована»
  * Трек-номер посылки равен её идентификатору в таблице
  * Если посылка в статусе «зарегистрирована», можно изменить адрес доставки или удалить посылку
* * * *
#### Структура проекта:
  * `main.go` точка входа в программу:
    - реализует подключается к базе данных SQLite  
    - описывает структуру `Parcel` представляет посылку с полями: номер, id клиента, статус, адрес, дата создания  
    - описывает `ParcelService` реализует логику работы с посылками и использует объект типа `ParcelStore` для работы с данными о посылке. Включает методы:  
      - `Register` регистрирует новую посылку, присваивает статус “registered”, генерирует дату создания и сохраняет в `ParcelStore`  
      - `PrintClientParcels` выводит на консоль список посылок для указанного клиента  
      - `NextStatus` обновляет статус посылки в соответствии с логикой (registered -> sent -> delivered)  
      - `ChangeAddress` изменяет адрес посылки
      - `Delete` удаляет посылку из хранилища
  * `parcel.go` - реализация методов стуктуры `ParcelStore`, описывающих CRUD операции взаимодействия с базой данных SQL.
* * * *
#### Запуск
`go run main.go`
* * * *
#### Пример результатов работы

