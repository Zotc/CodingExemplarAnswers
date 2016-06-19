# CodingExemplarAnswers
This is just answers from this test:https://gist.github.com/brandonsavage/65f413d6b508e3849c8fd07f3f407ac6
=====================================================================================================
Question 1

You've been tasked with identifying a string that contains the word "superman" (case insensitive). You've written the following code:

<?php

if(!strpos(strtolower($str), 'superman')) {
    throw new Exception;
}
QA has come to you and said that this works great for strings like "I love superman", but an exception is generated for strings like "Superman is awesome!", which should not happen. Explain why this occurs, and show how you would solve this issue (you must use strpos() in your answer).
****************************************************************************************************
Answer:
you need check strpos answer with === because if 'superman' will located in a first position strpos will return 0 and it will be recognized as FALSE, if strpos can not find string - it will return FALSE, so, answer will be or False or something number starting from 0
<?php
if(strpos(strtolower($str), 'superman')===false) {
    throw new Exception;
}
=====================================================================================================
Question 2

A client has called and said that they're noticing performance problems on their database when searching for a user by email address. You've checked, and the following query is running:

SELECT * FROM users WHERE email = 'user@test.com';
You run the EXPLAIN command and get the following results:

+----+-------------+-------+------+---------------+------+---------+------+-------+-------------+
| id | select_type | table | type | possible_keys | key  | key_len | ref  | rows  | Extra       |
+----+-------------+-------+------+---------------+------+---------+------+-------+-------------+
|  1 | SIMPLE      | users | ALL  | NULL          | NULL | NULL    | NULL | 10320 | Using where |
+----+-------------+-------+------+---------------+------+---------+------+-------+-------------+
Offer a theory as to why the performance is slow.
****************************************************************************************************
Answer:
we can create index for field email, because table have not any indexes, and MySql will do full scan of this table. if we add index for field email - Mysql will use this and query will be faster. i think email of users will have unique values

ALTER TABLE  `users` ADD UNIQUE (`email`)
