# How to do unit testing.

Laravel Rocket system already includes unit test codes in `tests` directory.

## How to run unit tests.

You can run unit test code after running `composer install` or `composer update`

```
% vendor/bin/phpunit
```

## Policy for unit testing

Sometimes people say that "I have no time to write unit test code". But it is wrong. They have no time to write tests because they didn't write tests before. Unit testing must reduce your development time especially on the end of the project ( Avoid "Another bug happens just after fixing one bug" & "Fixed bug appear again after fixing another bug").
