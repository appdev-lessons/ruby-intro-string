# The String class

Let's start by getting a more formal introduction to our friend, `String`.

First of all, notice that when I refer to Ruby classes, I capitalize the first letter. The _only_ time we use capital letters when we're programming is when we refer to Ruby classes. All other times — variable names, file names, etc — we're going to use lowercase letters only (other than when we're writing some copy inside a `String`, of course).

## Creating strings

We've actually been taking a shortcut this whole time when we've been saying something like

```ruby
s = "Hello, world!"
```

In Ruby, the formal way to create a new object is to use the `.new` method on the parent class:

```ruby
s = String.new
```

This will, however, just give us back an empty string `""`; but we can ask any object in Ruby what it is with the `.class` method:

```ruby
# create a new string and print its class
s = String.new
pp s
pp s.class
```
{: .repl #new_string title="New String" points="1"}

## Make the invisible visible

Let's practice **making the invisible visible**. Remove the leading `#` from the `pp` print statements one by one, and run the code each time with the "Run" button.

```ruby
# One-by-one, uncomment the p statements 
# below and rerun the code
s = String.new
# pp s 

s = "Hello, world!"
# pp s

s = s.upcase
# pp s
```
{: .repl #uncomment_each_line title="Make it visible" points="1"}

- In the code above, which of the following is true?
- The variable `s` contained *both* `"Hello, world!"` and `"HELLO, WORLD!"` in the end
    - Really? Did you try it?
- We completely overwrote the original `"Hello, world!"` content of `s`
    - Yes! Remember we can have `s` on both sides of a variable assignment operator
- We overwrote the variable `s` with new content, but we should never do that in real Ruby code in our apps
    - Nope. This is a very common step and you should get used to seeing it.
- None of the above
    - Not quite, experiment with the code a bit more.
{: .choose_best #invis_to_vis title="Invisible to visible" points="1" answer="2" }

## ASCII Codes 

With the `String.new` approach, we would have to add each character to our variable `s` one by one. One way to do so is by using the `.concat` method, which accepts a number as an argument, interprets it as an ASCII code, translates it into a single character, and adds it on to the end of the original string.

What's an ASCII code? At the hardware level, computers only store integers (specifically, in _binary_ form — using only `0`s and `1`s); so all other datatypes need to be encoded somehow as a number. [ASCII](https://en.wikipedia.org/wiki/ASCII), or American Standard Code for Information Interchange, was one scheme that was developed in the early days of computing to store English characters as integers. The codes are as follows:

<aside markdown="1">
Nowadays we use much more sophisticated encoding schemes such as [Unicode](https://en.wikipedia.org/wiki/Unicode) that supports glyphs from many more languages, and even emojis 🙌🏾 Fortunately, Ruby handles most of this low-level stuff for us behind the scenes, so we never really have to worry about it anymore.
</aside>


**ASCII Code**|**Character**|**ASCII Code**|**Character**|**ASCII Code**|**Character**|**ASCII Code**|**Character**|**ASCII Code**|**Character**|**ASCII Code**|**Character**
:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:
32|(space)|48|`0`|64|`@`|80|`P`|96|<code>`</code>|112|`p`
33|`!`|49|`1`|65|`A`|81|`Q`|97|`a`|113|`q`
34|`"`|50|`2`|66|`B`|82|`R`|98|`b`|114|`r`
35|`#`|51|`3`|67|`C`|83|`S`|99|`c`|115|`s`
36|`$`|52|`4`|68|`D`|84|`T`|100|`d`|116|`t`
37|`%`|53|`5`|69|`E`|85|`U`|101|`e`|117|`u`
38|`&`|54|`6`|70|`F`|86|`V`|102|`f`|118|`v`
39|`'`|55|`7`|71|`G`|87|`W`|103|`g`|119|`w`
40|`(`|56|`8`|72|`H`|88|`X`|104|`h`|120|`x`
41|`)`|57|`9`|73|`I`|89|`Y`|105|`i`|121|`y`
42|`*`|58|`:`|74|`J`|90|`Z`|106|`j`|122|`z`
43|`+`|59|`;`|75|`K`|91|`[`|107|`k`|123|`{`
44|`,`|60|`<`|76|`L`|92|`\`|108|`l`|124|`|`
45|`-`|61|`=`|77|`M`|93|`]`|109|`m`|125|`}`
46|`.`|62|`>`|78|`N`|94|`^`|110|`n`|126|`~`
47|`/`|63|`?`|79|`O`|95|`_`|111|`o`|
{: .bleed-full }

Given those ASCII codes, we can now build up a new string from scratch like so:

(Note: the `.concat` method can modify the variable `my_string` "in place"; meaning we don't need an intermediate variable at every step.)

```ruby
# instantiate a new variable of String class
my_string = String.new

# make the invisible visible!
pp my_string

# use the concat method to add characters
# one-by-one to the empty string variable
my_string.concat(72)
my_string.concat(101)
my_string.concat(108)
my_string.concat(108)
my_string.concat(111)
my_string.concat(44)

# make the invisible visible!
pp my_string

# add some more characters again
my_string.concat(32)
my_string.concat(119)
my_string.concat(111)
my_string.concat(114)
my_string.concat(108)
my_string.concat(100)
my_string.concat(33)

# make the invisible visible!
pp my_string
```
{: .repl #ascii_build title="ASCII Build" points="1"}

That's a lot of `concat`s! Just for fun, you give it a try. Make this graded code block say "Ruby <3" using only `.concat` to get the test to pass:

```ruby
my_string = String.new

# use .concat and pp to build the String
```
{: .repl #ascii_build_ruby title="concat some ASCII"}

```ruby
describe "concat some ASCII" do
  it "should print 'Ruby <3'" do
    path = "/tmp/code.rb"

    File.foreach(path) do |line|
      if line.match?(/Ruby <3/)
        expect(line).to_not match(/Ruby <3/),
          "Expected graded code block to NOT print the String literal 'Ruby <3', but did."
      end
    end

    expect { require_relative(path) }.to output(/Ruby <3/).to_stdout
  end
end
```
{: .repl-test #ascii_build_ruby_test_1 for="ascii_build_ruby" title="concat some ASCII should print 'Ruby <3'" points="1"}

## String literals 

Done with `concat`? What a pain! Now that we've shown that, under the hood, even creating a string follows the syntax of `noun.verb` — let's never do it again. From now on, we'll use the shortcut of creating string "**literals**" in place by typing the characters we want within quotes: `"Thank goodness!"`

These kinds of exceptions to the regular grammar in order to make life easier are known as "**syntactic sugar**".

## Methods

Next, let's familiarize ourselves with some of the `String` class's methods. Work through the runnable and graded code blocks associated with each method as you go.

### String addition, a.k.a. + 

We've already met the `.concat` method. `.concat` can accept an integer as an argument, which it interprets as an ASCII code, translates into a single character, and adds to the original string:

```ruby
pp "hi".concat(33)
```
{: .repl #concat_hi title="hi!" points="1"}

`.concat` can also accept a string literal as an argument, in which case it just adds the whole thing to the end of the original string.

```ruby
pp "hi".concat(" there") 
```
{: .repl #concat_literal title="Concat with literal" points="1"}

There's also a shorthand for `.concat`: `.+`. That may look a little funny, but it's nothing special, really; it's just a method with a very short (one letter long) name:

<aside markdown="1">
`.concat` as a shorthand for `.+` is not _quite_ true. The `+` method is not just an alias for `concat` — they do slightly different things. But they're close enough, for our purposes.
</aside>

```ruby
pp "hi".+(" there") # => "hi there"
```

But here's where it gets interesting; Ruby has another bit of nice _syntactic sugar_ for us. If a class has a method named `+`, then you are allowed to drop the `.` before the method name when you call it, and just say:

```ruby
"hi" +(" there") # => "hi there"
```

Wild! And, as we learned earlier when we were [introduced to the `pp` method](https://learn.firstdraft.com/lessons/8-ruby-intro-program-notes#make-the-invisible-visible), Ruby also allows you to omit the parentheses around arguments if you want to; so this can be further shortened to:

```ruby
pp "hi" + " there"
```
{: .repl #concat_plus title="Adding Strings" points="1"}

Now this is really starting to look familiar! It's a lot like the calculator language, actually. [Developer happiness](https://learn.firstdraft.com/lessons/8-ruby-intro-program-notes#developer-happiness), indeed.

Pass the next graded code block test by getting the terminal to print "Hello, world!" using two variables and the `+` addition method:

```ruby
first_part = "Hello,"

# create another variable and use "+" to 
# add it to the first_part, then print it
```
{: .repl #add_strings title="Adding Strings as variables"}

```ruby
describe "Adding Strings as variables" do
  it "should print 'Hello, world!'" do
    path = "/tmp/code.rb"

    File.foreach(path) do |line|
      if line.match(/^p.*"Hello, world!"/)
        expect(line).to_not match(/Hello, world!/),
          "Expected graded code block to NOT print the String literal 'Hello, world!', but did."
      end
    end
    
    assignment_counter = 0
    File.foreach(path) do |line|
      if line.include?("=") 
        unless line.include?("#")
          assignment_counter += 1
        end
      end
    end
    expect(assignment_counter).to be >= 2,
      "Expected graded code block to use at least two variables to store parts of the string before adding, but #{assignment_counter} '=' found."
    
    plus_counter = 0
    File.foreach(path) do |line|
      if line.include?("+") 
        unless line.include?("#")
          plus_counter += 1
        end
      end
    end
    expect(plus_counter).to be >= 1,
      "Expected graded code block to use the + plus method, but #{plus_counter} '+' found."

    expect { require_relative(path) }.to output(/Hello, world!/).to_stdout
  end
end
```
{: .repl-test #add_strings_test_1 for="add_strings" title="Adding Strings as variables should print 'Hello, world!'" points="1"}

### String multiplication, a.k.a * 

`String`s can be multiplied by numbers using the `*` method:

```ruby
"Ya" * 5 # => "YaYaYaYaYa"
```

<aside markdown="1">
More syntactic sugar here, like with the `+` method above; you can say `"Ya" * 5` rather than `"Ya".*(5)`.
</aside>

This sort of makes sense, if you think about multiplication as being repeated addition.

Get this next graded code block to say "HelloHelloHello" using the new `*` method:

```ruby
pp "Hello"
```
{: .repl #multiply_string title="Hello x 3"}

```ruby
describe "Hello x 3" do
  it "should print 'HelloHelloHello'" do
    path = "/tmp/code.rb"

    File.foreach(path) do |line|
      if line.match(/^p.*"HelloHelloHello"/)
        expect(line).to_not match(/HelloHelloHello/),
          "Expected graded code block to NOT print the String literal 'HelloHelloHello', but did."
      end
    end
    
    expect { require_relative(path) }.to output(/HelloHelloHello/).to_stdout
  end
end
```
{: .repl-test #multiply_string_test_1 for="multiply_string" title="Hello x 3 should print 'HelloHelloHello'" points="1"}

The order matters, though. See what happens when you try:

```ruby
pp 3 * "Hello"
```
{: .repl #order_matters title="Order matters" points="1"}

[Read The Error Message (RTEM)](https://learn.firstdraft.com/lessons/67-ruby-intro-fundamentals#seriously-please-read-the-error-message)!

Does this make sense? `"Hello" * 3` is calling the `String` method `*` with an argument of `3`, which kinda makes sense (add `"Hello"` to itself `3` times).

But `3 * "Hello"` is calling the `Integer` method `*` with an argument of `"Hello"`, which doesn't make much sense (what would it mean to add `3` to itself `"Hello"` times?).

Thus, we can see why the `String` version of `*` and the `Integer` version of `*` both need an integer argument. Again, [the bottom line](https://learn.firstdraft.com/lessons/67-ruby-intro-fundamentals#the-bottom-line) is — at all times as you are writing Ruby, you should be thinking: "What **class** is this object? What **methods** does _this_ class have available?" Even when there's some syntactic sugar making things _look_ unconventional, don't forget your basics! It's still `noun.verb` under the hood.

### reverse 

The reverse method returns a new `String` with the characters from the `String` in reverse order.

```ruby
pp "I can speak in backwords words".reverse
```
{: .repl #reverse title="Reverse" points="1"}

### upcase 

The upcase method returns a copy of the `String` with all lowercase letters replaced with their uppercase counterparts.

```ruby
pp "hello".upcase
```
{: .repl #upcase title="Upcase" points="1"}

### downcase 

The downcase method returns a copy of the `String` with all uppercase letters replaced with their lowercase counterparts.

```ruby
pp "I'M NOT YELLING AT YOU".downcase
```
{: .repl #downcase title="Downcase" points="1"}

### swapcase 

The swapcase method returns a copy of the `String` with all uppercase letters replaced with their lowercase counterparts, _and_ vice versa.

```ruby
pp "FaMiLy".swapcase
```
{: .repl #swapcase title="Swapcase" points="1"}

Using the supplied variables and the previous methods, get this graded code block to output "HELLO friends AnD FaMiLy" on one line:

```ruby
greeting = "hello"
people = " FRIENDS"
other_people = " aNd fAmIlY"

# use the "case" methods and + (String addition)
# to print the requested output
```
{: .repl #case_methods title="Changing cases" readonly_lines="[1, 2, 3]"}

```ruby
describe "Changing cases" do
  it "should print 'HELLO friends AnD FaMiLy'" do
    path = "/tmp/code.rb"

    File.foreach(path) do |line|
      if line.match(/^p.*"HELLO friends AnD FaMiLy"/)
        expect(line).to_not match(/HELLO friends AnD FaMiLy/),
          "Expected graded code block to NOT print the String literal 'HELLO friends AnD FaMiLy', but did."
      end
    end
    
    expect { require_relative(path) }.to output(/HELLO friends AnD FaMiLy/).to_stdout
  end
end
```
{: .repl-test #case_methods_test_1 for="case_methods" title="Changing cases should print 'HELLO friends AnD FaMiLy'" points="1"}

### gsub 

The `gsub` method returns a copy of the `String` it was called on with all occurrences of the first argument substituted for the second argument.

```ruby
a = "Hello"
pp a.gsub("ll", "ww")
```
{: .repl #gsub_letters title="gsub letters" points="1"}

Make the graded code block below output "put spaces in between these words" using the starting variable and the `gsub` method:

```ruby
sentence = "put_spaces_in_between_these_words"
```
{: .repl #gsub_spaces title="Add spaces with gsub" readonly_lines="[1]"}

```ruby
describe "Add spaces with gsub" do
  it "should print 'put spaces in between these words'" do
    path = "/tmp/code.rb"

    File.foreach(path) do |line|
      if line.match(/^p.*"put spaces in between these words"/)
        expect(line).to_not match(/put spaces in between these words/),
          "Expected graded code block to NOT print the String literal 'put spaces in between these words', but did."
      end
    end
    
    expect { require_relative(path) }.to output(/put spaces in between these words/).to_stdout
  end
end
```
{: .repl-test #gsub_spaces_test_1 for="gsub_spaces" title="Add spaces with gsub should print 'put spaces in between these words'" points="1"}
 
### strip 

`strip` removes all leading and trailing whitespace.

```ruby
pp "   This has a lot of space on the outside     ".strip
```
{: .repl #strip title="Strip" points="1"}

### capitalize 

capitalize returns a `String` with the first character converted to uppercase and the remainder to lowercase.

```ruby
pp "beginning".capitalize
```
{: .repl #capitalize title="Capitalize" points="1"}

- Is `"   hi  ".strip.capitalize + "!"` a valid way to output `"Hi!"`? (You can always try it in the runnable code block above.)
- Yes
    - Exactly. We can chain methods together!
- No
    - Actually, it is. We can chain methods together!
{: .choose_best #chain_methods title="Chaining methods" points="1" answer="1" }

## Conclusion

That's it for `String` for now. We'll come back to them later. Next, we'll take a look at numbers, starting with `Integer`.

- Approximately how long (in minutes) did this lesson take you to complete?
{: .free_text_number #time_taken title="Time taken" points="1" answer="any" }

<span style="font-size: large">**When you are done here, close the window and return to Canvas for the next lesson in the series.**</span>

----
