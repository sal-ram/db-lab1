1.	Дана схема базы данных в виде следующих отношений.  С помощью операторов SQL создать логическую структуру соответствующих таблиц для хранения в СУБД, используя известные средства поддержания целостности (NOT NULL, UNIQUE, и т.д.). Обосновать выбор типов данных и используемые средства поддержания целостности. При выборе подходящих типов данных использовать информацию о конкретных значениях полей БД (см. прил.1)
CREATE TABLE "СОТРУДНИК"
![image](https://user-images.githubusercontent.com/64357780/114863950-d4fa4d80-9e09-11eb-95b3-8e7f3eee4be4.png)
2.  Ввести в ранее созданные таблицы конкретные данные (см. прил. 1). Использовать скрипт-файл из операторов INSERT или вспомогательную утилиту.
![image](https://user-images.githubusercontent.com/64357780/114872776-109a1500-9e14-11eb-9a19-6b1db9a3a1a7.png)
3.  Используя оператор SELECT создать запрос для вывода всех строк каждой таблицы. Проверить правильность ввода. При необходимости произвести коррекцию значений операторами INSERT, UPDATE, DELETE. 
![image](https://user-images.githubusercontent.com/64357780/114874629-ecd7ce80-9e15-11eb-97e2-42bdb453624a.png)

![image](https://user-images.githubusercontent.com/64357780/114874759-109b1480-9e16-11eb-9940-d1e2feffdd68.png)

![image](https://user-images.githubusercontent.com/64357780/114874824-214b8a80-9e16-11eb-91d7-9b530163ba3c.png)

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

