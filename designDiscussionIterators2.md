Title: Types of Iterators
TOC: yes
Author: Thomas J. Kennedy


# The Class Checklist Table

Let us revisit Cross-Language Class Checklist Table...

| C++                                   | Java                              | Python 3                     | Rust                       |
| :------------------------             | :------------------------------   | :---------------             | :----                      |
| Default Constructor                   | Default Constructor               | `__init__`                   | `new()` or Default trait   |
| Copy Constructor                      | Clone and/or Copy Constructor     | `__deepcopy__`               | Clone trait                |
| Destructor                            |                                   |                              |                            |
|                                       | finalize (deprecated/discouraged) | `__del__`                    | Drop trait                 |
| Assignment Operator (=)               |                                   |                              |                            |
| Accessors (Getters)                   | Accessors (Getters)               | Accessors (`@property`)      | Accessors (Getters)        |
| Mutators (Setters)                    | Mutators (Setters)                | Setter (`@attribute.setter`) | Mutators (setters)         |
| Swap                                  |                                   |                              |                            |
| Logical Equivalence Operator (==)     | equals                            | `__eq__`                     | std::cmp::PartialEq trait  |
| Less-Than / Comes-Before Operator (<) | hashCode                          | `__hash__`                   | std::cmp::PartialOrd trait |
| Stream Insertion Operator (<<)        | toString                          | `__str__`                    | std::fmt::Display trait    |
|                                       |                                   | `__repr__`                   | std::fmt::Debug trait      |
| `begin` and `end`                     | `iterator`                        | `__iter__`                   | `iter` and `iter_mut`      |

Let us remove the non-iterator focused rows...

| C++                       | Java                            | Python 3         | Rust                      |
| :------------------------ | :------------------------------ | :--------------- | :----                     |
| `begin` and `end`         | `iterator`                      | `__iter__`       | `iter()` and `iter_mut()` |

Now that we only have one row... we can *reorganize the table...*

| Language | Iterator Acquisition                |
| :---     | :---                                |
| C++      | `begin` and `end`                   |
| Java     | `iterator`                          |
| Python   | `__iter__`                          |
| Rust     | `iter` or `iter_mut` or `into_iter` |


# Types of Iterators

There are three (3) types of iterators...

  1. *Read Only* - This type of iterator allows the stored data to be
     accessed/retrieved but **not** changed.

  2. *Read and Write (Mutating)* - This type of iterator allows stored data to
     be both accessed and changed.

  3. *Consuming* - This type of iterator removes each piece of data from the
     original collection.

Let us add a new *Type* column to our iterator table.

| Iterator Type  | Language | Iterator Acquisition                            |
| :--            | :--      | :---                                            |
| Read Only      | C++      | `begin` and `end` or <br /> `cbegin` and `cend` |
| Read Only      | Java     | &ndash;                                         |
| Read Only      | Python   | &ndash;                                         |
| Read Only      | Rust     | `iter`                                          |
| Read and Write | C++      | `begin` and `end`                               |
| Read and Write | Java     | `iterator`                                      |
| Read and Write | Python   | `__iter__`                                      |
| Read and Write | Rust     | `iter_mut`                                      |
| Consuming      | C++      | &ndash;                                         |
| Consuming      | Java     | &ndash;                                         |
| Consuming      | Python   | &ndash;                                         |
| Consuming      | Rust     | `into_iter`                                     |

\bSidebar

**Note that we are focusing on iterators over collections.**

Topics such as Python
Generators, Java Streams, and C++ Ranges are not part of this discussion.

\eSidebar

Take note of how not every language provides every type of iterator.

Before we continue... let us remove the *"blank"*
entries.

| Iterator Type  | Language | Iterator Acquisition                            |
| :--            | :--      | :---                                            |
| Read Only      | C++      | `begin` and `end` or <br /> `cbegin` and `cend` |
| Read Only      | Rust     | `iter`                                          |
| Read and Write | C++      | `begin` and `end`                               |
| Read and Write | Java     | `iterator`                                      |
| Read and Write | Python   | `__iter__`                                      |
| Read and Write | Rust     | `iter_mut`                                      |
| Consuming      | Rust     | `into_iter`                                     |

We can now (a little more clearly) see that...

  - C++ and Rust both provide *Read Only* and *Read and Write* iterators
  - C++ iterators require both a `begin` and an `end` function instead of a
    single function. 
  - Java, Python, and Rust are similar in **how** an iterator is obtained.


# What About the Actual Iterators?

So far we have looked at the functions that are necessary to obtain iterators.
What about the interfaces of the iterators themselves?

| Operation                       | C++                                  | Java      | Python     | Rust   |
| :--                             | :--                                  | :--       | :--        | :--    |
| Increment                       | `operator++` and `operator++(int v)` | `next`    | `__next__` | `next` |
| Dereference                     | `operator*`                          | `next`    | `__next__` | `next` |
| Stop Condition (Boundary Check) | `operator!=` and/or `operator==`     | `hasNext` | `__next__` | `next` |

At the end of the day...

  - C++ iterators are the most tedious to implement.
  - Java iterators are the most straightforward to implement.
  - Python and Rust iterators have their `__next__` and `next` functions pull
    triple duty.
  - Python and Rust iterators use a form of exceptions in their boundary
    checks.


# How Do Iterators Compare?

Taking into account both how iterators are obtained and the iterator interface
in each language...

  - C++ iterators are most similar to Rust iterators.
  - Java iterators are most similar to Python iterators.
  - C++ iterators require the most *boilerplate code*.
