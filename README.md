Takeaway Challenge
==================

This is a program written by Sara Tateno in response to Makers Academy's Weekend Challenge #2.

It is designed to meet the following user stories:-

```
As a customer
So that I can check if I want to order something
I would like to see a list of dishes with prices

As a customer
So that I can order the meal I want
I would like to be able to select some number of several available dishes

As a customer
So that I can verify that my order is correct
I would like to check that the total I have been given matches the sum of the various dishes in my order

As a customer
So that I am reassured that my order will be delivered on time
I would like to receive a text such as "Thank you! Your order was placed and will be delivered before 18:52" after I have ordered
```

To install the program:-
  1. Fork and clone the repo, e.g. `git clone git@github.com:saratateno/takeaway-challenge.git`
  2. Run `gem install bundler` in your directory
  3. Run `bundle` to install the project gems
  4. Create a `.env` file in the project root directory
  5. Store your Twilio credentials in the  `.env` file in the following format:-
  ```
  TWILIO_NUMBER='+441234567890'
  TWILIO_MOBILE='+440987654321'
  TWILIO_ACCOUNT_SID='ACxxxxxxxxxxxxxxxxxxxxxxxxxx'
  TWILIO_AUTH_TOKEN='cd0xxxxxxxxxxxxxxxxxxxxxxxxx'
  ```

To use the program:-
  1. Run `irb` or `pry` from the command line
  2. `load './lib/takeaway.rb'`
  3. `takeaway = Takeaway.new`

You can now use the following commands:-
* `takeaway.view_menu` to see the available dishes
* `takeaway.add_to_order(dish_name)` entering a string of the dish name to add to your order
* `takeaway.remove_from_order(dish_name)` entering a string of the dish name to remove it from your order
* `takeaway.view_order` to see a summary of your order
* `takeaway.total_price` to see the total cost of your order
* `takeaway.checkout(total, phone_number)` to purchase your order and to receive a confirmation text to your phone

You are required to 'pay' the correct amount for your order to be processed.

This program comes with a short menu of only three items. Dishes can be added / removed to the menu (by the takeaway owner) by creating new dish objects `menu.add(Dish.new(dish_name, price))`.

Program example:-
```sh
[5] pry(main)> t = Takeaway.new
=> #<Takeaway:0x007fe7c9e0c640
 @menu=
  #<Menu:0x007fe7c9e0c618
   @dishes=
    [#<Dish:0x007fe7c9e0c5a0 @name="Satay", @price=4.5>,
     #<Dish:0x007fe7c9e0c550 @name="Spring rolls", @price=3.0>,
     #<Dish:0x007fe7c9e0c500 @name="Tom yum soup", @price=4.9>]>,
 @order=#<Order:0x007fe7c9e0c4b0 @basket={}>>
[6] pry(main)> t.add_to_order('Satay')
=> 1
[7] pry(main)> t.view_order
1x Satay = 4.5
=> {#<Dish:0x007fe7c9e0c5a0 @name="Satay", @price=4.5>=>1}
[8] pry(main)> t.add_to_order('Spring rolls', 3)
=> 3
[9] pry(main)> t.view_order
1x Satay = 4.5
3x Spring rolls = 9.0
=> {#<Dish:0x007fe7c9e0c5a0 @name="Satay", @price=4.5>=>1,
 #<Dish:0x007fe7c9e0c550 @name="Spring rolls", @price=3.0>=>3}
[10] pry(main)> t.add_to_order('Tom yum soup', 2)
=> 2
[11] pry(main)> t.remove_from_order('Satay')
=> 1
[12] pry(main)> t.view_order
3x Spring rolls = 9.0
2x Tom yum soup = 9.8
=> {#<Dish:0x007fe7c9e0c550 @name="Spring rolls", @price=3.0>=>3,
 #<Dish:0x007fe7c9e0c500 @name="Tom yum soup", @price=4.9>=>2}
[13] pry(main)> t.total_price
=> 18.8
[14] pry(main)> t.checkout(18.8)
=> "Thank you! Your order was placed and will be delivered by 21:38"
```



Takeaway Challenge
==================

Instructions
-------

* Challenge time: rest of the day and weekend, until Monday 9am
* Feel free to use google, your notes, books, etc. but work on your own
* If you refer to the solution of another coach or student, please put a link to that in your README
* If you have a partial solution, **still check in a partial solution**
* You must submit a pull request to this repo with your code by 9am Monday morning

Task
-----

* Fill out your learning plan self review for the week: https://github.com/makersacademy/learning_plan_november2015 (if you haven't already)
* Fork this repo
* Run the command 'bundle' in the project directory to ensure you have all the gems
* Write a Takeaway program with the following user stories:

```
As a customer
So that I can check if I want to order something
I would like to see a list of dishes with prices

As a customer
So that I can order the meal I want
I would like to be able to select some number of several available dishes

As a customer
So that I can verify that my order is correct
I would like to check that the total I have been given matches the sum of the various dishes in my order

As a customer
So that I am reassured that my order will be delivered on time
I would like to receive a text such as "Thank you! Your order was placed and will be delivered before 18:52" after I have ordered
```

* Hints on functionality to implement:
  * Ensure you have a list of dishes with prices
  * Place the order by giving the list of dishes, their quantities and a number that should be the exact total. If the sum is not correct the method should raise an error, otherwise the customer is sent a text saying that the order was placed successfully and that it will be delivered 1 hour from now, e.g. "Thank you! Your order was placed and will be delivered before 18:52".
  * The text sending functionality should be implemented using Twilio API. You'll need to register for it. It’s free.
  * Use the twilio-ruby gem to access the API
  * Use the Gemfile to manage your gems
  * Make sure that your Takeaway is thoroughly tested and that you use mocks and/or stubs, as necessary to not to send texts when your tests are run
  * However, if your Takeaway is loaded into IRB and the order is placed, the text should actually be sent

* Advanced! (have a go if you're feeling adventurous):
  * Implement the ability to place orders via text message.

* A free account on Twilio will only allow you to send texts to "verified" numbers. Use your mobile phone number, don't worry about the customer's mobile phone.
* Finally submit a pull request before Monday at 9am with your solution or partial solution.  However much or little amount of code you wrote please please please submit a pull request before Monday at 9am


In code review we'll be hoping to see:

* All tests passing
* High [Test coverage](https://github.com/makersacademy/course/blob/master/pills/test_coverage.md) (>95% is good)
* The code is elegant: every class has a clear responsibility, methods are short etc.

Reviewers will potentially be using this [code review rubric](docs/review.md).  Referring to this rubric in advance will make the challenge somewhat easier.  You should be the judge of how much challenge you want this weekend.

Notes on Test Coverage
------------------

You can see your [test coverage](https://github.com/makersacademy/course/blob/master/pills/test_coverage.md) when you submit a pull request, and you can also get a summary locally by running:

```
$ coveralls report
```

This repo works with [Coveralls](https://coveralls.io/) to calculate test coverage statistics on each pull request.

Build Badge Example
------------------

[![Build Status](https://travis-ci.org/makersacademy/takeaway-challenge.svg?branch=master)](https://travis-ci.org/makersacademy/takeaway-challenge)
[![Coverage Status](https://coveralls.io/repos/makersacademy/takeaway-challenge/badge.png)](https://coveralls.io/r/makersacademy/takeaway-challenge)
