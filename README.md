03_Queue_Lab
============

Implement an array-based queue in C++

Note: When you create your project, do NOT add ArrayQueue.ipp to the list of source files, add it to the list of include files. You will see that ArrayQueue.ipp is #included at the bottom of ArrayQueue.h. See ArrayQueue.h for more explanation.

Requirements
------------

1. remove takes O(1) time
2. add takes O(1) time, unless it calls grow (in that case O(n) is okay)
3. grow is only called if the number of items == backingArraySize, and the size of the array is doubled during grow
4. grow takes O(n) time
5. Do not leak memory (make sure grow and the destructor do the right thing)
6. getNumItems is O(1) time
7. add and remove throw excpetions as appropriate
8. You must use the array in a circular fashion. If you don't do this you probably won't be able to get #1, #2 and #3 to all be true.

Reading
=======
"Open Data Structures," Chapter 2, up through section 2.4 (ArrayDequeue). http://opendatastructures.org/ods-cpp/2_Array_Based_Lists.html

Information about the Von Neumann computing model may be helpful. This optional reading is section 2.2 of "Algorithms and Data Structures: A Basic Toolbox" by Melhorn and Sanders. A free copy may be found here: http://www.mpi-inf.mpg.de/~mehlhorn/ftp/Toolbox/Introduction.pdf

Questions
=========

#### 1. Which of the above requirements work, and which do not? For each requirement, write a brief response.

1. Yes, it is constant time. Since it's a circular array it already knows where the information is, and doesn't need to
search the array.
2. Yes, it should be constant unless grow is called. Because the method doesn't need to go through the entire list 
to find where it needs to put information, it is constant. By modding we find out where there is space.
3. Under add() we find out if backingSizeArrray and numItems are equal. If they are, then we grow the array.
4. Grow has to be linear time because it takes information from one array and places it into another. So we "visit" every
piece of information with the method.
5. We delete the backingArray at the end, and set it to NULL (just in case).
6. Since getNumItems is a variable and a method, it is constant. (We just return the variable in the method).
7. Remove throws an exception when you try to use it on an already empty array.
8. That's why we use (front+numItems)%backingArraySize. So we can find the free spaces in the array, and move "front" to where the
array ends. Making an efficient use of space. 

#### 2. If we did a Stack instead of a Queue, which of the private methods and variables would we need to keep, and which could we get rid of? Explain your answer.
We would still need the size, a variable to keep track of the front and back of the stack, 
 and the amount of info in the array (numItems).
 
#### 3. What is one question that confused you about this excercise, or one piece of advice you would share with students next semester?
Start early on homework, and take notes during class. 

#### 4. In Java you might write "class ArrayQueue extends Queue" ... how do you write the same thing in C++?
class ArrayQueue : public Queue <T>

#### 5. What is the purpose of "templates" in C++?
A template lets the user create a class of any type of data. By using "T" it doesn't restrict the class from
being only strings, or ints, or floats, etc. Methods can return any type, and any type can be an input.

#### 6. What would the syntax be for dynamically allocating an array of 10 ints, in C++?
int* arr = new arr[10];

#### 7. What is the purpose of a class destructor in C++? Why don't you need them in Java?
The deconstructor closes everything you opened or created. So, it deletes any remaining variables, 
and "cleans up" once everything has run. The garabge collector is the deconstructor in java. The language cleans up for you.
