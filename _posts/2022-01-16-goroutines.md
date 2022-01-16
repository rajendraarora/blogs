---
layout: post
title:  "Goroutines"
comments: true
date:   2022-01-16
categories: Goroutines
description: "A portal to learn about Goroutines to understand some basics examples of go keywords."
tags: goroutines go
image: "assets/img/go.png"
author: 
    name: Raj Arora
    twitter: rajendraarora16
    image: "assets/img/rajendra_circle.gif"
twitter:
    username: rajendraarora16
    card: summary_large_image
social:
    name: Raj Arora
    links:
        - https://twitter.com/rajendraarora16
        - https://www.facebook.com/rajendra.arora.contact/
        - https://www.linkedin.com/in/arorar16/
        - https://github.com/rajendraarora16
---

# Goroutines

A Goroutine is a lightweight thread managed by the Go runtime. A Goroutine is a function or method which executes independently and simultaneously in a connection with any other Goroutine present in our program.
<br/>

In other word, Goroutines are functions/methods that run concurrently with other functions/methods.

# How to create a Goroutines?

We can create our own Goroutine by simply using `go` keyword as prefex to the function or method.

{% highlight go %}
go function(x, y, z)
{% endhighlight %}

`function(x, y, z)` will start new goroutine runnning.

<br/>

I will go over basics to a complex example to understand more on examples. So let's start with basics..

<br/>

Let's assume we have this 

{% highlight go %}
package main

import "fmt"

func main() {
	displayGreetMsg("Welcome") 
	displayGreetMsg("Raj Arora")
}

func displayGreetMsg(str string) {
	for i := 0; i < 5; i++ {
		fmt.Println(str)
	}
}
{% endhighlight %}


As you can see, it will return the following output:

{% highlight go %}
// Welcome
// Welcome
// Welcome
// Welcome
// Welcome
// Raj Arora
// Raj Arora
// Raj Arora
// Raj Arora
// Raj Arora
{% endhighlight %}

<br/>
Now, if you try to add `go keyword` in the following function:

{% highlight go %}
package main

import "fmt"

func main() {
	go displayGreetMsg("Welcome") /* Goroutine function */
	displayGreetMsg("Raj Arora")  /* normal function */
}

func displayGreetMsg(str string) {
	for i := 0; i < 5; i++ {
		fmt.Println(str)
	}
}
{% endhighlight %}

You will get the following outputs:

{% highlight go %}
// Raj Arora
// Raj Arora
// Raj Arora
// Raj Arora
// Raj Arora
{% endhighlight %}

As you can notice that the above program returns the continous `Raj Arora` output but it doesn't return `Welcome` message because we passed `go` keyword here with `go displayGreetMsg("Welcome")`. The reason because:
- When a new Goroutine executed, the Goroutine call returns immediately. The control does not wait for the Goroutine to complete their execution just like normal function. So it moves forward to the next line after the Goroutine call and ignore the values.

<br/>

You will be able to understand now why our Goroutine did not run. After the call `go displayGreetMsg("Welcome")`, the control returned immediately to the next line of code without waiting for `displayGreetMsg("Welcome")` to finish and it printed the `displayGreetMsg("Raj Arora")`. And then later the main Goroutine terminated since there is no other code to execute. That's why we see `Raj Arora` as an output five times.

<br/>

Let's run this program after some modification so you will get to know what's happening behind:

{% highlight go %}
package main

import (
	"fmt"
	"time"
)

func main() {
	go displayGreetMsg("Welcome") /* Goroutine function */
	displayGreetMsg("Raj Arora")  /* normal function */
}

func displayGreetMsg(str string) {
	for i := 0; i < 5; i++ {
		time.Sleep(1 * time.Second) /* timer */
		fmt.Println(str)
	}
}
{% endhighlight %}

In above program, you may notice that I added a timer before printing. You will now get the following output:

{% highlight go %}
// Welcome
// Raj Arora
// Raj Arora
// Welcome
// Welcome
// Raj Arora
// Welcome
// Raj Arora
// Raj Arora
{% endhighlight %}

The reason because:
- Now the `go displayGreetMsg("Welcome")` has enough time to execute before the main Goroutine terminates. It prints `Welcome` and then wait for 1 second and print `Raj Arora` and then wait for 1 second and so on.

# One more example in brief

This time I am using this example which I learnt from Udemy, here we have the following program:

{% highlight go %}
package main

import (
	"fmt"
	"net/http"
)

func main() {

	var links []string

	links = []string{
		"https://google.com",
		"https://stackoverflow.com/",
		"https://yandex.com",
		"https://github.com",
	}

	for _, link := range links {
		checkLink(link)
	}
}

func checkLink(link string) {

	_, err := http.Get(link)

	if err != nil {
		fmt.Println(link, "might be down")
	}

	fmt.Println(link, "is up!")
}
{% endhighlight %}

It will return the following output:

{% highlight go %}
// https://google.com is up!
// https://stackoverflow.com/ is up!
// https://yandex.com is up!
// https://github.com is up!
{% endhighlight %}

Now I am here using `go` keyword to run our Goroutine program

{% highlight go %}
package main

import (
	"fmt"
	"net/http"
	"time"
)

func main() {

	var links []string

	links = []string{
		"https://google.com",
		"https://stackoverflow.com/",
		"https://yandex.com",
		"https://github.com",
	}

	for _, link := range links {
		/* Groutine "go" keyword
		/* which creates a new thread */
		go checkLink(link)
		/* Timer */
		time.Sleep(1 * time.Second)
	}
}

func checkLink(link string) {

	_, err := http.Get(link)

	if err != nil {
		fmt.Println(link, "might be down")
	}

	fmt.Println(link, "is up!")
}

{% endhighlight %}

Now that will put some delays to get your output:

{% highlight go %}
// https://google.com is up!
// https://stackoverflow.com/ is up!
// https://yandex.com is up!
// https://github.com is up!
{% endhighlight %}

Hope, my contribution will help you to understand this topic. Please feel free to reach out to me on twitter [@rajendraarora16](https://twitter.com/rajendraarora16) for any queries. 😉
