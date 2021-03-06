If we want to add functionality to a class that already exists, in languages like Java, you would use the _Decorator Pattern_ or _Adapter Pattern_ to add that functionality. In Scala, you still use the _Adapter Pattern_ but the compiler fuses the adapter to the target automatically, giving you the look and feel of one single class with your additional methods.

Enter the following into your editor:

<pre class="file" data-filename="src/MyApp.scala" data-target="replace">

package com.xyzcorp;

class IntWrapper(x:Int) {
  def isOdd: Boolean = x % 2 != 0
  def isEven: Boolean = !isOdd
}

object MyApp extends App {
  // Tell the compiler that I intend to perform a conversion
  import scala.language.implicitConversions
  
  // Define the conversion, for every Int wrap or adapt an IntWrapper
  // This is only applicable for this scope, inside the App
  implicit def int2IntWrapper(x:Int):IntWrapper = new IntWrapper(x)
  
  println(10.isOdd)
  println(10.isEven)
}

</pre>

We will then compile

`scalac -d target src/MyApp.scala`{{execute}}

Then we will run

`scala -cp target com.xyzcorp.MyApp`{{execute}}

