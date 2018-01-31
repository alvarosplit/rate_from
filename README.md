Rate MAIL FROM to avoid mailings.

Alvaro Marin Illera - Oct 2008 - split@splitcc.net

Installation steps:

mysql> create database rate_from;

mysql> use rate_from;

mysql> create table rate_from (
       id int NOT NULL auto_increment,
       mail_from varchar(150) NOT NULL,
       count int(10),
       timestamp int(11),
       PRIMARY KEY  (`id`),
       KEY `mail_from` (`mail_from`)
);

mysql> create table rate_from_default (
       id int NOT NULL auto_increment,
       mail_from varchar(150) NOT NULL,
       count int(10),
       PRIMARY KEY  (`id`),
       KEY `mail_from` (`mail_from`)
);

Set the default limit:

mysql> insert into rate_from_default values("","default","100");

You can insert in rate_from_default a different value for some accounts:

mysql> insert into rate_from_default values("","foo@foobar.com","1000");

Set permissions to access:

mysql> grant all on rate_from.* to user@'127.0.0.1' identified by "password";

Create an archive called: /var/log/rate_from.log with write permissions for qmail user.
