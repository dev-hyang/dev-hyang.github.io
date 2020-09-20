---
layout:     post
title:      2020-09-10-Database CP02 - Stored Procedures
subtitle:   
date:       2020-09-10
author:     Elon
header-img: img/post-bg-desk.jpg
catalog: true
tags:
    - Database
    - SQL
    - Stored Procedures
---
## What's Stored Procedures in SQL?
A stored procedure is a user defined piece of code written in the local version of PL/SQL, which may return a value(making it a function) that is invoked by calling it explicitly. For example, below CLP script creates a PL/SQL function and procedure, and then calls the PL/SQL proc.
	
	CONNECT TO mydb
	/(from IBM DB2)
	CREATE TABLE emp (
	     name            VARCHAR2(10),
	     salary          NUMBER,
	     comm            NUMBER,
	     tot_comp        NUMBER
	)
	/
	INSERT INTO emp VALUES ('Larry', 1000, 50, 0)
	/
	INSERT INTO emp VALUES ('Curly', 200, 5, 0)
	/
	INSERT INTO emp VALUES ('Moe', 10000, 1000, 0)
	/
	CREATE OR REPLACE FUNCTION emp_comp (
	     p_sal           NUMBER,
	     p_comm          NUMBER )
	RETURN NUMBER
	IS
	BEGIN
	    RETURN (p_sal + NVL(p_comm, 0)) * 24;
	END emp_comp
	/
	CREATE OR REPLACE PROCEDURE update_comp(p_name IN VARCHAR) AS
	BEGIN
	    UPDATE emp SET tot_comp = emp_comp(salary, comm)
	      WHERE name = p_name;
	END update_comp
	/
	CALL update_comp('Curly')
	/
	SELECT * FROM emp
	/
	CONNECT RESET
	/
## What's trigger in SQL?
A trigger is a stored procedure that runs automatically when various events happen(eg. update, insert, delete). For example:
	
	CREATE TABLE T1 (c1 INT, c2 CHAR(2))@
	CREATE TABLE T2 (c1 INT, c2 CHAR(2))@
	CREATE or replace PROCEDURE proc(IN val INT, IN name CHAR(2))
	LANGUAGE SQL 
	DYNAMIC RESULT SETS 0
	MODIFIES SQL DATA
	BEGIN
	  DECLARE rc INT DEFAULT 0;
	  INSERT INTO T2 VALUES (val, name);
	  GET DIAGNOSTICS rc = ROW_COUNT;
	  IF ( rc > 0 ) THEN
	      RETURN 0;
	  ELSE
	      RETURN -200;
	  END IF;
	END@
	CREATE or replace TRIGGER trig1 AFTER UPDATE ON t1
	REFERENCING NEW AS n
	FOR EACH ROW 
	WHEN (n.c1 > 100)
	BEGIN ATOMIC
	   DECLARE rc INTEGER DEFAULT 0;
	   CALL proc(n.c1, n.c2);
	   GET DIAGNOSTICS rc = RETURN_STATUS;
	   VALUES(CASE WHEN rc < 0 THEN CAST(RAISE_ERROR('70001', 'PROC CALL failed') as varchar(70))END);
	END@
	/Issuing below statement will fire the trigger and the procedure will be invoked.
	UPDATE T1 SET c1 = c1+1 WHERE c2 = 'CA'@
## Client/Server SQL engines VS SQLite
Longer answer:  With SQLite, your application is the stored procedure.
**In a traditional client/server database like PostgreSQL or Oracle or
SQL Server, every SQL statement involves a round-trip to the server.
So there is a lot of latency with each command.  The way applications
overcome this latency is to put many queries into a stored procedure,
so that only the stored procedure invocation needs to travel over the
wire and latency is reduced to a single server round-trip**.

But with SQLite, each statement is just a procedure call.  There is no
network traffic, not IPC, and hence very little latency.  Applications
that use SQLite can be very "chatty" with the database and that is not
a problem.  For example, the SQLite website is backed by SQLite (duh!)
and a typical page request involves 200 to 300 separate queries.  That
would be a performance killer with a client/server database, but with
SQLite it is not a problem and the pages render in about 5

## Other resources
TBD