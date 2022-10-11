# Future

Key Ideas

* Future - this is a callback function.  



```{admonition} Concept
**Future** - Flutter is a single threaded program.  This means that each function must complete before moving on to the next one. *Problem* - what if a function needs more time to wait for something? This would stop the program leaving the user waiting for it to complete. A call backback function will all the program to continue.  In Flutter, future is the command to tell the program to continue and that function will finish sometime in the future.
```



## Key Terms

**Key terms:**

- **async**: You can use the `async` keyword before a function’s body to mark it as asynchronous.
- **async function**: An `async` function is a function labeled with the `async` keyword.
- **await**: You can use the `await` keyword to get the completed result of an asynchronous expression. The `await` keyword only works within an `async` function.

    https://dart.dev/codelabs/async-await#why-asynchronous-code-matters



# Lecture Code

```dart
import 'dart:async';

import 'dart:io';

Duration mywaittime = Duration(seconds: 5);

Future<void> function1() async {

  // simulates a wait state
  Future.delayed(mywaittime, () async {
    var thedata = await myDelayedData();
    print(thedata);
  });

  stdout.writeln("Who wants a hotdog?");

}

Future <String> myDelayedData() =>
    Future.delayed(mywaittime,()=>"** This is the delayed data **");

void function1a()  {

  // simulates a wait state
  Future.delayed(mywaittime, () {
    print(myDelayedData());
  });

  stdout.writeln("Function 1a");
}


void function2() {
  print("This is function 2");
}

void function3() {
  print("This is function 3");
}

main(List<String> arguments) {

  // toggle to comments to see the right and wrong ways
  
  stdout.writeln("\nThe Wrong Way");
  function1a();
  function2();
  function3();

/*
  stdout.writeln("\nThe Right Way");
  function1();
  function2();
  function3();
*/

}



```



## Example 2

``` Dart
import 'dart:async';
 
Duration myseconds = Duration(seconds: 10);
 
Future<void> waitOnInfo() async{
 
    await waitOnSomething();
 
}
 
Future<void> waitOnSomething() async{
	//code that takes a while goes here
	Future.delayed(myseconds,(){
        
	//this is programming a pause
	//for this example 
	//get some data wait a while;
	print("Now its Done");
	});
	//return "Item 1a - thedata";	
}
 
void function2()
{
	print("Item 2");
}
void function3()
{
	print("Item 3");
}
main(List<String> arguments) {
 
    waitOnInfo();
    function2();
    function3();

    waitOnSomething();
 
}
```

