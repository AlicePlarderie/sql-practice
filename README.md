# sql-practice
база данных - "Компьютерная фирма"
Схема БД состоит из четырех таблиц:
Product(maker, model, type)
PC(code, model, speed, ram, hd, cd, price)
Laptop(code, model, speed, ram, hd, price, screen)
Printer(code, model, color, type, price)
Таблица Product представляет производителя (maker), номер модели (model) и тип ('PC' - ПК, 'Laptop' - ПК-блокнот или 'Printer' - принтер). Предполагается, что номера моделей в таблице Product уникальны для всех производителей и типов продуктов. В таблице PC для каждого ПК, однозначно определяемого уникальным кодом – code, указаны модель – model (внешний ключ к таблице Product), скорость - speed (процессора в мегагерцах), объем памяти - ram (в мегабайтах), размер диска - hd (в гигабайтах), скорость считывающего устройства - cd (например, '4x') и цена - price (в долларах). Таблица Laptop аналогична таблице РС за исключением того, что вместо скорости CD содержит размер экрана -screen (в дюймах). В таблице Printer для каждой модели принтера указывается, является ли он цветным - color ('y', если цветной), тип принтера - type (лазерный – 'Laser', струйный – 'Jet' или матричный – 'Matrix') и цена - price.
>----------------------------
1st task:
  Найдите номер модели, скорость и размер жесткого диска для всех ПК стоимостью менее 500 дол. Вывести: model, speed и hd
select model, speed, hd from PC where price < 500
select model, speed, hd from Laptop where price < 500
select model from Printer where price < 500

output: 
model  speed  hd
1232  500  10.0
1232  450  8.0
1232  450  10.0
1260  500  10.0
>----------------------------
2nd task:
  Найдите номер модели, объем памяти и размеры экранов ПК-блокнотов, цена которых превышает 1000 дол.
select model, ram, screen from Laptop where price > 1000

output:
model  ram  screen
1750  128  14
1298  64  15
1752  128  14
>----------------------------
3rd task:
  Найдите все записи таблицы Printer для цветных принтеров.
Select * from Printer where color = 'y'

output:
code  model  color  type  price
3  1434  y  Jet  290.0000
2  1433  y  Jet  270.0000
>----------------------------
4th task:
  Найдите номер модели, скорость и размер жесткого диска ПК, имеющих 12x или 24x CD и цену менее 600 дол.
select model, speed, hd from PC where (cd = '12x' or cd = '24x') and price < 600

output:
model  speed  hd
1232  500  10.0
1232  450  8.0
1232  450  10.0
1260  500  10.0
>----------------------------
5th task:
  Добавить в таблицу PC следующую модель:
  code: 20
  model: 2111
  speed: 950
  ram: 512
  hd: 60
  cd: 52x
  price: 1100
insert into PC (code, model, speed, ram, hd, cd, price)
values (20,2111,950,512,60,'52x',1100)
>----------------------------
6th task:
  Добавить в таблицу Product следующие продукты производителя Z:
  принтер модели 4003, ПК модели 4001 и блокнот модели 4002
insert into Product (maker,model,type)
values ('Z',4003,'Printer'), ('Z',4001,'PC'),('Z',4002,'Laptop')
>----------------------------
7th task:
  Добавить в таблицу PC модель 4444 с кодом 22, имеющую скорость процессора 1200 и цену 1350.
insert into PC (code, model, speed, price)
values (22, 4444, 1200, 1350)
>----------------------------
8th task:
  Найдите модели принтеров, имеющих самую высокую цену. Вывести: model, price
Select model, price from Printer where price = (select max(price) from Printer)
>----------------------------
9th task:
  Найдите среднюю скорость ПК.
select avg(speed) from PC
>----------------------------
10th task:
  Найдите среднюю скорость ПК-блокнотов, цена которых превышает 1000 дол.
select avg(speed) from Laptop where price > 1000
