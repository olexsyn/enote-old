# SwimDB

## compet - соревнования

```sql
CREATE TABLE compet (
  compid    MEDIUMINT     UNSIGNED NOT NULL AUTO_INCREMENT PRIMARY KEY,
  compname  VARCHAR(70)            NOT NULL,         /* название */
  dates     VARCHAR(70)            NOT NULL,         /* 2019-05-31,2019-06-01,2019-06-02 */
  course    ENUM('S','L','?')      NOT NULL DEFAULT '?',
  cityid    SMALLINT           DEFAULT NULL,         /* id город */
  poolid    SMALLINT           DEFAULT NULL,         /* id бас. */
  extra     VARCHAR(50)        DEFAULT NULL          /* необходимые примечания */
--
) ENGINE=MyISAM;
```

* compid - id соревнования - от  даты начала - xYYMMDDX
  * x - зарезервировано для годов, позднее 2**099**:
    * макс. значение для unsigned MEDIUMINT 16777215, это позволит отобразить дату 2167-12-31,9 = 16712319
    * для даты, например, 2023-11-25 compid будет выглядеть, как 2311250 (2023-11-25,0)
  * 0 - разряд для совпадающих по дате вместо X: 0,1,2,...,9)
  * пример: соревнования стартуют 2017-11-10: значит 1711100 (если еще какие-то соревнования, то 1711101


## prot - протоколы

```sql
CREATE TABLE prot (
  resid    INT       UNSIGNED NOT NULL AUTO_INCREMENT PRIMARY KEY,
  compid   MEDIUMINT UNSIGNED              NOT NULL DEFAULT '0', /* NULL, например, временно для заграничных */
  course   ENUM('S','L','?')               NOT NULL DEFAULT '?',
  gender   ENUM('M','W')                   NOT NULL,
  stroke   ENUM('FR','FL','BA','BR','IM')  NOT NULL,
  dist     ENUM('50','100','200','400','800','1500') NOT NULL,
  ord      SMALLINT UNSIGNED               NOT NULL DEFAULT '0',   /* место */
  status   ENUM(`,'DNS','EXH','DSQ')      NOT NULL DEFAULT `,
  result   VARCHAR(8)                      NOT NULL DEFAULT '',    /* время, text */
  timing   ENUM('A','S','H','?')          NOT NULL DEFAULT '?',    /* хронометраж: A - автоматический, S - полуавтоматический, H - ручной */
  swrid    SMALLINT UNSIGNED               NOT NULL DEFAULT '0',
  year     YEAR(4)                         NOT NULL DEFAULT '0000',
  lname    VARCHAR(30)                     NOT NULL,               /* фамилия (lastname) */
  fname    VARCHAR(30)                     NOT NULL,               /* имя (firstname) */
  datest   DATE                            NOT NULL DEFAULT '0000-01-01',  /* по дням или дате соревн. */
--
  KEY idx_comp (compid),                      /* выборка всех результатов одного соревнования */
  KEY idx_swr  (swrid),                       /* выборка результатов на разных дистанциях пловца(ов) */
  KEY idx_name (lname, fname),                /* в протоколах, это более важный индекс, чем по swrid */
  KEY idx_dist (stroke, dist, gender, course) /* выборка результатов для одной дистанции с разных соревновнований */
) ENGINE=MyISAM;
```


## res - результаты

```sql
CREATE TABLE res (
  resid    INT       UNSIGNED NOT NULL AUTO_INCREMENT PRIMARY KEY,
  compid   MEDIUMINT UNSIGNED              NOT NULL,
  course   ENUM('S','L','?')               NOT NULL DEFAULT '?',
  gender   ENUM('M','W')                   NOT NULL,
  stroke   ENUM('FR','FL','BA','BR','IM')  NOT NULL,
  dist     ENUM('50','100','200','400','800','1500') NOT NULL,
  swrid    SMALLINT UNSIGNED               NOT NULL DEFAULT '0',
  mstime   MEDIUMINT UNSIGNED              NOT NULL DEFAULT '0',  /* время, мс */
  timing   ENUM('A','S','H','?')          NOT NULL DEFAULT '?',   /* хронометраж: A - автоматический, S - полуавтоматический, H - ручной */
  datest   DATE DEFAULT NULL,                                     /* временно м.б. NULL т.к. есть дата соревнований */
--
  KEY idx_comp (compid)                        /* выборка всех результатов одного соревнования */
  KEY idx_swr  (swrid)                         /* выборка результатов на разных дистанциях пловца(ов) */
  KEY idx_dist (stroke, dist, gender, course)  /* выборка результатов для одной дистанции с разных соревновнований */
) ENGINE=MyISAM;
```

**course** и **gender** дублируются в других таблицах, но здесь присутствуют для удобства и быстроты выборок

Таблица результаты и др. информация из протокола. для естафет - надо другую таблицу

```sql
CREATE TABLE res (
  id       int          unsigned NOT NULL AUTO_INCREMENT PRIMARY KEY,
  compid   mediumint(7) unsigned NOT NULL,             /* id соревнования (см. выше) */
  dat      date                  NOT NULL,
  part     enum('am','pm')       DEFAULT NULL,         /* раздел - утро/вечер, если NULL - то не имеет значения */
  course   enum('S','L')         NOT NULL,             /* вода - короткая/длинная */
  gender   enum('M','F')         NOT NULL,
  stroke   enum('FR','FL','BA','BR','IM') NOT NULL,
  dist     smallint(5)  unsigned NOT NULL,             /* дистанция, м */
  swrid    smallint(5)  unsigned DEFAULT NULL,         /* id пловца, если не найден - NULL */
  year     smallint(5)  unsigned DEFAULT NULL,         /* год рождения по протоколу! ??? */
  mstime   mediumint(8) unsigned DEFAULT NULL,         /* время, мс; NULL - дисквалификация/не_стартовал */
  ord      smallint(3)  unsigned DEFAULT NULL,         /* занятое место (по протоколу!), если NULL - см. причину в state */
  state    tinyint      unsigned DEFAULT NULL,         /* NULL - Ок, 0 - EXH, 1 - DNS, 2...N - DSQ */
  rank1    varchar(8)            DEFAULT NULL,         /* разряд до, по протоколу, если есть */
  rank2    varchar(8)            DEFAULT NULL,         /* разряд после, по протоколу, если есть */
  name     varchar(40)           DEFAULT NULL,         /* фамилия имя пловца, на всякий случай,*/
  city     varchar(40)           DEFAULT NULL,         /* город */
  club     varchar(40)           DEFAULT NULL,         /* клуб */
  fst      enum('У','О','Д','ЗС') DEFAULT NULL,        /* спортивне товариство */
  coaches  varchar(40)           DEFAULT NULL,         /* тренеры, по протоколу, если есть */
  extra    varchar(40)           DEFAULT NULL,         /* необходимые примечания, например, если есть сомнения в имени */
--
  KEY key_compet  (compid,gender,stroke,dist),         /* выборка по дистанциям для одного соревнования */
  KEY key_bestime (course,gender,stroke,dist,mstime),  /* поиск наилучшего времени всех соревнований */
  KEY key_swrtime (swrid)                              /* поиск результатов пловца */
) ENGINE=MyISAM;
```

* если **swrid** не найден, то `NULL`, в **name** - по любому: имя/фамилия из протокола
* **state**: 0 - если не стартовал (DNS), 1 - DSQ (причина не указана), 2 - DSQ (фальстарт), и т.д.
* **state** может быть большим нуля (`DSQ`) при **mstime** большим нуля: дисквалификация, но время учтено
* UNIQUE для **swrid** не действует, пока списки пловцов формируются не из Базы
* "разряд до" **rank1** и после **rank2** - необходимы для истории протокола, ведь разряд меняется
* "разряда до" **rank1** в протоколах может не быть, но его желательно проставить до обновления текущими результатами
* "разряда после" **rank2** тоже может не быть (можно проставить скриптом)

FEATURES:

* при общих стартах должна быть возможность определения победителей и призеров для различных возрастных категорий
* state
  * NULL - если результат защитан,
  * 0 (EXH) - если вне конкурса
  * 1 (DNS) - если не стартовал
  * 2 (DSQ) - дисквалификация без расшифровки
  * 3...N   - id дисквалификации
* [коды дисквалификаций](.db/dsq_codes)

Строка с записью результата должна содержать:

* id-соревнования
* id-спортсмена
* вода (можно брать от соревнования, но будет накладно)
* пол (можно брать от спортсмена, но будет накладно)
* стиль
* длина дистанции
* время в миллисекундах

а также, очевидно

* день (0,1,2..n; от даты соревнования + это значение = дата заплыва)
* id дистанции LW_FRE_400  (course gender style dist)
* предварительное время ? для проставления дорожек и заплывов?
* показанное время
* разряд после (чтобы не вычислять, и т.к. нормативы меняются)
* если эстафета swrid - id команды, в таблице team есть id пловцов


## res - future

Вся информация о заплыве пловца (на будущее, когда и организация и проведение будет через БД).

```sql
DROP TABLE IF EXISTS heat;
CREATE TABLE heat (
  id       int unsigned  NOT NULL AUTO_INCREMENT PRIMARY KEY, /* не , тк не ищем id, только для правок */
  compid   smallint(5)  unsigned NOT NULL,             /* id соревнования 2222 */
  course   enum('S','L')         NOT NULL DEFAULT 'S', /* вода - короткая/длинная */
  gender   enum('M','F','X')     NOT NULL,
  stroke   enum('FR','FL','BA','BR','IM') NOT NULL,
  dist     smallint(5)  unsigned NOT NULL,             /* дистанция, м */

  day      tinyint      unsigned NOT NULL DEFAULT '0', /* день соревнований, первый - 0 */
 ?part     enum('am','pm')       NOT NULL DEFAULT 'am',/* раздел - утро/вечер */
  eventid  tinyint      unsigned NOT NULL DEFAULT '0', /* событие в списке дня (напр, #2. 100м в/ст муж) */
  type     enum('qua','sem','fin') NOT NULL DEFAULT 'fin', /* предвар., полуфин., финальные */
  heat     tinyint      unsigned NOT NULL DEFAULT '0', /* номер заплыва для дистанции */
  lane     tinyint      unsigned NOT NULL DEFAULT '0', /* номер дорожки в заплыве */
  swrid    smallint(5)  unsigned NOT NULL DEFAULT '0', /* id пловца, команды, если эстафета */
  /* name     varchar(40)           NOT NULL,          /* временное поле - фамилия имя пловца */,
  /* msqual   mediumint(8) unsigned NOT NULL DEFAULT '0', /* время квалификации или предварительное */
  rankbef  tinyint      unsigned NOT NULL DEFAULT '0', /* rank before */
  mstime   mediumint(8)          NOT NULL DEFAULT '0', /* время, мс */
  timing   ENUM('A','S','H','?') NOT NULL DEFAULT '?', /* хронометраж: A - автоматический, S - полуавтоматический, H - ручной */
  rankaft  tinyint      unsigned NOT NULL DEFAULT '0', /* rank after */
  ordheat  tinyint               NOT NULL DEFAULT '0', /* занятое место в заплыве */
  ordevent tinyint               NOT NULL DEFAULT '0', /* общее занятое место на дистанции */
  dateup   timestamp             NOT NULL DEFAULT CURRENT_TIMESTAMP, /* время внесения записи */
--
  /* UNIQUE unq (compid,day,part,stroke,dist,swrid), * course заложен в compid, gender в swrid */
  KEY key_bestime (course,gender,stroke,dist,mstime), /* поиск наилучшего времени всех соревнований */
  KEY key_swrtime (swrid,mstime),                    /* поиск результатов пловца */
  KEY key_order   (compid,eventid,ordevent)          /* в порядке завоеванных мест */
) ENGINE=MyISAM;
```

* **ordevent** может повторяться, как и иметь пропуски: 1,2,3,3,5,6,6,6,9,10...

### Привязка к г/р в соревнованиях не нужны?

:idea: что, если

рейтинг после соревнований - один, только по времени, кто как проплыл и взрослые и дети. Но этот рейтинг можно перестроить по заданным годам (какие угодно, возможно даже М + Ж). Это прикольно, ни у кого такого рейтинга нет! И подстегнет некоторых - если девчонки будут выше пацанов (в разрядах, понятно, надо учитывать пол)

Это решает проблему, когда проводятся одни соревнования для различных годов участников 1999-2000, 2001-2002, 2003-2004

Зачем несколько протоколов? Протокол один. Интересует - рейтинг относительно годов участников - указываем год - получаем перестроенный протокол.

построение:
* только указанные года
* указанные года + младшие (тогда младшие могут попасть в призы)
* показывать старших, как EXH (вне конкурса)


## records - рекорды

Для построения рейтингов, информации о лучших результатах пловца на различных дистанциях...

После внесения результатов в rec надо запускать скрипт, который будет обновлять/добавлять личные рекорды пловцов в эту таблицу.

## DB simple

```sql
CREATE TABLE compet (
  compid    SMALLINT      UNSIGNED NOT NULL AUTO_INCREMENT PRIMARY KEY,
  compname  VARCHAR(70)            NOT NULL,         /* название */
  datstart  DATE                   NOT NULL,
  datfinish DATE                   NOT NULL,
  course    ENUM('S','L','?')      NOT NULL DEFAULT '?',
  cityid    SMALLINT           DEFAULT NULL,         /* id город */
  poolid    SMALLINT           DEFAULT NULL,         /* id бас. */
  extra     VARCHAR(50)        DEFAULT NULL,         /* необходимые примечания */
--
) ENGINE=MyISAM;
```

:warning: желательно, чтобы данные ENUM имели одинаковое кол-во симв., что удобно для правки и просмотра

```sql
CREATE TABLE res (
  resid    INT      UNSIGNED NOT NULL AUTO_INCREMENT PRIMARY KEY,
  compid   SMALLINT UNSIGNED               NOT NULL,
  course   ENUM('S','L','?')               NOT NULL DEFAULT '?',
  gender   ENUM('M','W')                   NOT NULL,
  stroke   ENUM('FR','FL','BA','BR','IM')  NOT NULL,
  dist     ENUM('050','100','200','400','800','150') NOT NULL,
  swrid    SMALLINT UNSIGNED               NOT NULL DEFAULT '0',
  mstime   MEDIUMINT UNSIGNED              NOT NULL DEFAULT '0',  /* время, мс */
  timing   ENUM('A','S','H','?')           NOT NULL DEFAULT '?',  /* хронометраж: A - автоматический, S - полуавтоматический, H - ручной */
  datest   DATE DEFAULT NULL, /* временно м.б. NULL т.к. есть дата соревнований */
--
  KEY idx_comp (compid)                        /* выборка всех результатов одного соревнования */
  KEY idx_swr  (swrid)                         /* выборка результатов на разных дистанциях пловца(ов) */
  KEY idx_dist (stroke, dist, gender, course)  /* выборка результатов для одной дистанции с разных соревновнований */
) ENGINE=MyISAM;
```

**course** и **gender** дублируются в других таблицах, но здесь присутствуют для удобства и быстроты выборок

## rank - нормативные нормы

Т.к. предполагает частое обращение - тип `MEMORY` (стр. 132).

Очищается при перезагрузке MySQL, поэтому, проверять взятием контрольного значения с заполнением, в случае очистки.

### rank (memory)

Аналогична **rank_st**, за исключением:

```sql
ENGINE=MEMORY;
```

создается программно.

:warning: Хеш-индекс хорошо подходит для точной выборки из таблиц MEMORY. Это стандартный тип индекса для таблиц MEMORY. При выполнении сравнений по диапазону значений в таблицах MEMORY необходимо воспользоваться индексом с двоичным деревом. Для этого в объявлении индекса нужно добавить ключевое слово USING BTREE

```sql
PRIMARY KEY USING BTREE(id)
```

[Принимайте во внимание соответствие типа индекса типу операции сравнения](/mysql/indexes/choose_index#prinimajte_vo_vnimanie_sootvetstvie_tipa_indeksa_tipu_operacii_sravnenija)
### rank_st (st - stable)

```sql
CREATE TABLE rank_st (
  id     smallint(5)  unsigned NOT NULL PRIMARY KEY,
  rid    tinyint      unsigned NOT NULL,
  course enum('S','L')         NOT NULL,
  gender enum('M','W')         NOT NULL,
  stroke enum('FR','FL','BA','BR','IM') NOT NULL,
  dist   smallint(5)  unsigned NOT NULL,
  mstime mediumint(8) unsigned NOT NULL,
  timing   ENUM('A','S','H','?') NOT NULL DEFAULT '?',  /* хронометраж: A - автоматический, S - полуавтоматический, H - ручной */

--
  KEY key_main (course,gender,stroke,dist,mstime)
) ENGINE=MyISAM;


LOCK TABLES rank_st WRITE;

INSERT INTO rank_st VALUES
(  1, 7, 'S', 'W','FRE',  50,  27000),
(  2, 6, 'S', 'W','FRE',  50,  28000),
(  3, 5, 'S', 'W','FRE',  50,  30500),
(  4, 4, 'S', 'W','FRE',  50,  34000),
(  5, 3, 'S', 'W','FRE',  50,  38000),

...

(412, 7, 'L', 'M','IMD', 400, 282000),
(413, 6, 'L', 'M','IMD', 400, 298000),
(414, 5, 'L', 'M','IMD', 400, 321000),
(415, 4, 'L', 'M','IMD', 400, 357000),
(416, 3, 'L', 'M','IMD', 400, 403000);

UNLOCK TABLES;
```

[полная версия](projects:swimming:dev:db:rank_st)

* `PRIMARY KEY` в rank и rank_st нужен для определения стиля и дистанции. Это значение (1..416) будет записываться в таблицу разрядов `rankset`, чтобы знать не только самый лучший разряд спортсмена, но и другие разряды на других дистанциях.

| short | 100m | FREE | **1:01.08** | II | 2016-03-14 |
| long  | 100m | FREE | **1:02.45** | II | 2015-11-29 |


  select rid, course, stroke, dist, mstime from rank where id=234;


| rid | course | stroke | dist | mstime |
|   2 | L      | FRE    |  200 | 211000 |


### swrranks

История разрядов пловцов.

Можем узнать разряд пловца на конкретной дистанции, когда был установлен лучший разряд - есть действительный.


```sql
CREATE TABLE rank_st (
  id     int  unsigned NOT NULL PRIMARY KEY AUTOINCREMENT,
  datecr /* дата установления */
  rid    tinyint      unsigned NOT NULL, /* rank id*/
  course enum('S','L')         NOT NULL, /**/
  gender enum('M','W')         NOT NULL,
  dist   smallint(5)  unsigned NOT NULL,
  stroke enum('FR','FL','BA','BR','IM') NOT NULL,
  mstime mediumint(8) unsigned NOT NULL,
--
  KEY key_main (course,gender,stroke,dist,mstime)
) ENGINE=MyISAM;
```
