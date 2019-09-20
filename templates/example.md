---
description: Lets use everything we've learned
---

# Example

### Name and date

First, we create a step for our name 

![](../.gitbook/assets/image%20%2847%29.png)

Next, we have to drag a 'free text' field from the sidebar to this step

![](../.gitbook/assets/image%20%2811%29.png)

Now we drag a date field to the same step

![](../.gitbook/assets/image%20%2812%29.png)

Add the following text   
`The date today is {{Name.answer}}`

### Options

Now we have to create a step that's going to ask us to pick a value from a list of options

![](../.gitbook/assets/image%20%2821%29.png)

Next, we drag an option group from the sidebar to this step with the options

![](../.gitbook/assets/image%20%2837%29.png)

### Choice

Next, in case someone picks the second option, we want to know why, so we add the following field to the same step

![](../.gitbook/assets/image%20%2863%29.png)

`{{#Example.Options.indexOf("first") > -1}}I don't like that option, {{Name.yourname}}{{/}}{{#Example.Options.indexOf("second") > -1}}That's a good option!{{/}}{{#Example.Options.indexOf("third") > -1}}{{/}}`

### Calculation

We can also a calculation inside the form, and have form calculate something based on the given answers.  
First we create a calculation step with three number fields.  
We call them `Calc.fav` `Calc.house` and `Calc.multiply`

![](../.gitbook/assets/image%20%283%29.png)

Now, we drag an expression to this step and have it multiply the sum of your favorite number with your address by a number of choice, which we call Calc.total

![](../.gitbook/assets/image%20%2826%29.png)

Under article 3, we added the following code

`Your total is ({{Calc.fav}} + {{Calc.house}}) * {{Calc.multiply}} = {{Calc.total}}`

Since we defined the articles, and we added 'scroll to article 3' in all steps, we will be shown this part of the text when someone has to answer the questions. 

### Lets add in a variable article

We're going to create a table of contents with one variable article we want to be able to take out. First we're going to create a step with a choice field. 

![](../.gitbook/assets/image%20%2823%29.png)

We want article 4 to show, unless someone answers 'no', and when it doesn't show, we want the other article numbers to automatically update, so we write the following text:`Table of contents  
Article {{$[1]}} Beginning  
Article {{$[2]}} Middle  
Article {{$[3]}} Example  
{{#article.answer !== "no"}}Article {{$[4]}} Article Example{{/}}  
Article {{$[5]}} Final`  
and we write write article 4 in the same way:

![](../.gitbook/assets/article4.png)

### A final check to see if we understand everything!

![](../.gitbook/assets/image%20%2848%29.png)

![](../.gitbook/assets/image%20%2852%29.png)

If someone answers no, we want to know how bad they understand it. We will use the Likert scale for that.

![](../.gitbook/assets/image%20%286%29.png)

We add the following text:`{{#understand.question == 1}}That's great!{{/}}`

`{{#understand.scale == "neutral" || understand.scale == "decent" || understand.scale == "good"}}You'll get there if you keep practicing!{{/}}`

`{{#understand.scale == "not at all" || understand.scale == "not good enough"}}Try reading the documentation again, follow along, and try again! :){{/}}`

We now have the following text

![](../.gitbook/assets/image%20%2855%29.png)

### Lets see how our template works!

![Date is working, no name yet](../.gitbook/assets/image%20%2820%29.png)

![Lets try the second one](../.gitbook/assets/image%20%2851%29.png)



![Good!](../.gitbook/assets/image%20%2859%29.png)

![](../.gitbook/assets/image%20%2858%29.png)

![Article 4 gets removed and 5 turns to 4](../.gitbook/assets/image%20%2827%29.png)

![Read again!](../.gitbook/assets/image%20%287%29.png)

![We&apos;ll get there!](../.gitbook/assets/image%20%2854%29.png)

![Done!](../.gitbook/assets/image%20%2828%29.png)









