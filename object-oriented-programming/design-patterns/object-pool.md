---
title: "Object Pool Design Pattern in PHP"
updated: "September 20, 2016"
permalink: "/articles/object-oriented-programming/design-patterns/object-pool/"
redirect_from: "/faq/object-oriented-programming/design-patterns/object-pool/"
---

Object pool pattern is a software creational design pattern which is used in
situations where the cost of initializing a class instance is high. It can offer
a significant performance boost.

![Object Pool Design Pattern UML](/_images/object-oriented-programming/design-patterns/object-pool.png "Object Pool Design Pattern")

Object pool (resource pool) manages instantiated classes. Client code has access
to the pool and can then use it to avoid creating new objects by going through
the pool to find the one that has already been instantiated. When the pool is
empty it will create new objects. Depending on the wanted implementation and
functionality the pool can be also set to limit the number of instantiated
classes.

## PHP Example of Object Pool

```php
<?php

class ObjectPool
{
    /** @var array Instances of reusable objects */
    private $instances = [];

    /**
     * Get object from instances.
     *
     * @param string $key Key for retrieving the instance.
     *
     * @return ReusableObject
     */
    public function get($key)
    {
        return $this->instances[$key];
    }

    /**
     * Add object to list of instances.
     *
     * @param ReusableObject
     */
     public function add($object, $key)
     {
         $this->instances[$key] = $object;
     }
}

class ReusableObject
{
    /**
     * Do something.
     */
    public function doSomething()
    {
        // ...
    }
}

// Client code
$pool = new ObjectPool();
$reusableObject = new ReusableObject();
$pool->add($reusableObject, 'reusable_object_key')

$reusableObject = $pool->get('reusable_object_key');
$reusableObject->doSomething();
```

## More Practical Examples

Practical example can be also a managing a conference with call for papers. When
the call for paper is issued, speakers propose their talks and the managers
decide which speakers to invite. Speakers get assigned to talk sessions. If a
speaker cancels the talk, the talk session becomes available for the next speaker.

Most of the time keep all reusable objects that are not currently in use in the
same object pool so that they can be managed by one coherent policy. To achieve
this, the reusable pool class is designed to be a singleton class.

## Discussion

Object pool allows clients to "check out" objects from the pool, when those objects
are no longer needed by the client processes, they are returned to the pool in
order to be reused.

However, we don't want a process to have to wait for a particular object to be
released, so the object pool also instantiates new objects as they are required,
but must also implement a facility to clean up unused objects periodically.

## Structure

The general idea for the connection pool pattern is that if instances of a class
can be reused, you avoid creating instances of the class by reusing them.

* Reusable - instances of classes in this role collaborate with other objects for
  a limited amount of time, then they are no longer needed for that collaboration.
* Client - instances of classes in this role use Reusable objects.
* ReusablePool - instances of classes in this role manage Reusable objects for
  use by Client objects. Usually, it is desirable to keep all Reusable objects
  that are not currently in use in the same object pool so that they can be managed
  by one coherent policy. To achieve this, the ReusablePool class is designed to
  be a singleton class. Its constructor(s) are private, which forces other classes
  to call its getInstance method to get the one instance of the ReusablePool
  class.

A Client object calls a ReusablePool object's acquireReusable method when it needs
a Reusable object. A ReusablePool object maintains a collection of Reusable
objects. It uses the collection of Reusable objects to contain a pool of
Reusable objects that are not currently in use.

If there are any Reusable objects in the pool when the acquireReusable method is
called, it removes a Reusable object from the pool and returns it. If the pool
is empty, then the acquireReusable method creates a Reusable object if it can.
If the acquireReusable method cannot create a new Reusable object, then it waits
until a Reusable object is returned to the collection.

Client objects pass a Reusable object to a ReusablePool object's releaseReusable
method when they are finished with the object. The releaseReusable method returns
a Reusable object to the pool of Reusable objects that are not in use.

In many applications of the Object Pool pattern, there are reasons for limiting
the total number of Reusable objects that may exist. In such cases, the
ReusablePool object that creates Reusable objects is responsible for not creating
more than a specified maximum number of Reusable objects. If ReusablePool objects
are responsible for limiting the number of objects they will create, then the
ReusablePool class will have a method for specifying the maximum number of objects
to be created. That method is indicated in the above diagram as setMaxPoolSize.

## Rules

* The Factory Method pattern can be used to encapsulate the creation logic for
  objects. However, it does not manage them after their creation, the object pool
  pattern keeps track of the objects it creates.
* Object Pools are usually implemented as Singletons.

## Open Source PHP Implementations

* [Pool in pthreads](http://php.net/manual/en/class.pool.php)
* [PSR-6](http://www.php-fig.org/psr/psr-6/) compatible cache libraries

[Dependency injection container](/faq/object-oriented-programming/dependency-injection-container/)
can also use object pool together with some other design patterns.

## See Also

* [Wikipedia: Object pool pattern](https://en.wikipedia.org/wiki/Object_pool_pattern)
* [DesignPatternsPHP: Pool](http://designpatternsphp.readthedocs.io/en/latest/Creational/Pool/README.html)
