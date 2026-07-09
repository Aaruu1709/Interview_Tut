Since String is immutable...

Every concatenation creates a new object.

So tell me...

Why don't we always use String? Why do we need StringBuilder?
---------------------------------------------------------------------------------
String is immutable, which means every modification creates a new object.

If we repeatedly concatenate Strings, especially inside loops, many temporary String objects are created.

This increases memory usage and puts additional pressure on the Garbage Collector.

StringBuilder solves this problem because it is mutable.

Instead of creating a new object for every modification, it updates the existing character sequence internally.

That's why StringBuilder is preferred when we perform multiple String modifications, especially in loops.

-------------------------------------------------------------------------------------
Can you give me a practical example where you would use StringBuilder?
---------------------------------------------------------------------------------------
Strong Answer

Suppose I'm generating a CSV file, building a JSON response manually, creating a large SQL query dynamically, or appending log messages inside a loop.

In these situations, using String concatenation with + would create many temporary String objects.

Using StringBuilder allows all modifications to happen on the same object, making the operation much more memory-efficient.

-----------------------------------------------------------------
Follow-up Question 2

Now I ask

Then what is the difference between

String

StringBuilder

StringBuffer
------------------------------------------------------------------------------

The main difference is mutability and thread safety.

String is immutable, so every modification creates a new object.

StringBuilder is mutable and is not thread-safe, making it faster for single-threaded applications.

StringBuffer is also mutable, but its methods are synchronized, making it thread-safe.

Because synchronization introduces overhead, StringBuffer is generally slower than StringBuilder.

In most modern applications, I use StringBuilder unless multiple threads need to modify the same sequence of characters.

-------------------------------------------------------------------------------

Follow-up Question 3

Suppose you're writing code inside a loop.

Which one will you choose?
-------------------------------------------------------------------------------
I would use StringBuilder.

Since loops often perform repeated concatenation, using String would create many temporary objects.

StringBuilder avoids that overhead by modifying the same obje

-------------------------------------------------------------------------------

Follow-up Question 4

Suppose multiple threads are modifying the same String sequence.

Now what?
-------------------------------------------------------------------------------
n that case, I would use StringBuffer because it provides synchronized methods, making modifications thread-safe.

However, if thread safety isn't required, I'd prefer StringBuilder because it offers better performance.


-------------------------------------------------------------------------------
Follow-up Question 5

Now...

Real production question.

Suppose your application becomes slow.

Profiler shows millions of String objects.

What will you do?
-------------------------------------------------------------------------------

First, I'd identify where those Strings are being created using a profiler.

If repeated concatenation is happening inside loops, I'd replace it with StringBuilder.

I'd also review whether duplicate literals can be reused through the String Pool and whether unnecessary temporary Strings can be avoided.

Finally, I'd measure the impact after optimization instead of assuming the change improves performance.

--------------------------------------------------------------------------------
Follow-up Question 6

Now...

One of my favorite questions.

How does StringBuilder actually work internally
--------------------------------------------------------------------------------

Internally, StringBuilder maintains a resizable character array.

When we append data, it stores the new characters in that array instead of creating a new object.

If the array becomes full, it creates a larger array, copies the existing characters, and continues appending.

This is much more efficient than creating a new String object after every modification.

--------------------------------------------------------------------------------

Follow-up Question 7

Now...

Tricky one.

Is StringBuilder immutable?
--------------------------------------------------------------------------------
No.

StringBuilder is mutable.

Methods such as append(), insert(), delete(), and reverse() modify the same object instead of creating new ones.

--------------------------------------------------------------------------------

Follow-up Question 8

Now...

Coding question.

Which is better?

String s = "";

for(int i=0;i<1000;i++){

    s = s + i;

}

OR

StringBuilder sb = new StringBuilder();

for(int i=0;i<1000;i++){

    sb.append(i);

}
-------------------------------------------------------------------------------

The second approach using StringBuilder is better.

The first approach creates a new String object during every iteration because Strings are immutable.

The second approach modifies the same object, making it much more efficient in terms of memory and performance.

-------------------------------------------------------------------------------


String

↓

intern()

↓

Compile Time vs Runtime

↓

String Memory Diagram

↓

Coding Traps

↓

Production Scenarios

↓

Rapid Fire

↓

Interview Closing
-----------------------------------------------------------------
I see you've worked on Java.

Can you explain what intern() does?
-----------------------------------------------------------------------
he intern() method returns the reference of the String from the String Pool.

If an equivalent String already exists in the pool, intern() returns that existing pooled object.

If it doesn't exist, the String is added to the pool, and its pooled reference is returned.

This helps reduce duplicate String objects and improves memory efficiency when many identical Strings are created.

-------------------------------------------------------------------------------------
Why would we use intern()?
-------------------------------------------------------------------------------------

It's useful when an application creates many duplicate Strings dynamically.

By calling intern(), those duplicate values can share a single pooled object instead of creating multiple identical objects.

However, in most business applications, we don't call intern() explicitly because String literals already use the String Pool automatically.

-----------------------------------------------------------------------------------------------
```
String s1="Java";

String s2=new String("Java").intern();

System.out.println(s1==s2);
```
It prints true.

intern() returns the pooled reference.

Since "Java" already exists in the String Pool, both s1 and s2 point to the same pooled object.



-----------------------------------------------------------------------------------------------

Next Question
Compile Time vs Runtime
-----------------------------------------------------------------------------------------------

Tell me...

Which of these uses the String Pool?

String s="Java";

or

String s=new String("Java");

Good answer

String literals are resolved using the String Pool.

Objects created using new String() are created in the Heap.

Even though the literal "Java" may already exist in the pool, new String() creates an additional object.

-----------------------------------------------------------------------------------------------
What about this?

String s="Java";

String t="Ja"+"va";

Strong Answer

This is evaluated at compile time.

Since both values are String literals, the compiler optimizes the expression into "Java".

Therefore, both variables refer to the same pooled object.

-----------------------------------------------------------------------------------------------

String a="Ja";

String b="va";

String c=a+b;

Will this use String Pool?

Strong Answer

No.

Here, concatenation happens at runtime because a and b are variables.

The result is created as a new String object, so c does not automatically refer to the pooled literal.



-----------------------------------------------------------------------------------------------

Coding Trap
Aman

Predict the output.

String s1="Java";

String s2="Java";

System.out.println(s1==s2);

Answer

True.

Next.

String s1=new String("Java");

String s2=new String("Java");

System.out.println(s1==s2);

False.

Next.

System.out.println(s1.equals(s2));

True.

Next.

String s="Java";

s.concat("8");

System.out.println(s);

Output?

Strong answer

Java

Because String is immutable.

concat() returns a new String.

Since the returned object wasn't assigned back to s, the original String remains unchanged.

Excellent.

Next.

String s="Java";

s=s.concat("8");

System.out.println(s);

Output?

Java8
----------------------------------------------------------------------------
Production Scenario

-----------------------------------------------------------------------------------


our application is using too much memory.

Heap dump shows millions of duplicate Strings.

What will you do?
-----------------------------------------------------------------------------------
Strong answer

First, I'd identify where duplicate Strings are being created using a profiler or heap dump.

I'd check for unnecessary String creation through repeated concatenation or object creation.

I'd replace loop-based concatenation with StringBuilder where appropriate.

If the application creates many identical dynamic Strings, I'd evaluate whether intern() is suitable, but only after measuring its impact.

Finally, I'd verify the improvements through profiling instead of relying on assumptions.







-----------------------------------------------------------------------------------
Rapid Fire Round

Now...

I'm going to ask quickly.

Answer in one line.
-----------------------------------------------------------------------------------

Why is String immutable?


➡️ Thread safety, security, String Pool optimization, reliable HashMap keys.
-----------------------------------------------------------------------------------

Where is String Pool?

➡️ Inside Heap memory (special pool managed by JVM).
-----------------------------------------------------------------------------------

Is String thread-safe?

➡️ Yes, because it is immutable.
-----------------------------------------------------------------------------------

Why is String final?

➡️ To prevent subclasses from breaking immutability.
-----------------------------------------------------------------------------------

StringBuilder or StringBuffer?

➡️ StringBuilder for performance, StringBuffer when thread safety is required.
-----------------------------------------------------------------------------------

== or equals()?

➡️ == compares references.

➡️ equals() compares contents.
-----------------------------------------------------------------------------------

new String() or Literal?

➡️ Prefer literals unless you specifically need a separate object.
-----------------------------------------------------------------------------------

concat() modifies String?

➡️ No.

Returns a new object.
-----------------------------------------------------------------------------------
StringBuilder mutable?

➡️ Yes.
-----------------------------------------------------------------------------------

String synchronized?

➡️ No, but immutable objects are naturally safe to share.
-----------------------------------------------------------------------------------

-----------------------------------------------------------------------------------

-----------------------------------------------------------------------------------


-----------------------------------------------------------------------------------

-----------------------------------------------------------------------------------






