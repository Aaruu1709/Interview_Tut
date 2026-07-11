Object- Class
-------------------------------------------------------------------
"Why does every Java class extend Object?"
Can you tell me what Object class is?
-------------------------------------------------------------------
The Object class is the root parent class of Java. It is present in the java.lang package, and every class in Java directly or indirectly inherits from it.

Even if we don't explicitly extend any class, the Java compiler automatically makes our class extend Object.

The main purpose of the Object class is to provide a common set of methods that every Java object should have, such as toString(), equals(), hashCode(), clone(), getClass(), wait(), notify(), and notifyAll().

Because every class extends Object, we can write generic code that works with any type of object. It also enables concepts like polymorphism, where an Object reference can refer to an instance of any class.

--------------------------------------------------------------------
"Why does every Java class extend Object?"
------------------------------------------------------------------------------------
Every Java class extends the Object class because it provides a common foundation for all objects. This ensures that every object has basic functionalities like object comparison, string representation, hashing, runtime class information, and thread synchronization. It also allows Java to treat every object uniformly through an Object reference.
Everything starts from Object.
```
class Employee {

}

public class Test {
    public static void main(String[] args) {

        Employee emp = new Employee();

        System.out.println(emp.toString());
        System.out.println(emp.hashCode());
        System.out.println(emp.getClass());
    }
}
```
Even though we didn't write these methods inside Employee, we can call them because Employee automatically inherits them from Object.


--------------------------------------------------------------------
"Can you name some important methods of the Object class?"
--------------------------------------------------------------------
toString() → Returns the string representation of an object.
equals() → Compares two objects for logical equality.
hashCode() → Returns the hash code of the object.
clone() → Creates a copy of an object (if supported).
getClass() → Returns runtime class information.
wait(), notify(), notifyAll() → Used for thread communication in multithreading.
finalize() → Deprecated; it was used before an object was garbage collected.

--------------------------------------------------------------------
Follow-up Question 1
Why did Java create one parent class for every object?
----------------------------------------------------------------------------------------------------------------------------------------
Java introduced the Object class so that all objects share a common set of behaviors.
It provides common methods like toString(), equals(), hashCode(), and getClass() to every object, so developers don't have to implement these methods from scratch in every class.
Since every class extends Object, an Object reference can point to any Java object. This supports polymorphism and allows Java to handle different objects in a common way.

Even if the Employee class doesn't explicitly define toString(), it inherits that method from the Object class.

Therefore, every Java object has access to the methods defined in Object.


--------------------------------------------------------------------
Follow-up Question 2
Can you tell me some important methods of Object class?
--------------------------------------------------------------------
The methods I use most frequently are:

equals() → compares objects logically.
hashCode() → generates a hash value used by collections like HashMap.
toString() → provides a readable string representation of an object.
getClass() → returns runtime class information.

Other methods like clone(), wait(), notify(), and notifyAll() are available but are used in more specific scenarios.

--------------------------------------------------------------------
You create

Employee e1 = new Employee(101, "Aarti");

Employee e2 = new Employee(101, "Aarti");

Then

System.out.println(e1.equals(e2));
--------------------------------------------------------------------
By default, the equals() method inherited from the Object class compares object references, not the contents of the objects.

Although e1 and e2 contain the same data, they are two different objects created at different memory locations.

Since their references are different, the default implementation of equals() returns false.

##"By default, equals() compares object references, not object contents."
--------------------------------------------------------------------
Follow-up Question 3
Then why do we override equals()?
--------------------------------------------------------------------
We override equals() when two different objects should be considered equal based on their business data rather than their memory references.

For example, in an Employee Management System, two Employee objects with the same employee ID may represent the same employee, even if they are different objects in memory.

By overriding equals(), we define what "equal" means for our business domain.
##We override equals() to define business equality, not memory equality.
--------------------------------------------------------------------
Mwmory:
Why do you think Java compares references by default instead of comparing all object fields automatically
--------------------------------------------------------------------
By default, Java compares object references because it doesn't know what "equal" means for every class.

Every class has different business rules.

For example, two Employee objects might be considered equal based on employeeId, while two Student objects might be considered equal based on rollNumber, and two Product objects might be considered equal based on productCode.

Since Java cannot automatically decide which fields define equality, the default implementation simply checks whether both references point to the same object in memory.

If the business requires logical equality, developers should override the equals() method to define their own comparison rules.

--------------------------------------------------------------------
your company says:

"Employees are uniquely identified by id."
When you override equals(), which fields will you compare and why?
--------------------------------------------------------------------
In this case, I would compare only the id field because the business requirement clearly states that an employee is uniquely identified by their employee ID.

Even if other fields like name, email, or salary change over time, the employee's identity remains the same as long as the id is the same.

So, comparing only the id correctly reflects the business definition of equality and avoids treating the same employee as different just because some details were updated.


--------------------------------------------------------------------
You overrode equals() to compare only the id.

Now tell me...

Why do we also need to override hashCode()?

Why isn't overriding only equals() enough?
--------------------------------------------------------------------
HashMap and HashSet use both hashCode() and equals() together.

The hashCode() method is used first to determine the bucket where an object should be stored or searched.

Only if two objects have the same hash code does Java call equals() to check whether they are logically equal.

Therefore, if we override equals() without overriding hashCode(), two logically equal objects may end up in different buckets, and collections like HashSet or HashMap may treat them as different objects.

That's why both methods must always be overridden together.

--------------------------------------------------------------------
--------------------------------------------------------------------
