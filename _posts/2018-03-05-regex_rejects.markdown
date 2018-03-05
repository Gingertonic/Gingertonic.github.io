---
layout: post
title:      "Regex Rejects"
date:       2018-03-05 10:43:40 -0500
permalink:  regex_rejects
---

<style>
table {
    border-collapse: collapse;
    width: 100%;
}

td, th {
    border: 1px solid #dddddd;
    text-align: left;
    padding: 8px;
}

tr:nth-child(even) {
    background-color: #dddddd;
}
</style>

<img src="https://i.imgur.com/WjmTL3b.png" alt="RegEx Rejects" style="width: 100%;"/>

### Is that really pronounced... *'rejects'*?

No, not generally. But I pronounce it that way and think it's very apt since it rejects anything that doesn't match what we ask it for.
More commonly it's pronounced 'Reg-Ex' with a hard 'g' for reasons which will become clear if not already so.
<br>*I also say 'Frez-nels', not 'fre-nelle'. (If you're not a lighting tech ignore that). 
<br>I like to see people's faces after saying both these things.*


### What is Regex?
RegEx stands for 'Regular Expressions'. My first instinct was to think *"Can't be that regular, I've never heard of them."*

So let's see what some of these 'regular' expressions look like:

```
/\A[aeiou]/i
```

```
/\bun\S*ing\b/
```

```
\b\w{5}\b/
```

```
/^[A-Z].+\.\z/
```

```
/^\D*(\d\D*){10}$/
```



**Er... that sure doesn't look like anything I'd call 'regular'... **
<br>
#### **Why the name then?** <br>
You know what, I've tried to find out and it's pretty confusing. For now, here's a Wiki quote...
> A regular expression, regex or regexp (sometimes called a rational expression) is, in theoretical computer science and formal language theory, a sequence of characters that define a search pattern. Usually this pattern is then used by string searching algorithms for "find" or "find and replace" operations on strings.

>The concept arose in the 1950s when the American mathematician Stephen Cole Kleene formalized the description of a regular language.

### We ain't in type-what-you-mean-Ruby-land anymore, Dorothy.
Or are we?
You do, actually type what you mean, we just use a shorthand. I think of it like the time I tried to learn the kind of [shorthand] that is used by journalists and court room note-takers.

You might see this : `/\b[(\!)(\?)(\.)]+/` and think it's incomprehensible.


But think it's time for another dictionary. Have a quick study of the following and we'll meet back in a minute, right below.
<br>
<br>

## A (Very) Abridged Regex-English Dictionary

<table>
  <tr>
    <th>#</th>
    <th>Regex</th>
    <th>English</th>
  </tr>
  <tr>
	<td>1</td> <td><code>[rht]</code> </td>  <td>any r,  h or t characters </td> 
  </tr>
  <tr>
    <td>2</td> <td><code>[dlp]</code>  </td>  <td>any characters except d, l, or p </td> 
  </tr>
	  <tr>
    <td>3</td> <td><code>[a-z]</code> </td>  <td>any lower case character within the range of a to z </td> 
  </tr>
	  <tr>
    <td>4</td> <td><code>[F-R]</code></td>  <td>any upper case character within the range of F to R </td> 
  </tr>
	  <tr>
    <td>5</td> <td><code>[R-Tf-z]</code>  </td>  <td>any upper case character within the range of R to T and any lower case character within the range of f to z </td> 
  </tr>
	  <tr>
    <td>6</td> <td><code>^</code></td>  <td>start of line </td> 
  </tr>
	  <tr>
    <td>7</td> <td><code>$</code> </td>  <td>end of line </td> 
  </tr>
	  <tr>
    <td>8</td> <td><code>\A</code> </td>  <td>start of string </td> 
  </tr>
	  <tr>
    <td>9</td> <td><code>\z</code>  </td>  <td>end of string </td> 
  </tr>
	  <tr>
    <td>10</td> <td><code>.</code>  </td>  <td>any single character </td> 
  </tr>
		  <tr>
    <td>11</td> <td><code>\</code> </td>  <td>'escape' - used eg if looking for a literal version of a special character in Regex eg <code>\.</code> finds only any period </td> 
  </tr>
		  <tr>
    <td>12</td> <td><code>\s</code></td>  <td>any whitespace character</td> 
  </tr>
		  <tr>
    <td>13</td> <td><code>\S</code></td>  <td>any non-whitespace character</td> 
  </tr>
		  <tr>
    <td>14</td> <td><code>\d</code></td>  <td>any digit </td> 
  </tr>
		  <tr>
    <td>15</td> <td><code>\D</code> </td>  <td>any non-digit</td> 
  </tr>
	  <tr>
    <td>16</td> <td><code>\w</code> </td>  <td>any word character</td> 
  </tr>
	  <tr>
    <td>17</td> <td><code>\W</code> </td>  <td>any non-word character</td> 
  </tr>
	  <tr>
    <td>18</td> <td><code>\b</code> </td>  <td>any word boundary</td> 
  </tr>
	  <tr>
    <td>19</td> <td><code>a?</code></td>  <td>zero or 1 of "a"</td> 
  </tr>
	  <tr>
    <td>20</td> <td><code>t*</code> </td>  <td>zero or more of "t"</td> 
  </tr>
	 <tr>
    <td>21</td> <td><code>s+</code> </td>  <td>one or more of "s"</td> 
  </tr>
	 <tr>
    <td>22</td> <td><code>(tea ){3}</code> </td>  <td>exactly 3 "tea "s </td> 
  </tr>
	 <tr>
    <td>23</td> <td><code>b{4,}</code> </td>  <td>4 of more "b"s</td> 
  </tr>
	 <tr>
    <td>24</td> <td><code>h{7,9}</code></td>  <td>between 7 and 9 "h"s</td> 
  </tr>
	 <tr>
	 <th>Modifiers</th> 
  </tr>
	 <tr>
    <td>25</td> <td><code>/i</code> </td>  <td>case insensitive</td> 
  </tr>
	 <tr>
    <td>26</td> <td><code>/x</code>  </td>  <td>ignore whitespace in the expression</td> 
  </tr>
 <tr>
	 <th>Bonus addition</th> 
  </tr>
	 <tr>
    <td>27</td> <td><code>tea|coffee</code></td>  <td>tea or coffee</td> 
  </tr>

  
</table>

**Bonus**
* 27: **RegEx:** `tea|coffee` **English:** tea or coffee




### Nice studying! 
**Let's go back to those examples and see if we can understand them any better now...**
##### one
```
/\A[aeiou]/i
```
Okay so from the dictionary above, we're using elements  8, 1 and 25.
This would find any string which start with a vowel. Becasue we added the `/i` modifer, it doesn't matter if it's a lower or upper case vowel. Although at the start of the string we might expect it to be upper case, we're covered for any lazy typers!
<br><br><br>


##### two
```
/\bun\w*ing\b/
```
This one took me a while but it's looking more friendly each time I review it. We're using elements 18, 16, 20 and 18 again.
So we're looking through a string to find any parts which have: a word boundary followed by 'un' (`\bun`), then zero or more word characters (`\w*`), then 'ing' right before a word boundary(`ing\b`). So basically any word that begins with 'un' and ends with 'ing. it would pick up 'unifying' and 'uncomprimising' but not 'coming' or 'undeniable' since they don't start and end as requested in the Regex.
<br>
*Note:* `\w` *- word characters - include any letter, number or underscore so this expression would also pick up somthing like 'un4giving'. To avoid this and pick up only letters, we could change the expression to* `/\bun[a-z]*ing\b/`
<br><br><br>

##### three
```
\b\w{5}\b/i
```
Here we are using 18, 16, 23 and our fave 18 again with the modifier 25 for spice. We're looking for any 5 letter word. The modifier means it doesn't matter if the word is uppercase, lowercase or a mix.
<br><br><br>

##### four
```
/^[A-Z].+[\.|\!|\?]\z/
```
Another mindscrewer, here we're using a combo of 6, 4, 10, 21, 11, 27 and 9. Whhheewww! That's a bit wild so here's...
It will pick up a string that starts with a capital letter and ends in either a period, an exclamation mark or a question mark.
<br><br><br>

##### five
```
/^\D*(\d\D*){10}$/
```
Here's a phone number checker! It's basic and limited to find a 10-digit phone number regardless of whether it's been formatted as...
* 2438894546
* (718)891-1313
* 234 435 9978
* (800)4261134 

...or any other weird way. It won't pick up anything with more or less than 10 numbers in it, regardless of any extra bumpf there is in there.
It uses 6, 15, 14, 15, 20, 22 and 7.
<br><br><br>

##### six
```
/\b[(\!)(\?)(\.)]+/
```
This final one I just pulled out in a unrelated lab which was exciting because I was actually able to find a use for it 'in the wild'. The test called for a method which would count how many individual sentences there are in a string.
Here's the test:
```
  describe "#count_sentences" do

    it  "returns the number of sentences in a string" do
      expect("one. two. three?".count_sentences).to eq(3)
    end

    it "returns zero if there are no sentences in a string" do
      expect("".count_sentences).to eq(0)
    end

    it "returns the number of sentences in a complex string" do
      complex_string = "This, well, is a sentence. This is too!! And so is this, I think? Woo..."
      expect(complex_string.count_sentences).to eq(4)
    end
  end
	```

so I pulled out some Regex to pass to the `.split` method and ended up with this rather nice thing:<br>
```self.split(/\b[(\!)(\?)(\.)]+/).length```

## Further resources
* [Rubular](http://rubular.com/) *Test your RegEx for use in Ruby here!*
* [Regexr](https://regexr.com/) *You can test here too **and** it amazingly shows you what each element is doing! Designed for RegEx in JS but an excellent playground for general RegEx exploration.*
* [Rex Egg](http://www.rexegg.com/) *Special mention as it features dinosaurs*

# Now you're ready to explore Regex-land 
**And now you can order a coffee in the local language!**<br>
`/(latte|cortado|cappuccino|chai) with (oat|almond) milk/i`

<br>

<img src="https://static.pexels.com/photos/158557/coffee-cup-and-saucer-black-coffee-tea-spoon-158557.png" alt="Coffee time" style="width: 100%;"/>







