---
description: The template content is parsed as mustache and may be formatted as HTML.
---

# Content

## Table

This section explains the options and limitations of the table.

![](../.gitbook/assets/image%20%2834%29.png)

After adding a table, the table properties can be entered.

**Rows** – Number of rows of the table **Columns** – Number of columns of the table **Width** – Width of the table in percentages **Height** – Height of the rows **Edge thickness** – 0 = no edge, 1 = an edge everywhere

![](../.gitbook/assets/image%20%282%29.png)

It is possible to adjust the properties of a cell. To do so, you need to click on a cell with the right mouse button. You then go to cell and cell properties.

**Width** – Width of the column in which the cell is located **Height** – Height of the row in which the cell is located **Alignment** – Here, you can determine the alignment of the text in the cell. By default, the text is aligned top left.

## Field content 

FillTheDoc recognizes any text typed in the content as regular text and will read all spaces and paragraphs. When you want to add a static piece of content, based on user input, you put the location of this content in the text between mustaches.  `{{}}`

When you ask the user for his name in the field 'questions' and step 'name', and you want to add this to the text 'Hello \(insert name\), this document is for you!', you get the following text:

`Hello {{questions.name}}, this document is for you!`

## Dynamic text with the help of a statement

In the text of a template, words/pieces of text can be made dynamic with the help of a statement. This is possible by using fields and their outcomes.

_Example:_ Every dynamic piece of text is opened using the following code: `{{#condition}}`

Every dynamic piece of text is closed using the following code: `{{/}}`

This translates into the following statement: `{{#condition}}text{{/}}`

In the above statement, text is only visible under a certain condition.



Field1 is a Selection list with choices Yes and No in the case above.

`{{#field1 == "Yes"}}This sentence must be made dynamic/variable{{/}}`

This means that when the user puts field1 to Yes, the sentence appears, and with all other possible options, in this case just No, the sentence does not become visible.

You can use `!==` to do the opposite:

`{{#field1 !== "Yes"}}This sentence must be made dynamic/variable{{/}}`

Now, the sentence will only NOT appear if Yes is selected with field1 and WILL appear with all other possible options.



It is possible to use other operators \(see concepts\) besides the == symbol from the example. If the outcome of a field is a word, the word should be put in quotation marks \(“\). A number does not need to be put between quotation marks \(“\).

For example: `{{#x == 5}}` and `{{#x == "cow"}}`



For an **option group**, the following code needs to be used:  

`{{#optionsFieldName.indexOf("Option3") > -1}}Text for tickable box 3{{/}}`

When a tickable box isn't ticket by the user, it returns the value -1. When it's checked, it returns the value 0 and when there is a list of things that can be checked, it will assign values increasingly: 1, 2, 3 etc.  
When you want to show a certain text under the condition that one of the tickable boxes in a field is checked, you should there check if its value is not -1

You can also use: `{{#optionsFieldName.includes("Option3")}}Text for tickable box 3{{/}}`

\`\`

You can refer to a **checkbox** by checking it's checked \(true\) or unchecked \(false\) like so: `{{#fieldgroup.field == true}}this is readable when box is checked{{/}}`

\`\`

You can refer to an answer in a **Likert Scale** as follows:  
`{{#fieldgroup.field.0 == yes}}text shows if answer to first question is yes{{/}}`

Here, the text shows up if the answer to the first question is yes.

## If-statement

It is possible to use an if-statement in the text.

Suppose there is a Selection list \(field1\) with two choices: Yes and No.

For an if-statement, the following code is used: 

`{{#field1 == "Yes"}}The Employee does receive vacation days{{/}}{{#field1 !== "Yes"}}The Employee does not receive vacation days{{/}}`

What this means is that if field1 is set to Yes, then the sentence: “The Employee does receive vacation days” will appear, and otherwise, the sentence: “The Employee does not receive vacation days” is displayed.

This can be done with as many choices as desired, not just with a field with two choices, since you can also use `== "No"` instead of `!== "Yes".` 

You can also use:`{{field1=="Yes" ? "The Employee does receive vacation days" : "The Employee does not receive vacation days"}}`

Creating an if-statement is possible with the use of the following fields: Selection list, Option group, Check box, Likert scale and Number with unit.

## Creating a list of articles

It is possible to create a numbered list of articles. If you put a \# before each article number, the software turns these numbers into a numbered list. This means that if an article is dynamic and is not displayed, the numbers of the articles still form a consecutive list.

Example:

This is what the programming looks like, under ‘Edit’.

> Article \#1 Duration
>
> Piece about duration
>
> Article \#2 Period
>
> Piece about period
>
> Article \#3 Insurance
>
> Piece about insurance

This is shown in the document as follows, under ‘View’.

> Article 1 Duration
>
> Piece about duration
>
> Article 2 Period
>
> Piece about period
>
> Article 3 Insurance
>
> Piece about insurance

If Article 2 is not dynamic and not displayed, Article 3 will be given number 2.

> Article 1 Duration
>
> Piece about duration
>
> Article 2 Insurance
>
> Piece about insurance

It is then also possible to scroll to an article, see ‘Scroll to article’ under ‘Steps’.

NOTE! Sometimes the \# symbol stays in the ‘View’ environment in front of the article number, to resolve this, you remove the space and the first letter after the article number and then enter it again.

It is possible to, for example, have references to the article numbers change with the article number.

Example:

Suppose that Article 1 from the previous example contains a reference to Article 3: “See what is described in Article 3.” and Article 2 is not displayed, then the reference to Article 3 can be changed to 2 with the following code: `Article {{$[3]}}` . The sample sentence will then look as follows: “`See what is described in Article {{$[3]}}`.” So if Article 2 is not dropped, the sentence is shown as follows: “See what is described in Article 2”.

## Date

A number of additional functions are possible with regard to the date. It is possible to add or subtract a period from a chosen date in a Date field and to display it in the text. This can be done with the help of the following codes:

**Add** – `{{datefield.addPeriod(1, 'year')}}` Adds a year to the date `{{datefield.addPeriod(duration)}}` Here, ‘duration’ is a Number with unit field with a period as the entered value, for instance: ‘week’, ‘month’ or ‘year’. The function automatically records the period and adds it to the date. The same applies to subtractions. The periods are also recognized in English.

**Subtract** – `{{datefield.substractPeriod(1, 'year')}}` Subtracts a year from the date

Date fields can use the additional function by using [_moment.js_](http://momentjs.com/docs/).  
In this case, the variable date field ‘datefield’ is the field name of a Date field. This name can be changed as desired.

`x.localeDateFormat()` transforms a date to the selected local standard

## Troubleshooting

It may be that when entering an incorrect code or forgetting to close a statement, it is no longer possible to test the document under ‘View’.

When this situation occurs, it is important to systematically find out the problem. Save the template and then remove all text first, and if this does not solve the problem, eliminates steps 1 by 1 and check whether you can use the software again under 'View'. This way, you can figure out where the problem is step by step and resolve it.

### Known problems

If a statement \(see ‘Dynamic text using a statement'\) is closed once too many, then the piece becomes fully blank under 'View'. The same happens if you forget a mustache, for instance: `{{field1}`.

If a statement is not closed, then the text under the opening of the statement disappears. This can be solved by closing or removing the statement.

