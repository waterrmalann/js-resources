# Demystifying Synchronous and Asynchronous Programming in JavaScript: A Beginner's Guide

**JavaScript** is a **synchronous**, **single-threaded** programming language.

Pretty sure you’ve heard that before, but do you really understand what is meant by that statement?

What does synchronous mean? What does single-threaded mean? Are they related at all?

Let’s break it down and take a closer look.

# “Synchronous”

What is synchronous exactly? **Synchronous** means that JavaScript code is executed **line-by-line**, **one after another**, in the order it appears in your code. Similar to reading a book, from the first page to the last page without skipping any pages.

Imagine you have two tasks in your code, such as downloading an image and displaying a message. In a synchronous execution, JavaScript would first download the image, and only after it’s done, it would display the message. So, the order of execution is strictly sequential.

## What is “Asynchronous” then?

You would already have an idea by now, synchronous is sequential, asynchronous is not. That’s basically it! **Asynchronous** refers to a way of handling tasks where a task doesn’t necessarily block or wait for another task to complete before moving on. So, instead of going line-by-line, we may skip a few lines, then come back to the previous line, go back, go forth, and and eventually read all the lines in a very unpredictable way. It allows the program to continue executing other tasks while waiting for a particular task to finish in the background.

For a better example, let’s imagine you’re cooking in your kitchen. You start boiling water for pasta and then chop vegetables while the water is boiling. You don’t stand there staring at the water until it boils; you can do other tasks in the meantime. This is similar to how asynchronous code works in JavaScript, where it can initiate a task, like a network request, and then continue doing other things while waiting for the response.

A common misconception that people often have is that Asynchronous means parallel or at the same time but this is not entirely accurate. Let's clarify this:

**Asynchronous does not necessarily mean parallel or simultaneous execution.**

While asynchronous operations allow you to initiate multiple tasks and continue working on other things while waiting for some of them to finish, it doesn't guarantee that these tasks will run in parallel. In fact, in a single-threaded environment like JavaScript, true parallel execution of tasks is not possible.

Let’s reimagine the same scenario where you’re cooking in your kitchen. We mentioned that you can chop vegetables (task 2) while the water is boiling (task 1). But you can’t start another task like answering the phone (task 3) while chopping vegetables because both your hands are occupied, and you need to focus on the chopping to avoid cutting yourself.

In this analogy:

- **Task 1 (boiling water)** is similar to an asynchronous operation in JavaScript. You initiate it and then allow it to happen in the background while you move on to other tasks.
- **Task 2 (chopping vegetables)** is like the main thread in JavaScript. You're actively working on it, but it's not preventing other tasks from starting if they are asynchronous.
- **Task 3 (answering the phone)** represents a task that can't be done in parallel with chopping vegetables because both require your full attention. This is akin to how certain operations in JavaScript may need to wait for others to finish before they can start because they depend on the same resources or data.

So, asynchronous does not mean these tasks can happen simultaneously, but rather in a way that maximizes efficiency by not blocking tasks that can be done independently. It's about making the most of your time and resources.

In JavaScript, you use asynchronous operations when you have tasks that can be initiated and then proceed in the background while you continue with other work. This approach keeps your code responsive and prevents it from getting stuck waiting for one task to finish before moving on to the next.

However, just like in the kitchen analogy, there are situations where tasks may need to wait for each other, especially if they depend on shared resources or data. In such cases, you may need to carefully coordinate these tasks to ensure they run in the correct order, which is where JavaScript's asynchronous mechanisms like callbacks, promises, and async/await come into play. These tools help you manage the flow of your code and handle dependencies between asynchronous tasks effectively.

Still with me? Let’s go through one more example, in the context of programming.

Asynchronous code is best suited for and used for tasks that are I/O bound, (or from the kitchen example, when you are waiting for something you have no control over) such as:

- **Sending a network request:** Say you’re requesting for an image from an image hosting site. Depending on your internet speed, and various other factors, your program has to sit there waiting for who knows how long for image to come back, before executing other tasks in the synchronous nature. This is a task which you just have to wait for, that you have no control over.
- **Getting input from the user:** You’re waiting on the user to give you some input. Your program is effectively blocked because it needs further input to perform any more actions, even if those actions does not depend on the input at all. Yet another task you have no control over.
- **Reading a file or a database:** You request the hard drive or a database to give you some data and then you have to wait for the I/O controller or the database management system to get back to you with the data that you requested, where you have to sit idle.

It is not suited for tasks that are CPU-bound, (or from the kitchen example, when both your hands are occupied) such as:

- **Heavy number crunching:** Let’s say you’re calculating the factorials of millions of numbers. That would be a task which a single-thread would fully be occupied on. It cannot do anything else while that task is being executed. Asynchronous code may not be of any help at all for tasks like this other than executing them at the right time. Without the help of multi-threading, we cannot do anything else here.

Here's a key distinction:

- **Asynchronous** means tasks are started and then continue in the background while other tasks are being executed. It's more like managing a to-do list where you start tasks, mark them as "in progress," and continue with other tasks while waiting for them to complete.
- **Parallel** execution involves running multiple tasks truly simultaneously on multiple threads or processors. This can happen in multi-threaded environments, but it's not the same as asynchronous execution.

In JavaScript, for instance, asynchronous code helps maintain responsiveness in web applications by allowing tasks like network requests or file I/O to operate without blocking the main thread. However, these asynchronous tasks still occur one after the other in the single thread, but they are interleaved in such a way that it appears they are happening simultaneously.

So, while asynchronous code improves the user experience by preventing the UI from freezing during time-consuming operations, it doesn't guarantee that tasks are running in parallel, and true parallelism may require a multi-threaded environment or other parallel programming techniques.

# Let’s talk about threads now.

Bored? Oh you’re in for a treat. We’ve just went over “synchronous” and it’s counterpart. There’s “single-threaded” left. I promise I’ll keep this one short!

**Single-threaded** refers to the fact that JavaScript operates using a single execution thread. Think of a thread as a worker that processes your code. In a single-threaded environment, there's only one worker handling all your code instructions.

Picture a busy restaurant kitchen with just one chef. The chef can only cook one dish at a time, so they have to finish making one dish before moving on to the next. Similarly, in a single-threaded JavaScript environment, tasks are processed one at a time, and the next task has to wait until the current one is completed.

**Multi-threaded** means that a program or application can execute multiple tasks or threads concurrently. Each thread acts as an independent worker, allowing different parts of the program to run simultaneously.

<aside>

> [!NOTE]
> 💡 **Concurrency is** like juggling multiple tasks at once. Imagine you're a chef in a busy restaurant kitchen. You're not waiting for one dish to finish cooking before you start another; instead, you're managing multiple dishes simultaneously.

</aside>

Picture the same busy restaurant kitchen, but instead of just one chef who can only cook one dish at a time. We have many chefs who can each cook a dish independently of each other. Similarly, in a multi-threaded environment, different parts of your code can run in parallel, making better use of computer resources and potentially improving performance.

<aside>

> [!NOTE]
> 💡 **Parallelism is** like having multiple people to handle multiple tasks. It is different from concurrency, just like how a team of builders can finish a house much quicker than a single worker.

</aside>

Now, let's bring it all together:

- **Synchronous and Single-threaded**: In a synchronous and single-threaded environment like JavaScript, tasks are executed one after another, in the order they appear in the code. Each task must wait for the previous one to complete before it can start. While this ensures predictable execution order, it can lead to blocking, especially when handling time-consuming tasks.
- **Asynchronous and Single-threaded**: When we write asynchronous code in JavaScript. It can initiate tasks asynchronously, allowing them to run independently while the main thread continues with other work. This approach keeps the program responsive and prevents blocking for I/O bound tasks where our hands are free to do other things while waiting for something else. **Note:** It does not prevent blocking for CPU-bound tasks where our hands are both occupied.
- **Synchronous and Multi-threaded**: In contrast, some languages and environments are both synchronous and multi-threaded. In this setup, tasks are executed sequentially within a single thread, just like in a synchronous single-threaded environment. However, there's an additional capability where multiple threads can be created to run tasks concurrently. This allows for better utilization of multi-core processors and can enhance performance when handling tasks that can be parallelized.
- **Asynchronous and Multi-threaded**: Some programming languages or environments can be both asynchronous and multi-threaded. In this scenario, tasks can be initiated asynchronously, and multiple threads can execute different tasks concurrently. This can be powerful for handling a high volume of tasks efficiently.

In summary, synchronous programming in a single-threaded environment leads to sequential execution, while asynchronous programming in a single-threaded environment allows tasks to run independently. On the other hand, asynchronous and multi-threaded environments enable multiple tasks to run simultaneously, which can significantly enhance performance, especially when dealing with tasks like handling numerous user requests or processing large datasets.

---

~ [***Alan Varghese***](https://alanvarghese.me)
