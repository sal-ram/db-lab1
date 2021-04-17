1.	Дана схема базы данных в виде следующих отношений.  С помощью операторов SQL создать логическую структуру соответствующих таблиц для хранения в СУБД, используя известные средства поддержания целостности (NOT NULL, UNIQUE, и т.д.). Обосновать выбор типов данных и используемые средства поддержания целостности. При выборе подходящих типов данных использовать информацию о конкретных значениях полей БД (см. прил.1)

CREATE TABLE "СОТРУДНИК"
![image](https://user-images.githubusercontent.com/64357780/115071819-2856c380-9f10-11eb-9c36-6c9fbe69bda4.png)
2.  Ввести в ранее созданные таблицы конкретные данные (см. прил. 1). Использовать скрипт-файл из операторов INSERT или вспомогательную утилиту.
![image](https://user-images.githubusercontent.com/64357780/114872776-109a1500-9e14-11eb-9a19-6b1db9a3a1a7.png)
3.  Используя оператор SELECT создать запрос для вывода всех строк каждой таблицы. Проверить правильность ввода. При необходимости произвести коррекцию значений операторами INSERT, UPDATE, DELETE. 

ТАБЛИЦА
![image](https://user-images.githubusercontent.com/64357780/114874629-ecd7ce80-9e15-11eb-97e2-42bdb453624a.png)
ТАБЛИЦА
![image](https://user-images.githubusercontent.com/64357780/114874759-109b1480-9e16-11eb-9940-d1e2feffdd68.png)
ТАБЛИЦА
![image](https://user-images.githubusercontent.com/64357780/114874824-214b8a80-9e16-11eb-91d7-9b530163ba3c.png)
ТАБЛИЦА
![image](https://user-images.githubusercontent.com/64357780/114874877-2f011000-9e16-11eb-9ae2-be7f5289009f.png)

4.	Создать запросы для вывода:
a)	всех различных размеров налогов;

SELECT DISTINCT "НАЛОГ" FROM "СОТРУДНИК";
![image](https://user-images.githubusercontent.com/64357780/114876777-198ce580-9e18-11eb-8efa-7549d65d5a37.png)

SELECT DISTINCT "ОТЧИСЛЕНИЕ В ПЕНСИОННЫЙ ФОНД" FROM "МЕСТО РАБОТЫ";
![image](https://user-images.githubusercontent.com/64357780/114877129-6ffa2400-9e18-11eb-9102-6c6615a37727.png)
b)	всех различных мест работы;

SELECT DISTINCT "НАЗВАНИЕ ОРГ." FROM "МЕСТО РАБОТЫ";
![image](https://user-images.githubusercontent.com/64357780/114877827-1a724700-9e19-11eb-9b79-423d5408c2f2.png)
c)	всех различных районов проживания сотрудников.

SELECT DISTINCT "АДРЕС" FROM "СОТРУДНИК";
![image](https://user-images.githubusercontent.com/64357780/114878131-5c02f200-9e19-11eb-936f-2b3212beed0b.png)

5.	Создав запрос получить следующую информацию:

a)	фамилии и адреса сотрудников, имеющих налог более 8%;

SELECT "ФАМИЛИЯ", "АДРЕС" FROM "СОТРУДНИК" WHERE "НАЛОГ" >= 8;
![image](https://user-images.githubusercontent.com/64357780/114880130-3a0a6f00-9e1b-11eb-95fd-c8794530e29f.png)
b)	почасовую оплату и название для должностей, в названии которых встречаются слова “научный сотрудник”;

SELECT "ПОЧАСОВАЯ ОПЛАТА", "НАЗВАНИЕ" FROM "ДОЛЖНОСТЬ" WHERE "НАЗВАНИЕ" like '%научный сотрудник%'
![image](https://user-images.githubusercontent.com/64357780/114918651-bf544a80-9e40-11eb-8fe4-f75161b94c8c.png)
c)	номер, дату и количество часов для тех записей о работе, где плата превышала 100000руб.
SELECT "НОМЕР", "ДАТА", "КОЛ-ВО ЧАСОВ" FROM "РАБОТА" WHERE "ПЛАТА" >= 100000
![image](https://user-images.githubusercontent.com/64357780/114918849-fe829b80-9e40-11eb-8b78-2ad4a0799cbe.png)

6.	На основании данных о работе вывести все данные в таком формате:
a)	номер, фамилия сотрудника, дата, количество часов. Отсортировать по количеству часов;

SELECT РАБОТА.НОМЕР, СОТРУДНИК.ФАМИЛИЯ, РАБОТА.ДАТА, РАБОТА."КОЛ-ВО ЧАСОВ" FROM РАБОТА, СОТРУДНИК ORDER BY РАБОТА."КОЛ-ВО ЧАСОВ";
![image](https://user-images.githubusercontent.com/64357780/114922257-e4e35300-9e44-11eb-8885-b886684f16e4.png)


b)	название работы, должность, дата, плата.

SELECT "МЕСТО РАБОТЫ"."НАЗВАНИЕ ОРГ.", "ДОЛЖНОСТЬ"."НАЗВАНИЕ", "РАБОТА"."ДАТА", "РАБОТА"."ПЛАТА" FROM РАБОТА, "МЕСТО РАБОТЫ", ДОЛЖНОСТЬ 
![image](https://user-images.githubusercontent.com/64357780/114921894-7b634480-9e44-11eb-8890-3c4b95690cf9.png)
ПРОДОЛЖЕНИЕ...
![image](https://user-images.githubusercontent.com/64357780/114921927-85854300-9e44-11eb-84ca-c9503e52f596.png)

7.	Вывести:

a)	названия организаций, где работали доценты или служащие того же района;

SELECT "МЕСТО РАБОТЫ"."НАЗВАНИЕ ОРГ." FROM "МЕСТО РАБОТЫ"
JOIN РАБОТА ON РАБОТА."МЕСТО РАБОТЫ" = "МЕСТО РАБОТЫ".ИДЕНТИФИКАТОР
JOIN ДОЛЖНОСТЬ ON РАБОТА.ДОЛЖНОСТЬ = ДОЛЖНОСТЬ.ИДЕНТИФИКАТОР 
WHERE ДОЛЖНОСТЬ.НАЗВАНИЕ = ('Доцент')
UNION SELECT "МЕСТО РАБОТЫ"."НАЗВАНИЕ ОРГ." FROM "МЕСТО РАБОТЫ" 
JOIN РАБОТА ON РАБОТА."МЕСТО РАБОТЫ" = "МЕСТО РАБОТЫ".ИДЕНТИФИКАТОР
JOIN СОТРУДНИК ON РАБОТА.СОТРУДНИК = СОТРУДНИК.ИДЕНТИФИКАТОР 
WHERE СОТРУДНИК.АДРЕС = "МЕСТО РАБОТЫ".АДРЕС;

![image](https://user-images.githubusercontent.com/64357780/115071880-41f80b00-9f10-11eb-8b7b-c1d4e11cf9d7.png)

b)	фамилии и размер налога для тех работников, которые имели работу с почасовой оплатой менее 15000руб. не ранее января; 
Нет месяцев раньше января, поэтому предполагаю это условие можно не учитывать.

SELECT "СОТРУДНИК"."ФАМИЛИЯ", "СОТРУДНИК"."НАЛОГ" FROM "СОТРУДНИК"
JOIN РАБОТА ON РАБОТА."СОТРУДНИК" = "СОТРУДНИК".ИДЕНТИФИКАТОР
WHERE РАБОТА.ПЛАТА < 15000

![image](https://user-images.githubusercontent.com/64357780/115075187-2262e180-9f14-11eb-984b-1102c1df5be9.png)

c)	название и размер отчислений для организаций, где работал Александров более одного раза.

d)	номер работы, название организации, где работали работники из Советского района. Добавить в вывод фамилии таких работников и отсортировать по названию организации.

SELECT DISTINCT РАБОТА.НОМЕР, "МЕСТО РАБОТЫ"."НАЗВАНИЕ ОРГ.", СОТРУДНИК.ФАМИЛИЯ 
FROM РАБОТА, "МЕСТО РАБОТЫ", СОТРУДНИК
where СОТРУДНИК.АДРЕС = ('Советский') 
ORDER BY "МЕСТО РАБОТЫ"."НАЗВАНИЕ ОРГ.";

![image](https://user-images.githubusercontent.com/64357780/115112791-a06cca00-9fa0-11eb-8186-cd9a26f5f2bd.png)


8.	Создать запрос для модификации всех значений столбца с суммарной величиной платы, чтобы он содержал истинную сумму, полученную работником ( за вычетом налога). Вывести новые значения.

UPDATE РАБОТА SET ПЛАТА = ПЛАТА - ПЛАТА * СОТРУДНИК.НАЛОГ / 100 FROM СОТРУДНИК
WHERE РАБОТА.СОТРУДНИК = СОТРУДНИК.ИДЕНТИФИКАТОР;
SELECT * FROM РАБОТА;

![image](https://user-images.githubusercontent.com/64357780/115114093-f2b0e980-9fa6-11eb-9a7d-3488b65806a8.png)

10.	Расширить таблицу с данными о работах столбцом, содержащим величину отчислений в пенсионный фонд. Создать запрос для ввода конкретных значений во все строки таблицы.







