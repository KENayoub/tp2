SQL> connect system
Enter password:
Connected.

SQL> grant all privileges to Etud;

Grant succeeded.

SQL> connect Etud
Enter password:
Connected.
SQL> create table ETDIANT(
  2  CODEETUDIANT varchar(10) primary key,
  3  NOMEETUDIANT varchar(20),
  4  PRENOMETUDIANT varchar(20),
  5  DATENAISSANCE date,
  6  VILLE varchar(10)
  7  );

Table created.

SQL> create table COURS(
  2  CODECOURS varchar(10) primary key,
  3  INTITULE varchar2(20)
  4  NBHEURES number(2)
  5  );
NBHEURES number(2)
*
ERROR at line 4:
ORA-00907: missing right parenthesis


SQL> create table COURS(
  2  CODECOURS varchar(10) primary key,
  3  INTITULE varchar2(20),
  4  NBHEURES number(2)
  5  );

Table created.


SQL> create table RESULTAT(
  2  CODEETUDIANT varchar(10) references ETDIANT(CODEETUDIANT),
  3  CODECOURS varchar(10) references COURS(CODECOURS),
  4  NOTE number(5,2),
  5  constraint pk1 primary key(CODEETUDIANT,CODECOURS)
  6  );

Table created.

SQL> create table ENSEIGNANT(
  2  CODEENSEIGNANT varchar(10) primary key,
  3  NOMENSEIGNANT VARCHAR(20),
  4  PRENOMENSEIGNANT varchar(20),
  5  SPECIALITE varchar(20)
  6  );

Table created.

SQL> create table CHARGE(
  2  CODECOURS varchar(10) references COURS(CODECOURS),
  3  CODEENSEIGNANT varchar(10) references ENSEIGNANT(CODEENSEIGNANT),
  4  constraint pk2 primary key  (CODECOURS,CODEENSEIGNANT)
  5  );

Table created.

SQL> insert into ETDIANT VALUES ('dd1','ddnom','ddprenom','20230523','agadir');
insert into ETDIANT VALUES ('dd1','ddnom','ddprenom','20230523','agadir')
                                                     *
ERROR at line 1:
ORA-01861: literal does not match format string


SQL> insert into ETDIANT VALUES ('dd1','ddnom','ddprenom',TO_DATE('01-01-2001','DD-MM-YYYY'),'agadir');

1 row created.

SQL> insert into ETDIANT VALUES ('dd2','dd22nom','dd22prenom',TO_DATE('01-05-2023','DD-MM-YYYY'),'agadir');

1 row created.

SQL> insert into ETDIANT VALUES ('dd3','dd33nom','dd33prenom',TO_DATE('25-05-2023','DD-MM-YYYY'),'agadir');

1 row created.

SQL> insert into ETDIANT VALUES ('dd4','dd44nom','dd44prenom',TO_DATE('25-05-2023','DD-MM-YYYY'),'agadir');

1 row created.

SQL>
SQL> disconnect
Disconnected from Oracle Database 19c Enterprise Edition Release 19.0.0.0.0 - Production
Version 19.3.0.0.0
SQL>




SQL> connect system
Enter password:
Connected.
SQL> grant all privileges to Etud;

Grant succeeded.

SQL> connect Etud
Enter password:
Connected.

SQL> select * from ETDIANT;

CODEETUDIA NOMEETUDIANT         PRENOMETUDIANT       DATENAISS VILLE
---------- -------------------- -------------------- --------- ----------
dd1        ddnom                ddprenom             01-JAN-01 agadir
dd2        dd22nom              dd22prenom           01-MAY-23 agadir
dd3        dd33nom              dd33prenom           25-MAY-23 agadir
dd4        dd44nom              dd44prenom           25-MAY-23 agadir


SQL> SELECT table_name FROM user_tables
  2  ;

TABLE_NAME
--------------------------------------------------------------------------------
ETDIANT
COURS
RESULTAT
ENSEIGNANT
CHARGT 

SQL> insert into ETDIANT values ( 'dd5','dd55nom','dd55prenom',TO_DATE('23-05-2003','DD-MM-YY'),'casa');

1 row created.

SQL> select * from RESULTAT;

no rows selected

SQL> insert into COURS values ('C01','database',6);

1 row created.


SQL> insert into COURS values ('C02','database',8);

1 row created.

SQL> insert into COURS values ('C03','JAVA',8);

1 row created.

SQL> insert into COURS values ('C05','JAVA',4);

1 row created.

SQL> insert into COURS values ('C06','BASE DE DONNEE',4);

1 row created.

SQL> SELECT * FROM ETDIANT,COURS
  2  ;

CODEETUDIA NOMEETUDIANT         PRENOMETUDIANT       DATENAISS VILLE
---------- -------------------- -------------------- --------- ----------
CODECOURS  INTITULE               NBHEURES
---------- -------------------- ----------
dd5        dd55nom              dd55prenom           23-MAY-03 casa
C01        database                      6

dd1        ddnom                ddprenom             01-JAN-01 agadir
C01        database                      6

dd2        dd22nom              dd22prenom           01-MAY-23 agadir
C01        database                      6


CODEETUDIA NOMEETUDIANT         PRENOMETUDIANT       DATENAISS VILLE
---------- -------------------- -------------------- --------- ----------
CODECOURS  INTITULE               NBHEURES
---------- -------------------- ----------
dd3        dd33nom              dd33prenom           25-MAY-23 agadir
C01        database                      6

dd4        dd44nom              dd44prenom           25-MAY-23 agadir
C01        database                      6

dd5        dd55nom              dd55prenom           23-MAY-03 casa
C02        database                      8


CODEETUDIA NOMEETUDIANT         PRENOMETUDIANT       DATENAISS VILLE
---------- -------------------- -------------------- --------- ----------
CODECOURS  INTITULE               NBHEURES
---------- -------------------- ----------
dd1        ddnom                ddprenom             01-JAN-01 agadir
C02        database                      8

dd2        dd22nom              dd22prenom           01-MAY-23 agadir
C02        database                      8

dd3        dd33nom              dd33prenom           25-MAY-23 agadir
C02        database                      8


CODEETUDIA NOMEETUDIANT         PRENOMETUDIANT       DATENAISS VILLE
---------- -------------------- -------------------- --------- ----------
CODECOURS  INTITULE               NBHEURES
---------- -------------------- ----------
dd4        dd44nom              dd44prenom           25-MAY-23 agadir
C02        database                      8

dd5        dd55nom              dd55prenom           23-MAY-03 casa
C03        JAVA                          8

dd1        ddnom                ddprenom             01-JAN-01 agadir
C03        JAVA                          8


CODEETUDIA NOMEETUDIANT         PRENOMETUDIANT       DATENAISS VILLE
---------- -------------------- -------------------- --------- ----------
CODECOURS  INTITULE               NBHEURES
---------- -------------------- ----------
dd2        dd22nom              dd22prenom           01-MAY-23 agadir
C03        JAVA                          8

dd3        dd33nom              dd33prenom           25-MAY-23 agadir
C03        JAVA                          8

dd4        dd44nom              dd44prenom           25-MAY-23 agadir
C03        JAVA                          8


CODEETUDIA NOMEETUDIANT         PRENOMETUDIANT       DATENAISS VILLE
---------- -------------------- -------------------- --------- ----------
CODECOURS  INTITULE               NBHEURES
---------- -------------------- ----------
dd5        dd55nom              dd55prenom           23-MAY-03 casa
C05        JAVA                          4

dd1        ddnom                ddprenom             01-JAN-01 agadir
C05        JAVA                          4

dd2        dd22nom              dd22prenom           01-MAY-23 agadir
C05        JAVA                          4


CODEETUDIA NOMEETUDIANT         PRENOMETUDIANT       DATENAISS VILLE
---------- -------------------- -------------------- --------- ----------
CODECOURS  INTITULE               NBHEURES
---------- -------------------- ----------
dd3        dd33nom              dd33prenom           25-MAY-23 agadir
C05        JAVA                          4

dd4        dd44nom              dd44prenom           25-MAY-23 agadir
C05        JAVA                          4

dd5        dd55nom              dd55prenom           23-MAY-03 casa
C06        BASE DE DONNEE                4


CODEETUDIA NOMEETUDIANT         PRENOMETUDIANT       DATENAISS VILLE
---------- -------------------- -------------------- --------- ----------
CODECOURS  INTITULE               NBHEURES
---------- -------------------- ----------
dd1        ddnom                ddprenom             01-JAN-01 agadir
C06        BASE DE DONNEE                4

dd2        dd22nom              dd22prenom           01-MAY-23 agadir
C06        BASE DE DONNEE                4

dd3        dd33nom              dd33prenom           25-MAY-23 agadir
C06        BASE DE DONNEE                4


CODEETUDIA NOMEETUDIANT         PRENOMETUDIANT       DATENAISS VILLE
---------- -------------------- -------------------- --------- ----------
CODECOURS  INTITULE               NBHEURES
---------- -------------------- ----------
dd4        dd44nom              dd44prenom           25-MAY-23 agadir
C06        BASE DE DONNEE                4


25 rows selected.

SQL> INSERT INTO RESULTAT VALUES ('dd1','C01',12);

1 row created.

SQL> INSERT INTO RESULTAT VALUES ('dd1','C02',14);

1 row created.

SQL> INSERT INTO RESULTAT VALUES ('dd2','C02',15);

1 row created.

SQL> INSERT INTO RESULTAT VALUES ('dd3','C03',15);

1 row created.

SQL> INSERT INTO RESULTAT VALUES ('dd4','C03',15);

1 row created.

SQL> insert into ENSEIGNANT values ('D001','ahmed','ahmed','database');

1 row created.

SQL> insert into ENSEIGNANT values ('D002','ayoub','ahmed','mobile');

1 row created.

SQL> insert into ENSEIGNANT values ('D003','mohamed','mohamed','java');

1 row created.

SQL> insert into ENSEIGNANT values ('D004','mohamed','mohamed','langue');

1 row created.

SQL> insert into ENSEIGNANT values ('D004','mohamed','amine','reseau');
insert into ENSEIGNANT values ('D004','mohamed','amine','reseau')
*
ERROR at line 1:
ORA-00001: unique constraint (ETUD.SYS_C007460) violated


SQL> insert into ENSEIGNANT values ('D005','mohamed','amine','reseau');

1 row created.

SQL> insert into CHARGE values ('C01','D001');

1 row created.

SQL> insert into CHARGE values ('C02','D002');

1 row created.

SQL> insert into CHARGE values ('C03','D003');

1 row created.


SQL> insert into CHARGE values ('C05','D004');

1 row created.

SQL> insert into CHARGE values ('C06','D005');

1 row created.

SQL> commit
  2  ;

Commit complete.

SQL> update RESULTAT
  2  SET NOTE = NOTE + (NOTE * 5%);
SET NOTE = NOTE + (NOTE * 5%)
                           *
ERROR at line 2:
ORA-00911: invalid character


SQL> update RESULTAT
  2  SET NOTE = NOTE + ((NOTE * 5)/100);

5 rows updated.

SQL> commit
  2  ;

Commit complete.

SQL> update COURS
  2  set INTITULE = 'SGBD'
  3  where CODECOURS = 'C02';

1 row updated.


SQL> delete from RESULTAT
  2  WHERE CODECOURS = 'C05';

0 rows deleted.

SQL> delete from CHARGE
  2  WHERE CODECOURS = 'C05';

1 row deleted.

SQL> delete from COURS
  2  WHERE CODECOURS = 'C05';

1 row deleted.

SQL> COMMIT;

Commit complete.

SQL>  SELECT table_name FROM user_tables;

TABLE_NAME
--------------------------------------------------------------------------------
ETDIANT
COURS
RESULTAT
ENSEIGNANT
CHARGE

SQL>
SQL> select NOMEETUDIANT,VILLE
  2  FROM ETDIANT;

NOMEETUDIANT         VILLE
-------------------- ----------
dd55nom              casa
ddnom                agadir
dd22nom              agadir
dd33nom              agadir
dd44nom              agadir

SQL> select NOMEETUDIANT,VILLE
  2  FROM ETDIANT
  3  ORDER BY NOMEETUDIANT
  4  ;

NOMEETUDIANT         VILLE
-------------------- ----------
dd22nom              agadir
dd33nom              agadir
dd44nom              agadir
dd55nom              casa
ddnom                agadir

SQL> SELECT NOMEETUDIANT,VILLE
  2  FROM ETDIANT
  3  WHERE VILLE ='agadir'or VILLE= 'tiznit';

NOMEETUDIANT         VILLE
-------------------- ----------
ddnom                agadir
dd22nom              agadir
dd33nom              agadir
dd44nom              agadir

SQL> select NOMEETUDIANT,VILLE
  2  FROM ETDIANT
  3  WHERE VILLE IN ('agadir','tiznit','taroudant')
  4  order by VILLE,NOMEETUDIANT;

NOMEETUDIANT         VILLE
-------------------- ----------
dd22nom              agadir
dd33nom              agadir
dd44nom              agadir
ddnom                agadir

SQL> select NOMEETUDIANT,EXTRACT(YEAR FROM SYSDATE) - EXTRACT(YEAR FROM DATENAISSANCE) AS age,VILLE
  2  FROM ETDIANT
  3  ORDER BY VILLE,age;

NOMEETUDIANT                AGE VILLE
-------------------- ---------- ----------
dd22nom                       0 agadir
dd33nom                       0 agadir
dd44nom                       0 agadir
ddnom                        22 agadir
dd55nom                      20 casa

SQL> select NOMEETUDIANT,EXTRACT(YEAR FROM SYSDATE) - EXTRACT(YEAR FROM DATENAISSANCE) AS age
  2  FROM ETDIANT
  3  where age between 17 AND 20
  4  ORDER BY age desc;
where age between 17 AND 20
      *
ERROR at line 3:
ORA-00904: "AGE": invalid identifier


SQL> select NOMEETUDIANT,EXTRACT(YEAR FROM SYSDATE) - EXTRACT(YEAR FROM DATENAISSANCE) AS age
  2  FROM ETDIANT
  3  where EXTRACT(YEAR FROM SYSDATE) - EXTRACT(YEAR FROM DATENAISSANCE)  between 17 AND 20
  4  ORDER BY age desc;

NOMEETUDIANT                AGE
-------------------- ----------
dd55nom                      20

SQL> select NOMEETUDIANT,VILLE
  2  FROM ETDIANT
  3  WHERE VILLE IN ('Casa', 'Taroudant', 'Safi');

no rows selected

SQL> SELECT NOMEETUDIANT
  2  FROM ETDIANT
  3  WHERE NOMEETUDIANT LIKE '%Ben%' OR NOMEETUDIANT LIKE '%oui%';

no rows selected

SQL>