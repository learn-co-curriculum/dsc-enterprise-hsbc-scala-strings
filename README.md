
# `String`

String is the same object as in the Java

`StringOps` is an implicit wrapper class to provide added functionality that Java does not have.


```scala
val s = "Scala"
```

Can be declared, but unnecessary due to inference


```scala
val s:String = "Scala"
```

Type can be added by coercion


```scala
val s = "Scala":String
```

## `String` format and Interpolation

`String` can be formatted with C-style/Java format flags

Here is the Java-Style before, which still works in Scala


```scala
String.format("This is a %s", "test")
```

Here is the Scala style:


```scala
"This is a %s".format("test")
```

For a reference on the types of flags: http://docs.oracle.com/javase/8/docs/api/java/util/Formatter.html

Changing the order of arguments using format
Without specifying order, format will use the order provided:


```scala
println("Because you're %s, %s, %s times a lady".format("Three", "Twice", "Once"))
```

The above will surely render incorrectly (if you know the song):
```
Because you're Three, Twice, Once times a lady
```

To specify order we can use the `format %n$s` where `n` is the which argument we wish to use and `s` is the type. In this case, `String`.


```scala
println("Because you're %3$s, %2$s, %1$s times a lady".format("Three", "Twice", "Once"))
```

This will render:

Because you're Once, Twice, Three times a lady
The above can be trimmed to the following using printf

printf("Because you're %3$s, %2$s, %1$s times a lady", "Three", "Twice", "Once")

## Formatting Dates and Times

Java Time came with Java 8 and compliments well with Scala


```scala
import java.time._
println("We will be eating lunch on %1$tB the %1$te in the year %1$tY".format(LocalDate.now))
```

NOTE: The underscore for the import (_) is analogous to the asterisk in (*) in Java

## Smart Strings
Smart Strings are surrounded 3 x `"`

They allow multi-lines of code


```scala
val prose = """I see trees of green,
               red roses too
               I see them bloom,
               for me and you,
               and I think to myself,
               what I wonderful world"""
```

The problem with the above is that it that the margins are misaligned.

## Smart Strings with stripMargin

`stripMargin` can align the strings based on the pipe (`|`) by default


```scala
val prose = """I see trees of green,
               |red roses too
               |I see them bloom,
               |for me and you,
               |and I think to myself,
               |what I wonderful world""".stripMargin
```

## Smart Strings with customized stripMargin
stripMargin can align the strings based on a character of your choice.


```scala
val prose = """I see trees of green,
               @red roses too
               @I see them bloom,
               @for me and you,
               @and I think to myself,
               @what I wonderful world""".stripMargin('@')
```

## Smart Strings with combination format

Since Smart Strings are just `String` you can use all the same methods, including `format`

Here we will use format to include the colors


```scala
val prose = """I see trees of %s,
               |%s roses too
               |I see them bloom,
               |for me and you,
               |and I think to myself,
               |what I wonderful world""".stripMargin
                                         .format("green", "Red")
```




    prose: String =
    I see trees of green,
    Red roses too
    I see them bloom,
    for me and you,
    and I think to myself,
    what I wonderful world
    



## String Interpolation
You can replace any variable in a string from it’s environment or context with string interpolation

The only thing that you require is that the letter s precedes the string.

You can refer to an outside variable by using `$` to precede it, for example `$a`

If you require an expression wrap the expression in a bracket, for example, `${a + 1}`


```scala
val a = 99 //Setting up a value within the context
println(s"$a luftballoons floating in the summer sky")
```

## The `f` interpolator
Used to combine `String.format` functionality with String interpolation


```scala
val ticketsCost = 50
val bandName = "Psychedelic Furs"
println(f"The $bandName%s tickets are probably $$$ticketsCost%1.2f")
```

`$bandName%s` treats the interpolation as a String

`ticketsCost%1.2f` treats the cost with a width of `1` if possible and two decimal points

`$$` is used to escape the dollar sign

## Extra decoration for the f interpolator

The formats allowed after the `%` character are all part of the standard Formatter

http://docs.oracle.com/javase/8/docs/api/java/util/Formatter.html

Therefore, we can also try `%n` for a newline and `%%` for a percent.


```scala
val ticketsCost = 50
val bandName = "Psychedelic Furs"
val percentIncrease = 20
val musicGenre = "New Wave"
println(f"""The $bandName%s tickets are probably $$${ticketsCost%1.2f}
            |That's a ${percentIncrease}%% bump because everyone
            |likes ${musicGenre}""")
```

## Smart Strings and Regexes

Regular Strings are pretty terrible for creating regular expressions since you have to escape backslashes with to two backslashes:


```scala
val regex = "(\\d{3})-(\\d{4})".r //Yuck
```

the `.r` method creates a `scala.util.matching.Regex` object

A Smart String allows us to create a regex without having the two backslashes


```scala
val regex = """(\d{3})-(\d{4})""".r //Awesome!
```

Here is an example of what one can do with a regex and a method called `foreach` which will print each element in a collection


```scala
regex.findAllIn("My number is 404-3030").foreach(println)
```

## `String `Conclusion

* There are various ways to work with `String` in Scala
* You can use the standard String mechanisms you find in Java
* You can use smart string to create multilines.
* You can use the `format` method to do `String` style formatting
* You can also use string interpolation with varying flavors to do variable replacements in a `String`.
