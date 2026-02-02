# projet-DATALINK-ORACLE-DATABASE
projet DATALINK ORACLE DATABASE

-***************CREATION DATA BASE********************************
CREATE DATABASE nom_de_la_base
  USER sys IDENTIFIED BY mot_de_passe
  USER system IDENTIFIED BY mot_de_passe
  LOGFILE GROUP 1 ('path_to_redo_log_file_1', 'path_to_redo_log_file_2') SIZE 50M,
            GROUP 2 ('path_to_redo_log_file_3', 'path_to_redo_log_file_4') SIZE 50M
  MAXLOGFILES 5
  MAXLOGMEMBERS 5
  MAXDATAFILES 100
  MAXINSTANCES 1
  CHARACTER SET utf8
  NATIONAL CHARACTER SET utf8;


****************CREATION TABLESPACE************************************

CREATE TABLESPACE nom_du_tablespace
  DATAFILE 'path_to_datafile.dbf' SIZE 100M AUTOEXTEND ON;

**************** CREATIN DE UTILISATEUR******************************

CREATE USER nom_utilisateur IDENTIFIED BY mot_de_passe
  DEFAULT TABLESPACE nom_du_tablespace
  TEMPORARY TABLESPACE temp;

GRANT CONNECT, RESOURCE TO nom_utilisateur;

*******************commande RMAN pour cloner une base de données :******************

rman TARGET / AUXILIARY sys@nouvelle_base CATALOG rman_catalog
RMAN> DUPLICATE DATABASE TO nouvelle_base
  FROM ACTIVE DATABASE
  SPFILE
  NOFILENAMECHECK;

******************Commande pour exécuter DBCA en mode silencieux************************

dbca -silent -createDatabase -responseFile /path/to/dbca.rsp


*for linux*











0- ifconfig
0-ping 192.168.37.155
lsnrctl status
lsnrctl start
3- sqlplus / as sysdba
4- def
5- create user  c##UserSite1 identified by 123;
6- conn c##UserSite1/123
7- GRANT CREATE SESSION TO c##UserSite1;
8- grant connect, resource to c##UserSite1;
9- conn c##UserSite1/123;
10- show user
11 - create table xyz (id number , name varchar2(10));
12 - insert into xyz values (1,'kamal');
13- conn / as sysdba
15- GRANT UNLIMITED TABLESPACE TO c##UserSite1;
16- conn c##UserSite1/123;
17- 
insert into xyz values (2,'rachide');
insert into xyz values (3,'said');
insert into xyz values (4,'khalid');
insert into xyz values (5,'isame');
insert into xyz values (6,'imade');
insert into xyz values (7,'walid');
commit;

18- select * from xyz;

19- insert into xyz values (8 , 'sami');
20- commit; 
21- select * from xyz;

-----------------------------------------------------
db2:
1- . oraenv
2- sqlplus / as sysdba
3- !tnsping ORCL   /  !tnsping 192.168.37.144 
4- create user c##UserSite2  identified by 123;
5- grant connect, resource to c##UserSite2;
6- GRANT CREATE SESSION TO c##UserSite2;
6- grant create database link to c##UserSite2;
7- create public database link BD1 connect to c##UserSite1 identified by 123
  using '(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=192.168.37.144)(PORT=1521))(CONNECT_DATA=(SERVICE_NAME=ORCL)))';

8- select * from c##UserSite1.xyz@BD1;
9- insert into c##UserSite1.xyz@BD1 values(9,'mourad');
10- commit;
11- select * from c##UserSite1.xyz@BD1;
12- update c##UserSite1.xyz@BD1 set name='monssif' where id=1;










SQL> !tnsping 192.168.37.144

TNS Ping Utility for Linux: Version 21.0.0.0.0 - Production on 10-MAR-2024 06:43:02

Copyright (c) 1997, 2021, Oracle.  All rights reserved.

Used parameter files:
/home/monsif/Desktop/oo/app/oracle/homes/OraDB21Home1/network/admin/sqlnet.ora

Used EZCONNECT adapter to resolve the alias
Attempting to contact using '(DESCRIPTION=(CONNECT_DATA=(SERVICE_NAME=))(ADDRESS=(PROTOCOL=tcp)(HOST=192.168.37.144)(PORT=1521)))';
OK (120 msec)




SQL> create user c##acer identified by acer quota unlimited on users;

User created.

SQL> 


SQL> grant connect , resource to c##acer;

Grant succeeded.

SQL> 



SQL> grant create database link to c##acer;

Grant succeeded.

SQL> 



SQL> create public database link db4Link connect to c##lenovo identified by lenovo
  2  using '(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=192.168.37.144)(PORT=1521))(CONNECT_DATA=(SERVICE_NAME=ORCL)))';

Database link created.


SQL> grant create session to C##ACER;

Grant succeeded.

SQL> grant select any dictionary to C##ACER;

Grant succeeded.

********************************
SQL> insert into xyz values (7,'walid')
            *
ERROR at line 1:
ORA-01950: no privileges on tablespace 'USERS'

********************************

select * from c##lenovo.xyz@db6link;
********************************
create public database link db6link connect to c##lenovo identified by lenovo
  2  using '(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=192.168.37.144)(PORT=1521))(CONNECT_DATA=(SERVICE_NAME=ORCL)))';

GRANT UNLIMITED TABLESPACE TO c##lenovo;


*for windows*
 create user c##lenovo identified by lenovo quota unlimited on users;
 conn c##lenovo/lenovo

-----------------------

SQL> create user c##del identified by del quota unlimited on users;

User created.

SQL> conn c##lenovo/lenovo
ERROR:
ORA-01045: user C##LENOVO lacks CREATE SESSION privilege; logon denied


Warning: You are no longer connected to ORACLE.
SQL> show user
USER is ""
SQL> conn /as sysdba
Connected.
SQL> grant connect, resource to c##lenovo;

Grant succeeded.

SQL> conn c##lenovo/lenovo
Connected.
SQL> show user
USER is "C##LENOVO"
SQL> create table xyz (id number , name varchar2(10));

Table created.

insert into xyz values (1,'kamal');
insert into xyz values (2,'rachide');
insert into xyz values (3,'said');
insert into xyz values (4,'khalid');
insert into xyz values (5,'isame');
insert into xyz values (6,'imade');
insert into xyz values (7,'walid');
commit;


SQL> select * from xyz;

        ID NAME
---------- ----------
         1 kamal
         2 rachide
         3 said
         4 khalid
         5 isame
         6 imade
         7 walid

7 rows selected.

SQL>




php =
  (DESCRIPTION =
    (ADDRESS = (PROTOCOL = TCP)(HOST = samsung)(PORT = 1521))
    (CONNECT_DATA =
      (SERVER = DEDICATED)
      (SERVICE_NAME = php)
    )
  )

DB2LINK =
  (DESCRIPTION =
    (ADDRESS = (PROTOCOL = TCP)(HOST = 192.168.37.144)(PORT = 1521))
    (CONNECT_DATA =
      (SERVICE_NAME = your_service_name)
    )
  )


-- 1. Connectez-vous avec sqlplus en sysdba
sqlplus / as sysdba

-- 2. Arrêter l’instance
SHUTDOWN IMMEDIATE;

-- 3. Démarrer l’instance en mode mount
STARTUP MOUNT;

-- 4. Afficher la BD en cours
SELECT name FROM v$database;

-- 5. Afficher les fichiers de données
SELECT name FROM v$datafile;

-- 6. Afficher la taille des fichiers de données
SELECT file_name, bytes FROM dba_data_files;

-- 7. Afficher les fichiers de controles
SELECT name FROM v$controlfile;

-- 8. Afficher les fichiers Redolog
SELECT member FROM v$logfile;

-- 9. Ajouter un groupe Redolog redo04 de taille 20 M. Vérifier si le fichier est bien crée.
ALTER DATABASE ADD LOGFILE GROUP 4 ('redo04.log') SIZE 20M;
-- Vous devez vérifier dans votre système de fichiers si le fichier redo04.log a été créé.

-- 10. Ajouter un membre de même taille au dernier groupe ajouté
ALTER DATABASE ADD LOGFILE MEMBER 'redo04b.log' TO GROUP 4;

-- 11. Afficher les groupes Redolog et leur status.
SELECT group#, thread#, member FROM v$log;

-- 12. Supprimer la base de données
DROP DATABASE;

-- 13. Supprimer l’instance
SHUTDOWN ABORT;




