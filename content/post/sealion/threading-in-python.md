+++
title = "Threading in Python"
date = 2019-09-17T21:06:58-04:00
draft = true
tags = []
categories = ["sealion"]
+++


# Threading in Python
For my entire time working with Python I had assumed that threading was a form of multiprocessing, i.e. that creating a new thread with the [`threading`](https://docs.python.org/3/library/threading.html) library would start a separate process from the one created by the main Python program. I think this idea came from my fundamental misunderstanding of how Python works, and since the code I used with threading worked and I had (have?) only a vague sense of how CPUs divvy up processes to begin with I never had to face this misunderstanding. But this misunderstanding began to create problems as I was trying to figure out a way to run a GUI for [SeaLion's](https://github.com/kaganjd/sealion) server while the server also ran websockets with [asyncio](https://docs.python.org/3/library/asyncio.html). [Jen](https://github.com/kaganjd) suggested we spend a week just getting really deep into how Python threading works.

What I learned was that threading is one of several ways of doing [concurrency](https://pymotw.com/3/concurrency.html) in Python, i.e. doing multiple things at once. `Subproccesing` `multiprocessing`, `asyncio`, and `signal` are some of the other methods. In the case of `threading`, however, [CPython](https://en.wikipedia.org/wiki/CPython), the standard Python interpreter, has a [global interpreter lock](https://en.wikipedia.org/wiki/Global_interpreter_lock) preventing multiple threads from executing at the same time, so work being done on multiple threads can't actually happen at the same time, but rather only has the appearance of happening at the same time. This is really where my misunderstanding most got in the way - with true `multiprocessing` multiple actions can happen simultaneously, with threading in Python the single process can only do one thing at once and has to switch between threads.



References:
https://realpython.com/intro-to-python-threading/

https://pymotw.com/3/concurrency.html

https://pymotw.com/3/threading/index.html

https://docs.python.org/3/library/threading.html

https://docs.python.org/3/library/asyncio-dev.html

https://realpython.com/async-io-python/
