# CodingExemplarAnswers
This is just answers from this test:https://gist.github.com/brandonsavage/65f413d6b508e3849c8fd07f3f407ac6
<hr>
<strong>Question 1</strong>

You've been tasked with identifying a string that contains the word "superman" (case insensitive). You've written the following code:
<br>
<code>
<?php

if(!strpos(strtolower($str), 'superman')) {
    throw new Exception;
}
</code><br>
QA has come to you and said that this works great for strings like "I love superman", but an exception is generated for strings like "Superman is awesome!", which should not happen. Explain why this occurs, and show how you would solve this issue (you must use strpos() in your answer).
****************************************************************************************************
<strong>Answer:</strong>
you need check strpos answer with === because if 'superman' will located in a first position strpos will return 0 and it will be recognized as FALSE, if strpos can not find string - it will return FALSE, so, answer will be or False or something number starting from 0
<code>
<?php
if(strpos(strtolower($str), 'superman')===false) {
    throw new Exception;
}
</code>
<hr>
<strong>Question 2</strong>

A client has called and said that they're noticing performance problems on their database when searching for a user by email address. You've checked, and the following query is running:<br>
<code>
SELECT * FROM users WHERE email = 'user@test.com';
</code><br>
You run the EXPLAIN command and get the following results:<br>
<pre>
+----+-------------+-------+------+---------------+------+---------+------+-------+-------------+
| id | select_type | table | type | possible_keys | key  | key_len | ref  | rows  | Extra       |
+----+-------------+-------+------+---------------+------+---------+------+-------+-------------+
|  1 | SIMPLE      | users | ALL  | NULL          | NULL | NULL    | NULL | 10320 | Using where |
+----+-------------+-------+------+---------------+------+---------+------+-------+-------------+
</pre>
Offer a theory as to why the performance is slow.
****************************************************************************************************
<strong>Answer:</strong>
we can create index for field email, because table have not any indexes, and MySql will do full scan of this table. if we add index for field email - Mysql will use this and query will be faster. i think email of users will have unique values<br>
<code>
ALTER TABLE  `users` ADD UNIQUE (`email`)
</code>
