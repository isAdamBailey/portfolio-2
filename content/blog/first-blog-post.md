---
author: adam
category: Coding
created: 2020-04-15T06:39:13-07:00
title: Consecutively Running a Single PHPUnit test
tags: testing
excerpt: How to run a PHPUnit test multiple times, and log results.
image: "./../images/marco-marques-dJ_Zl5LpPto-unsplash.jpg"
image_caption: Generic image of a jungle, before tests were applied.

---
# Run A Test Consecutively

Have you ever had tests fail randomly due to fake or random data? Sometimes it passes 5 times then fails once. Don't you wish you could just set one to run 100 times and walk away, checking the results later? This article outlines how to run a single test (or suite) in PHPUnit multiple times and log the results to its own file.

lets say you have this line that runs a single test:

    ./vendor/bin/phpunit tests/Unit/BlogTest.php

You run it by pressing the "up" key to find the command in your terminal and press enter. It passes! On a hunch, you run it again, and again. It passes!

But when your teammate runs it it fails. Or it fails in your CI/CD pipeline. WHYYY????

Let's just run it a hundred times to make sure it wont fail.

Copy the code below and replace the test with your own test (I am running iTerm on macOSX):

    for run in {1..100}; do ./vendor/bin/phpunit tests/Unit/BlogTest.php &>> storage/logs/test.log; done

This runs the test you supply, as many times as you tell it in the for loop. Then it logs each result to a log in `storage/logs`

Enjoy!