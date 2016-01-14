---
layout: page
title: "Writing your own functions"
---

# What are functions?

Below is an incredibly great excerpt from [Massimo Banzi's Getting Started With Arduino](http://phylab.fudan.edu.cn/lib/exe/fetch.php?media=yuandi:arduino:getting_started_with_arduino_v2.pdf)


> "*If you’re at dinner and you ask somebody, “Please pass me the Parmesan cheese," this kicks off a series of actions that are summarised by the small phrase that you just said. As we’re humans, it all comes naturally, but all the individual tiny actions required to do this must be spelled out to the Arduino, because it’s not as powerful as our brain. So to group together a number of instructions, you stick a { before your code and an } after.*
>
> *You can see that there are two blocks of code that are defined in this way here. Before each one of them there is a strange command:*
>
> ````
> void setup()
> ````
> 
> *This line gives a name to a block of code. If you were to write a list of instructions that teach Arduino how to pass the Parmesan, you would write <code>void passTheParmesan()</code> at the beginning of a block, and this block would become an instruction that you can call from anywhere in the Arduino code. These blocks are called functions. If after this, you write <code>passTheParmesan()</code> anywhere in your code, Arduino will execute those instructions and continue where it left off."*



# Why use functions?

* Stay organized: Break out section of the program into neat little units

* Reduce Repetition: If you have to do the same operations more than once you’ll probably want a function. It means you only have to write and test one piece of code instead of checking it in lots of places

* Neater: You’ll use less code in your sketch

* Readability: You can name your functions sensibly which makes your whole sketch much easier to scan, read and understand

* Reusable: Once you’ve written a function for one piece of code, you can often quickly drop it into another sketch. 

# Writing a function

A simple function looks like this:

````
void passTheParmesan()
{
	// Add some action here
}
````

And is called like this:

````
void loop()
{
	// stuff goes here
	passTheParmesan();
	sprinkleParmesan();
	eatFood();
	// other stuff goes here
}
````

{% include note.html type="hint" title="Placing Functions" text="Functions can be placed anywhere in a sketch but it is common practice to add them after the <code>setup()</code> and <code>loop()</code> functions." %}


Let’s look at a more complicated example that returns a value. Can we write a function to give us the square of a number. 

````
int squared( int value )
{
	// multiply the number
	int sq = value * value;
	return sq;
}
````


**What’s happening here?**

This looks a little different, right? 

The first part of the function has changed from void to int. This tells us what the function will return or give us back. Up until now we have used functions that return nothing or void. These are reasonably common, but sometimes you want it to give you information back. In that case, you need to specify what the data type of that information is. Note that you can only return one variable from a function. 

The next part is still what the function is called, but we now have some stuff in the brackets. This tells us what **parameters** we can pass to the function. This is telling us that we can pass one integer variable to the function. 

OK, so we know we need to pass in one integer and it’s going to give us an integer back. Cool!

Now inside the function are a series of operation [terminated with a semicolon]. First it multiples the passed integer, the value parameter. A new local variable (only exists within the function) is created to hold the squared value.

Finally, we use the return function to say that the function is complete and we want to send a value back to where it was called. 

So what does that look like? 

````
void loop()
{
	// stuff goes here
	int sqValue;
	sqValue= squared(4); // this gives us 16
	sqValue = squared(5); // this gives us 25
	// do something with the number
}
````



Now we call the function a little differently. We know it gives us back an integer, so we need to create a variable to hold the output. We pass 4 into the function and the sqValue variable will end up containing the number 16.  We pass 5 into the function and the sqValue variable will end up containing the number 25, etc.

# Built in Functions

Arduino and Particle have a ton of built in functions to make it easier for you to write sketches and perform common actions. Take a look at them here: [http://arduino.cc/en/Reference/HomePage](http://arduino.cc/en/Reference/HomePage)

Some of the most useful are:

* <code>delay</code> - [https://docs.particle.io/reference/firmware/photon/#delay-](https://docs.particle.io/reference/firmware/photon/#delay-) 

* <code>min</code> - [https://docs.particle.io/reference/firmware/photon/#min-](https://docs.particle.io/reference/firmware/photon/#min-) 

* <code>max</code> - [https://docs.particle.io/reference/firmware/photon/#max-](https://docs.particle.io/reference/firmware/photon/#max-) 

* <code>abs</code> - [https://docs.particle.io/reference/firmware/photon/#abs-](https://docs.particle.io/reference/firmware/photon/#abs-)   

* <code>map</code> - [https://docs.particle.io/reference/firmware/photon/#map-](https://docs.particle.io/reference/firmware/photon/#map-) 

* <code>random</code> - [https://docs.particle.io/reference/firmware/photon/#random-numbers](https://docs.particle.io/reference/firmware/photon/#random-numbers) 

### Read more:

- [https://docs.particle.io/reference/firmware/photon/#other-functions](https://docs.particle.io/reference/firmware/photon/#other-functions)

