---
layout: post
title:  "Quicksort algorithm with Go"
comments: true
date:   2022-01-08
categories: data-structure
tags: data-structure go
image: "assets/img/partition_quick_sort.jpg"
author: "Raj Arora"
---

# Quicksort algorithm with Go

Quicksort algorithm is a "divide and conquer" algorithm. It takes the "pivot" element from the array and partitioning the other element into sub-arrays.

We can select the pivot with many ways but here I am going to select the last element with my example.


In case you want to understand what "divide and conquer" mean here:

![Divide and conquer screenshot](/assets/img/divide_conquer.jpg)

As you can see in screenshot above, it is partitioning the arrays we will be using the same approach here with go to create this algorithm.

Let's assume we have the following arrays:

{% highlight go %}
[38, -2, -1, 20, 50, 7, 8, 10]
{% endhighlight %}


Here is our approach how we are going to create our pseudo code with the following way:

![examplanation how it works](/assets/img/partition_quick_sort.jpg)

<br/>
<b>Pseudo code for our recursive algorithm:</b>

{% highlight go %}
quickSort(arr [], low, high) {
	if low < high {
		pi = partition(arr, low, high)

		quickSort(arr, low, pi-1) // Before partition
		quickSort(arr, pi+1, high) // After partition
	}
}
{% endhighlight %}

<br/>

Let's create a quick program using golang to show how we're implementing this Pseudo code.

Firstly let's create a simple logic with arrays:

{% highlight go %}
package main

import "fmt"

func main() {
	var (
		arr  []int
		low  int
		high int
	)

	arr = []int{38, -2, -1, 20, 50, 7, 8, 10}
	low = 0
	high = len(arr) - 1

	fmt.Println(arr)
	fmt.Println(low)
	fmt.Println(high)
}

// Output
// [38 -2 -1 20 50 7 8 10]
// 0
// 7
{% endhighlight %}

<br/>
As you can see, we just created a simple logic to make sure we are good at printing, now let's implement quick sort function with our main program:

{% highlight go %}
package main

func main() {
	var (
		arr  []int
		low  int
		high int
	)

	arr = []int{38, -2, -1, 20, 50, 7, 8, 10}
	low = 0
	high = len(arr) - 1

	quicksort(arr, low, high)
    
    fmt.Println(arr)
}
{% endhighlight %}

<br/>
Let's have a quick look at `quicksort` function logic

<br/>
{% highlight go %}
func quicksort(arr []int, low int, high int) {
	if low < high {
		// Partitioning..
		pi := partition(arr, low, high)

		// Before partitioning..
		quicksort(arr, low, pi-1)

		// After partitioning..
		quicksort(arr, pi+1, high)
	}
}
{% endhighlight %}

<br/>
Let's create a logic for our partitioning function

{% highlight go %}
// Here, it's our return function
func partition(arr []int, low int, high int) int {

	// Pivot
	pivot := arr[high]

	// Index
	index := low - 1

	for i := low; i <= high-1; i++ {
		if arr[i] < pivot {
			index++

			// Swapping
			arr[i], arr[index] = arr[index], arr[i]
		}
	}

	// Swapping
	arr[index+1], arr[high] = arr[high], arr[index+1]

	return index + 1
}
{% endhighlight %}
<br/>

Notice here two things which I made a mistake when I was implementing the logic:

- Inside `partition` function, our loop starts with `low` since our quicksort function is recursive. So we don't wanna mess up with arrays index here.
- Swapping, since go returns multiple return value so swapping is much easier with go. We don't need to define a separate function or `temp` declaration.

<br/>
Hopefully, we should get the following output:
{% highlight go %}
[-2 -1 7 8 10 20 38 50]
{% endhighlight %}


<br/>
In case, you want to see the complete program so here it is:
{% highlight go %}
package main

import "fmt"

func main() {
	var (
		arr  []int
		low  int
		high int
	)

	arr = []int{38, -2, -1, 20, 50, 7, 8, 10}
	low = 0
	high = len(arr) - 1

	quicksort(arr, low, high)

	fmt.Println(arr)
}

func quicksort(arr []int, low int, high int) {

	if low < high {
		// Partitioning..
		pi := partition(arr, low, high)

		// Before partitioning..
		quicksort(arr, low, pi-1)

		// After partitioning..
		quicksort(arr, pi+1, high)
	}
}

// Here, it's our return function
func partition(arr []int, low int, high int) int {

	// Pivot
	pivot := arr[high]

	// Index
	index := low - 1

	for i := low; i <= high-1; i++ {
		if arr[i] < pivot {
			index++

			// Swapping
			arr[i], arr[index] = arr[index], arr[i]
		}
	}

	// Swapping
	arr[index+1], arr[high] = arr[high], arr[index+1]

	return index + 1
}
{% endhighlight %}


# Time complexity

- Worst Time Complexity : `O(n^2)`
- Worst case can happen when array is already sorted
- Best time complexity : `O(nlogn)`
- Average Time Complexity : `O(nlogn)`

<br/>
Your feedback is appreciated, please feel free to reach out to me on @rajendraarora16 for any suggestions. 
Would be happy to say 👋
