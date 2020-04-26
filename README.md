**LogApp project**

I have decided to implement Dependency Injection in order to have the ability to use more than one logging service through the ILog interface. In order to use a new logger you just have to register it  in Program.cs.

I have left the calls in LogApplication.cs the same as the calls in the given start project. The only difference being the way they are called.

**LogService.Service**
	As the requirements stated: the log should not be interrupted by an exception. So I have covered the Log method logic in a try catch block. On the catch it appends any errors that have occurred to a collection and generates an error log.

*   The Logger folder contains the ILog interface and all the classes that implement this interface. There is a TestLogger class also which is close to a copy of the FileLogger class. But was changed  in order to process unit tests correctly. I do not know what would be the best solution to this. But I would haven’t come up with anything better.
*   The MainLoop method has been changed:
    *   The name of the method is now Log;
    *   There were errors occurring when I initially tried to launch the project in this method so those were fixed. Also there was a bug on the date checking  part whether to create a file and continue writing data to that file.
*   Models folder contains all the used Models. In this case, only the LogLine model
*   Utilities folder contains 4 static classes that are used in different operations.
    *   **ErrorUtilities** - all error logging logic.
    *   **LineUtilities** - operations with LogLine objects 
    *   **TestUtilities** -  operations that are needed to accomplish unit tests.
    *   **LogUtilities** - contains only the ConfigureLogDirectory method. Which is used to configure the logging directory.

            (NOTE: similar methods with the same name are located in TestUtilities and ErrorUtilities).


**LogService.Tests**
	
I have written 4 unit tests to test the functionality of this application:

*   **Write_ShouldCreateAFileWithData()** - this tests the creation and writing of a file. It was hard for me to seperate those two operations into two tests.  And I am not sure if this is the best way to test this properly. I think an integration test would be better in this case. But I have no prior knowledge of these and I would prefer to not try and pretend that I do.
*   **Log_ShouldStopWithFlush()** - this tests the Stop with Flush functionality.  The number of lines written to the log should be the same as the counter value;
*   **Log_ShouldStopWithFlush()** - this tests the Stop without Flush functionality. 
*   **Log_ShouldCreateTwoFiles()** - this tests the functionality that if midnight occurs a new file should be created and logging should continue on that file.

The tests generate log text files which are stored in LogTest\Tests

**Summary**

All in all, this was pretty challenging. I have little to no experience working with the Thread class. And seeing that it was a big part of the initially given code I opted to leave as much as I possibly could without breaking anything and try to work around it. So I can not guarantee at this point that everything is working as required and this would be the point in time where I would ask for some insights. 

The things that are keeping me  from saying this a great solution:



*   Thread related parts;
*   Stream related parts;
*   not 100% SOLID;
