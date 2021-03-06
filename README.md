
# JUtilities


Functional utilities for Java Android projects

Currently containing Option that can be used with Java 1.7.

##Option

Similar to Java 8 Optionals but mainly targeting Android and Java 7 here. 

###Why to use them?

In 1965,  Sir Tony Hoare introduced null reference.  Since then he apologised for that and called it “A Billion dollar mistake”. 
If the inventor of null pointers and references has condemned them,  why the rest of us should be using them?


###Where to use them?

Currently there are several ways to say that an object could be null.  Most popular way in Android nowadays is using Nullable or NonNull annotations. 
The problem with those annotations is that you cannot say what kind of objects are in an array,  or if you use Rx,  in an observable.
With Options you can instead ```List<Option<String>>``` of in Rx ```Observable<Option<Integer>>```.

###How to use them?

Basic pattern matching:
``` Java
String result = Option.ofObj("This string might have been null")
                      .match(str -> "Length of the string is " + str.length(),
                             () -> "The string did not exist");
```

Operating on Option:
```Java
String result = Option.ofObj("This string might have been null")
                      .filter(str -> str.contains("null"))
                      .map(str -> "This String contains word null: " + str)
                      .ofDefault(() -> "Did not find matching world in the String");
```

Using flatMap:

```Java
String result = Option.ofObj(firstString)
                      .flatMap(first -> Option.ofObj(secondString)
                                              .map(second -> String.format("Both Strings are valid: %s,  %s", first,  second))
                      .ofDefault(() -> "Some of the Strings were invalid");
```

###How to use them?

JUtilities are available on maven. Just add to you gradle files:

To your top level gradle.build file add repository:
```
repositories { 
        jcenter()
        maven { url "https://jitpack.io" }
}
```

To your module level gradle.build add dependency: 
```
dependencies {
    // other dependencies
    compile 'com.github.tomaszpolanski:JUtilities:1.0'
}
```


##References

This library was strongly inbluenced by [C# Functional Language Extensions](https://github.com/louthy/language-ext)
