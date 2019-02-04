# Java

Java Keywords: import, super, final/finally/finalize, static, public, protected, private, synchronized

**Abstract class and Interface\(both can’t be instantiated\)**:

• Abstract class: can contain data member, can have concrete methods, only extend one abstract class

• Interface: can only have abstract methods, extending class must implement all methods, can implements multiple interfaces, can’t have any fields

**final/finalize/finally:**

• Final class con’t be inherited, final methods can’t be override, final variable can’t be changed

• Finally is used to placed code, it will be proceed no matter if the exception is handled or not

• Finalize is used to perform clean up operation when object is going be to garbage collected

**Override and Overload:**

• Overload happens in compile-time and override happens in run-time

• Overloading -&gt; static binding, overriding -&gt; dynamic binding

• Override happens in inheritance, child class specifies the implementation of methods

• Overload always in the same class, differs by parameters

**Encapsulation:**

• make fields of a class private and provide public methods to access fields

• Pros: can modify out implementation without breaking other code using this class

Compile Process\(Java/C++\):

**Java:**

• source code through compiler and get .class file containing platform-independent byte codes

which can be interpreted by JVM\(javac temp.java\)

• JVM will convert the byte codes into platform-dependent machine code \(java temp.class\)

**C++:**

• Preprocessor precesses directives before compilation\(g++ -E .cpp\)

• Compiler compile the preprocessed source code int assembly code\(g++ -S .cpp\)

• Assembler takes the assembly code and converts into object code\(gcc -c .cpp\)

• Linker links the object codes with library object file and forms an executable file

**Memory Management:**

• Local Variable and Methods resides in stack

• Objects and Instance Variable\(class member\) reside in heap

• Objects declared in methods are just reference to objects, the references are in stack

• Garbage Collection: an object becomes eligible for garbage collection when it lost its last

reference: out of scope; assign reference to another object; reference to null

Singleton: Ensure that only one instance of a class is created

```
class Singleton {
    private Singleton() {}
    private static class SingletonHolder {
        static final Singleton INSTANCE = new Singleton();
    }
    public static final Singleton getInstance() {
        return SingletonHolder.INSTANCE;
    }
}
```

**hashcode\(\) and equals\(\):**

* hashcode\(\): generate unique integer for each object in heap, mapping the memory address to an integer value
* equals\(\): by default, if two references refer to same object, “==”; can be override to compare contents of two objects
* If equal, must have same hash code; same hash code can’t guarantee equal objects

**Collection\(List and Set\):**

• List: stores an ordered collection of elements, allow duplicates, sequence matters

• ArrayList/LinkedList:

* -&gt; ArrayList: dynamic arrays. Fast in search and indexing
* -&gt; LinkedList: provides linked-list based data structure. Fast in insert and remove

• Array and List: List no need to preassigned memory

• Set: cannot contain duplicate elements, uniqueness matters

• TreeSet/HashSet/LinkedHashSet\(no duplicate\)

* -&gt; TreeSet: implement using a tree for storage, elements are ordered by natural order
* -&gt; HashSet: implement Set by hash table, can access elements very quickly\(hash code\), constant time for basic operations, no order
* -&gt; LinkedHashSet: implemented as a hash table, provide order of insertion

•Queue: ordered list maintaining FIFO, can be implemented by LinkedList and PriorityQueue

•PriorityQueue: unbounded priority queue based on a priority heap

**Map\(K/V pairs, no duplicate keys\):**

• HashMap: implement Map interface by hash table, permit null keys and null values, no order, unsynchronized, store Key/Value Entry

-&gt; How HashMap works:

1. when add a new K/V entry, calculate the hash code of the key to locate a bucket and store Key/Value Entry

2. when get\(Key\), calculate the hash code of the key object to locate the bucket, then use equals\(\) method to match key objects and return the value

3. exceed load factor: rehash the hash table and bucket to twice\(race condition\)

4. collision: two key objects map to same bucket\(same hash code\)
5. Hash Function: calculate hash code, return same result to same object

•HashTable: differs with HashMap only by not permit null key or null value, use fast-fail iterator, synchronized

• TreeMap: red-black tree based, sorted by natural ordering of keys, not synchronized

* -&gt; O\(logn\) time complexity to get\(\), remove\(\), put\(\)

• LinkedHashMap: Hash table and linked-list implementation of the Map interface, maintain

insertion order, not synchronized

* -&gt; Suitable for LRU cache

Iterator: Iterator interface provides methods to iterate over any Collection

Comparable/Comparator\(both are interfaces\):

• Comparable\(Internal\): imposes a total ordering on the objects of each class that implements

it, make sure the objects can compare itself with another objects

* -&gt; List — Collections.sort\(\)
* -&gt; only one method: compareTo\(\)

•Comparator\(External\): external to the element type we are comparing, need to create

separate classes to conduct comparison job, can have different sorting attributes

String, StringBuffer and StringBuilder:

• Difference: Use StringBuilder whenever possible because it is faster than StringBuffer. But, if thread safety is necessary then use StringBuffer objects

**Immutable Objects:**

• An immutable object can’t be changed once it is created.

• String: Since String is immutable it can safely be shared between many threads ,which is considered very important for multithreaded programming.

Exceptions:

• Two subclass of Exception: IOException, RunTimeException

• NullPointerException: A NullPointerException is thrown when calling the instance method of a null object, accessing or modifying the field of a null object

• RunTimeException: Unchecked exception, can be ignored and not checked during compilation

• Throws: when a method does’t handle a checked exception or could throw an exception, it must declare it by using throw keyword

• Difference between throw and throws:

-&gt; Throw is used to trigger an exception where as throws is used in

declaration of exception.

• Throwable\(superclass\)

* -&gt; Error\(not catched\)
* -&gt; Exception\(catched\)

• Two types of Throwable:

* -&gt;unchecked: a method can throw without declaring them in a “throw” clause, all Errors and RunTimeExceptions are unchecked
* -&gt;checked: These exceptions cannot simply be ignored at the time of compilation. If call a method that throws an Exception, must try/catch.

**all Exceptions except RunTimeException are checked**

•Finally: code will run regardless of an exception;

When try/catch has a return statement, flow jumps to finally then to return

**Volatile**: the value of a volatile field becomes visible to all readers \(other threads in particular\) after a write operation completes on it

