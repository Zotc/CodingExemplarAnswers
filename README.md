# CodingExemplarAnswers
This is just answers from this test:https://gist.github.com/brandonsavage/65f413d6b508e3849c8fd07f3f407ac6

Question 1

You've been tasked with identifying a string that contains the word "superman" (case insensitive). You've written the following code:

<?php

if(!strpos(strtolower($str), 'superman')) {
    throw new Exception;
}
QA has come to you and said that this works great for strings like "I love superman", but an exception is generated for strings like "Superman is awesome!", which should not happen. Explain why this occurs, and show how you would solve this issue (you must use strpos() in your answer).

Answer 1:
you need check strpos answer with === because if 'superman' will located in a first position strpos will return 0 and it will be recognized as FALSE, if strpos can not find string - it will return FALSE, so, answer will be or False or something number starting from 0
<?php
if(strpos(strtolower($str), 'superman')===false) {
    throw new Exception;
}

