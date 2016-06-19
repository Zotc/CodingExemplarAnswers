# CodingExemplarAnswers
This is just answers from this test:https://gist.github.com/brandonsavage/65f413d6b508e3849c8fd07f3f407ac6
<hr>
<strong>Question 1</strong>

You've been tasked with identifying a string that contains the word "superman" (case insensitive). You've written the following code:
<br>
```php
<?php
if(!strpos(strtolower($str), 'superman')) {
    throw new Exception;
}
?>
```
QA has come to you and said that this works great for strings like "I love superman", but an exception is generated for strings like "Superman is awesome!", which should not happen. Explain why this occurs, and show how you would solve this issue (you must use strpos() in your answer).
****************************************************************************************************
<strong>Answer:</strong>
you need check strpos answer with === because if 'superman' will located in a first position strpos will return 0 and it will be recognized as FALSE, if strpos can not find string - it will return FALSE, so, answer will be or False or something number starting from 0
```php
<?php
if(strpos(strtolower($str), 'superman')===false) {
    throw new Exception;
}
?>
```

<hr>
<strong>Question 2</strong>

A client has called and said that they're noticing performance problems on their database when searching for a user by email address. You've checked, and the following query is running:<br>
```sql
SELECT * FROM users WHERE email = 'user@test.com';
```
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
```sql
ALTER TABLE  `users` ADD UNIQUE (`email`);
```

<hr>
<strong>Question 3</strong>
Starting with PHP 5.5, what is the recommended way to hash user passwords? Show some code that illustrates how you would hash a user's password, and also how you would check that a password supplied by a user matches the password on file.

If your client cannot upgrade to PHP 5.5, and you have to hash passwords using existing PHP libraries, what is one library/package that makes this easy?

<strong>Answer</strong>
starting with PHP 5.5 is recomended use included hashing function<br>
password_hash();  - create hash for password<br>
password_verify(); - that the given hash matches the given password<br>
<br>
as example see next code<br>
```php
<?php
$clearPassword="qwerty";
// PASSWORD_BCRYPT - is a recommended algorithm of password hashing
$hash = password_hash($clearPassword,PASSWORD_BCRYPT);

if (password_verify($clearPassword, $hash)) {
    echo 'Password is valid!';
} else {
    echo 'Invalid password.';
}
?>
```
<hr>
<strong>Question 4</strong>

You're given a sorted index array that contians no keys. The array contains only integers, and your task is to identify whether or not the integer you're looking for is in the array. Write a function that searches for the integer and returns true or false based on whether the integer is present. Describe how you arrived at your solution.<br>

<strong>Answer</strong>
PHP have a good function, called in_array(checkedValue, ourArray)<br>
so, solution for this question look like this:

```php
$checkedValue=6;
$ourArray=array(1,2,4,6,7,10,13,17,33);

if(in_array($checkedValue,$ourArray)) {
    echo "Array has value ".$checkedValue;
} else {
    echo "Array has not value ".$checkedValue;
}
```
<hr>
<strong>Question 5</strong>

During a large data migration, you get the following error: Fatal error: Allowed memory size of 134217728 bytes exhausted (tried to allocate 54 bytes). You've traced the problem to the following snippet of code:
<br>
```php
$stmt = $pdo->prepare('SELECT * FROM largeTable');
$stmt->execute();
$results = $stmt->fetchAll(PDO::FETCH_ASSOC);
foreach ($results as $result) {
    // manipulate the data here
}
```
Refactor this code so that it stops triggering the memory error.
<strong>Answer</strong>
in a row $results = $stmt->fetchAll(PDO::FETCH_ASSOC); all rows of resoult will load into  variable $results, if resoult of select has many rows - we can have error - allowed memory size of...
so, solution for this problem you will see below
```php
$stmt = $pdo->prepare('SELECT * FROM largeTable');
$stmt->execute();
while ($result = $stmt->fetch(PDO::FETCH_ASSOC, PDO::FETCH_ORI_NEXT)) {
    // manipulate the data here
}
```
