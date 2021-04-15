1.	Дана схема базы данных в виде следующих отношений.  С помощью операторов SQL создать логическую структуру соответствующих таблиц для хранения в СУБД, используя известные средства поддержания целостности (NOT NULL, UNIQUE, и т.д.). Обосновать выбор типов данных и используемые средства поддержания целостности. При выборе подходящих типов данных использовать информацию о конкретных значениях полей БД (см. прил.1)
CREATE TABLE "СОТРУДНИК"
(
    "ИДЕНТИФИКАТОР" INTEGER NOT NULL GENERATED BY DEFAULT AS IDENTITY,
    "ФАМИЛИЯ" varchar(100),
    "АДРЕС" varchar(100),
    "НАЛОГ" smallint CHECK ("НАЛОГ" <= 100 AND "НАЛОГ" >= 0),
    PRIMARY KEY ("ИДЕНТИФИКАТОР")
);

CREATE TABLE "МЕСТО РАБОТЫ"
(
    "ИДЕНТИФИКАТОР" integer NOT NULL GENERATED BY DEFAULT AS IDENTITY,
    "НАЗВАНИЕ ОРГ." varchar(100),
    "АДРЕС" varchar(100),
    "ОТЧИСЛЕНИЕ В ПЕНСИОННЫЙ ФОНД" smallint CHECK ("ОТЧИСЛЕНИЕ В ПЕНСИОННЫЙ ФОНД" <= 100 AND "ОТЧИСЛЕНИЕ В ПЕНСИОННЫЙ ФОНД" >= 0),
    PRIMARY KEY ("ИДЕНТИФИКАТОР")
);

CREATE TABLE "ДОЛЖНОСТЬ"
(
    "ИДЕНТИФИКАТОР" integer NOT NULL GENERATED BY DEFAULT AS IDENTITY,
    "НАЗВАНИЕ" varchar(100),
    "ПОЧАСОВАЯ ОПЛАТА" INTEGER,
    "МАКС. ЧИСЛО ЧАСОВ" INTEGER,
	PRIMARY KEY ("ИДЕНТИФИКАТОР")
);

CREATE TABLE "РАБОТА"
(
    "НОМЕР" INTEGER NOT NULL GENERATED BY DEFAULT AS IDENTITY,
    "СОТРУДНИК" varchar(100),
    "ДАТА" varchar(50),
    "МЕСТО РАБОТЫ" INTEGER,
    "ДОЛЖНОСТЬ" varchar(100),
	"КОЛ-ВО ЧАСОВ" INTEGER,
	"ПЛАТА" INTEGER,
	PRIMARY KEY ("НОМЕР")
);
