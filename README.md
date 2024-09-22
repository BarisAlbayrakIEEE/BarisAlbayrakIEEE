# 1. Introduction

**Caution**\
I created this github page as a reference for my job applications.
The page presents some of my works written in C++, python and java.
Please consider this README file as an extension of my resume.

**Personal History**\
I started creating software programs in the beginning of 2000s during my undergraduate period with FORTRAN.
For a long time, I developed using structured languages: FORTRAN, PATRAN PCL, and Visual Basic.
Later, in 2016, I started studying OOP using Python.
I have developed a number of projects using python, java and C++ later in my professional life.
For the last two years, like many other software engineers, I have been studying FP from books and by inspecting public works of other people from github.
I already had a good background in template metaprogramming, hence, I did not have a big trouble during my studies.

An incident made a great effect on my vision for software engineering.
I implemented a sorting algorithm in 2000s for my PATRAN PCL libraries which was *quite fast* comparing to a traditioanl sorting algorithm based on comparison.
I was realy proud of that algorithm. One day, after a decade around 2017, I decided to make a review of the sorting algorithms other people generated.
I was shocked that my algorithm was one of the well known sorting algorithms named as *counting sort* and dated back to **1950s**.
Although I was disappointed, this event was a milestone for me such that I realized that **software engineering was not creating genius functions but its a science**.
Hence, I decided to study starting from the fundamentals and build up following the strong references.
During this *education period* sometimes I followed wrong paths especially at the beginning when I developed programs in python.
Later, I decided to switch to java but soon I understood that C++ was the correct language.
C++ is the closest language to the machine among commercial languages.

Two years ago, I had a similar incident. I created a solution for a problem related to one of my data structures and inspected its pros and cons.
Later, I made a survey that how other people treated to the problem I faced.
The result was not surprising for me this time that other developers has approached the problem exactly the same way.
Even, the solution was named as same as what I typed to google: *swap and pop idiom*.
I felt realy good that **my studies has rewarded me with a satisfactory level** in software engineering discipline.

The following sections summarize my software engineering background and experience.

# 2. Fundamentals of the Software Engineering

## 2.1. Software Design
- **Modularity:** A design solution is highly modular if the high cohesion/low coupling principle is satisfied among the modules.
- **Layered Design:** The modules are arranged in a hierarchy of layers forming a tree-like diagram.
- **Object-Oriented Design (OOD):** The system is viewed as being made up of a collection of objects.
- **Function-Oriented Design (FOD):** The design is decomposed into a set of interacting units where each unit has a clearly defined function.
- **Data-Oriented Design (DOD):** The design deals with the data by focusing on the data layout, acccess patterns and transformations.

There exist mainly two reasons that OOD should be supported by FOD and DOD:
- OOD approach, especially the pointer-based data structures, results with performance degrades due to the cache misses
- FOD and DOD provide methods that improve the pure concurrency in OOD caused by the state manipulation of objects of a complex class hierarchy.
DOD provides tools to improve the memory allocation and the cache effectivity.
Additionally, with DOD, its possible to implement the concurrency with lock-free approach more easily.
FOD utilizes persistency and activates concurrency without any cost by removing the shared state.

## 2.2. Abstraction
- **The crucial mistake:** Designing the software which represents the real-life problem as it is without designing structural or behavioral abstractions.
- **Two Types:** Data abstraction should be considered together with the process abstraction.
- **Factors:** Many issues such as the data structures and the concurrency should be evaluated.
- **Separation of concerns:** Dividing a complex system into distinct sections each dealing with a specific concern while following the single responsibility and interface segregation principles
- **Maintainability, flexibility and extendibility:** A must

Abstraction is at the center of software design.
The approaches/methods and the factors considered during the design affect the structure and functionality of the product.

For example, the resultant product would be different if FOD approach is preferred instead of OOD.
Similarly, a concurrent system would have a different structure than a single-threaded system.

**Abstraction in OOD**\
Many developers unfortunately apply OOD in the wrong way.
**The 1st crucial mistake while following OOD approach**, is to design a class as the exact copy of the real life object.
Consider the vectors and the points in geometry.
The geometric definition of a point is based on a vector.
So, the 1st choice for a point class is to delegate a vector or inherit from the vector class.
However, a vector has an invariant that at least one component should be non-zero which does not apply to a point.

The above point example inspects the **WHAT** question only.
Consider two other geometric entities: axis and line piece.
An axis is the set of points achieved by infinitely translating a point along a vector in both directions.
A line piece, on the other hand, excludes the points of the axis those are out of the two boundary points.
So, why not defining the line piece class by inheritting from the axis class?
Then, adding the two boundary points would finish the definition of the line piece.
Again, this looks like a good design solution based on the famous **IS A** and **HAS A** relations.
The above two examples do not consider the functionality (i.e. the behavior) of the objects at all.
For example, how to perform the intersection operations involving an axis or a line piece?
The above design would require four overloads for the intersection.
Even worst, the intersection operation for axis-line piece combination would require double dispatching which is not supported by C++.
Although, the strategy (or visitor) design pattern or double dispatch idiom could easily solve the double dispatch problem,
these kind of problems are the signs of a bad design practice.
This is **the 2nd crucial mistake** that the behavioral analysis is considered to be a part of FOD
and is forgotten/neglected during OOD.
If the developer has considered the behaviors of the two entities,
she would have realized that the line piece was a bounded geometry
and the bounded geometries had common properties under many geometric operations.
A line piece acts very similarly with a surface or a solid as they are all bounded geometries.
Similarly, an axis is similar with a circle or an ellipse while perforrming a translation.
Hence, the term boundary would have an important role in the design of a geometric library
together with other issues such as pivot/anchor or analytically definability.
As a result, the interface of a geometric library would start by defining the abstractions which simulate the boundaries, anchors, some analytical definitions (etc.)
considering the geometric operations such as transformations and intersection.

Another mistake in the above line piece class is the boundary points defined as members of the line piece.
The line piece objects are aware of the boundary points while the points are not aware of the line using them.
Again, an unexperienced developer would solve this issue by creating an abstract base class for all entities and storing the pointers to the entities using the object.
The boundary points store a shared pointer to the line piece object.
This approach looks enough to define the relations between the objects in our geometry library.
However, what we did is re-implementing an existing data structure: **directed acyclic graph (DAG)**.
A DAG can easily manage the ancestor and descendant relations in a geometry library.
Hence, we neither need to store the raw pointers to the boundary points in the line piece object nor the shared pointer to the line piece in the boundary point objects.

**Abstraction in FOD**\
FOD models a system by studying the functionality of the posible solutions to the problem.
Hence, the abstraction concentrates on the behaviors and encapsulates specific pieces of logic in functions.
The functions are organized hierarchically (e.g. higher level functions) which allows for layered abstraction.
Generic programming is at the center of FOD which allows decoupling the implementation of a logic from the target types.

The abstractions mentioned above (boundaries, anchors, some analytical definitions, etc) are obvious by FOD approach
as those are the common entities involved in the fundamental operations performed in a geometric application.

FP relies on the immutable data structures.
Hence, for the geometry application of the above example would use a persistent DAG
which would, by definition, eliminate the need to synchronize the shared data in a concurrent system.

The implementation of such a persistent DAG would require the techniques of DOD
in order to decorate the DAG with efficient solutions to the problems related to the memory allocation and transformation.

## 2.3. Programming Paradigms
I am well-experienced with the following programming paradigms and the corresponding languages accept for Clojure and Haskel
- **Structured programming:** C, C++, FORTRAN, PATRAN PCL, Visual Basic
- **Object-Oriented Programming, OOP:** C++, Python, Java, Visual Basic
- **Functional Programming, FP:** Clojure, Haskel, etc.

Please see [PersistentDAG](https://github.com/BarisAlbayrakIEEE/PersistentDAG) repository in my github page as an example of my FP background.

I had some earlier work on a geometry library which is currently a mixture of buggy code.
I will publish two libraries from this work:

- **GeometryLibrary_OCCT, C++03:** Relying on OCCT smart pointers (i.e., handles); will present the wrong designs covered in [Abstraction and Modeling](#2.2-Abstraction-and-Modeling)
- **GeometryLibrary_Modern, C++20:** A well-designed concurrent library; will present a concurrent modern geometry library.

Please see [github](https://github.com/BarisAlbayrakIEEE/cpp) repository for the above two.

## 2.4. Data Structures and Algorithms
- **Allocations:** Contiguous vs pointer-based, static (stack) vs dynamic (heap), sequence vs set
- **Basic data structures:** Static and dynamic arrays, linked lists, queues, stacks, trees, binary trees, red-black trees, sets, graphs, hash maps/tables, etc.
- **Persistent data structures:** Partial vs full vs functional persistency, persistent implementations of the basic data structures (e.g. persistent vector)
- **Iterator design pattern:** Iterator categories, traversal algorithms (e.g. BFS and DFS)
- **Problem-solving techniques:** Divide and conquer (recursion, thread pools or task parallelism), dynamic programming (caching)
- **Fundamental algorithms:** Insert, erase, traversal, sort, partition, etc.
- **Time and space complexity analysis:** Best and worst cases, amortized analysis
- **Concurrency:** Lock-based vs lock-free designs, fine vs coarse-grained locking schemes, persistency
- **DOD principles:** Better memory allocation (size and alignment studies), improved cache effectivity and increased capacity for lock-free concurrency

## 2.5. OOP Concepts
- **Basic concepts:** Abstraction, encapsulation, inheritance, delegation, polymorphism
- **Class vs object:** Declaration vs definition, instantiation vs initialization vs assignment
- **High cohesion, low coupling:** Fully orthogonal interfaces, dependency inversion
- **SOLID principles:** Fundamental rules for all design methodologies (OOD, FOD, DOD, flow-oriented design or else), maintainable/flexible/extendible systems
- **Design patterns:** GoF, structural and behavioral design patterns, dependency inversion, orthogonality, abstract base classes, runtime polymorphism, delegation
- **Mixin classes:** Usually templated, rarely introduces new data but new functionality, usually multiple mixins can be used together, layered application, orthogonality
- **Proxy classes:** Loki's approach, similar to mixins, templated inheritance, orthogonality
- **Dispatching:** Single dispatch (polymorphism) and double dispatch (C++ does not support, but can be implemented, sign of a bad design)
- **Memory management:** Handle body idiom, exclusive and shared ownership, stack and heap memories, RAII, C++ value categories
- **Stack vs heap memories:** Scope of an object, static vs dynamic containers, source ownership
- **Memory leaks and dangling pointers:** Pointer/reference invalidation, functions returning local variables, RAII, smart pointers
- **Generic programming:** Templated interfaces vs runtime polymorphism, template specialization vs virtual tables, template metaprogramming, type traits, concepts
- **Exception and thread safety:** Pure member functions, at least strong exception safety, preconditions and invariants, race conditions, RAII

The traditional software design composes complex class hierarchies obtained by applying the well-known design patterns.
The design patterns deal with encapsulating different logics (creation, structure, behavior or else) from the rest of the system and follow the SOLID principles.
The last one, dependency inversion, of the SOLID principles plays a central role in this configuration.
The dependencies are redirected by the interfaces, which reduces the coupling and results in orthogonal modules.
The traditional design is highly based on abstract base classes (or interfaces) and dynamic polymorphism.
However, since C++99, with the lead of Stroustrup, C++ has been introducing new tools with every new standard, replacing dynamic polymorphism with static definitions.
Currently, many design patterns can be implemented generically, maybe with some additional help from template metaprogramming.

## 2.6. Functional Programming (FP)
- **Immutability:** Functions keep the state unchanged, functions prefer passing by value
- **Purity:** Approaching the functions in math, functions lacking side effects
- **Function hierarchy:** Higher-level functions, partial functions, function composition, function lifting, currying
- **Laziness:** Lazy initialization, copy on write idiom, caching and memoization
- **Algebraic data types:** Sum (holding either type, e.g. std::variant) and product (holding all types, e.g. std::tuple)
- **Functors and monads:** Category theory, transformations, handling state
- **Persistent data structures:** Free exception safety, free concurrency, free history

[PersistentDAG](https://github.com/BarisAlbayrakIEEE/PersistentDAG) repository in my github page contains a persistent DAG data structure.
The README file of the repository presents a detailed discussion about the persistent data structures and concurrency.

## 2.7. Template Metaprogramming
Template metaprogramming helps removing a lot of boilerplate code.

C++ provides a compile-time (i.e., static) template definition,
while for other languages (e.g., Java), template definitions result in a class hierarchy
as all objects inherit from the language's base object (e.g., JavaObject).
Hence, the following issues are related mostly to C++:\
- Template specializations
- Template type deduction rules
- Traits and type manipulation
- Static type checking (better debugging and compile-time error detection)

## 2.8. Concurrency
- **Why:** Separation of concerns, task parallelism and data parallelism
- **Amdahl’s law:** Scalability
- **Race conditions:** Accessing shared data concurrently while at least one thread writes to the data, data race (undefined behavior)
- **Atomic operation:** Indivisible operation: You can’t observe such an operation half-done from any thread in the system; it’s either done or not done
- **Data structure classification:** Lock-based and lock-free concurrent data structures
- **Deadlocks:** Define a lock order, avoid nested locks, define lock hierarchy
- **Proccess relationship types:** Synchronizes-with and happens-before relationships
- **Modification ordering:** Sequentially consistent ordering, relaxed ordering, and acquire-release ordering
- **Serialization:** Threads access the data serially rather than concurrently (e.g., in case of a mutex lock)
- **Oversubscription:** More threads than the hardware can support
- **Contention:** If the processors rarely have to wait for each other, you have low contention
- **Cache ping-pong:** the data is passed back and forth between the caches many times (e.g. locking a mutex in a loop)
- **L1/L2/L3 caches:** Memory segments designed to speed up access
- **Cache line:** Blocks of memory dealt with by the processors (typically 32 or 64 bytes)
- **False sharing:** The cache line is shared, even though none of the data is shared
- **Data proximity:** If the data is spread out in memory, the related cache lines must be loaded from memory onto the processor cache

## 2.9. Rules for Concurrent Data Structures
- **Thread Safety:** Ensure that no thread can see a state where the invariants of the data structure have been broken by the actions of another thread
- **Exception Safety:** Pay attention to how the data structure behaves in the presence of exceptions to ensure that the invariants are not broken
- **Shared data:** Design without shared data or decide about how to secure the shared data (lock-based or lock-free)
- **Race conditions:** Avoid race conditions inherent in the interface by providing functions for complete operations (e.g., top_and_pop) rather than for operation steps (e.g., top, pop)
- **Deadlocks:** Minimize the opportunities for deadlocks by designing the data structure, the interface and locking scheme carefully and avoiding nested locks
- **Granularity:** Decide fine/coarse-grained locking (for lock-based approach)
- **Cache effectivity and false sharing:** Optimize the cache usage while avoiding the false sharing

[PersistentDAG](https://github.com/BarisAlbayrakIEEE/PersistentDAG) repository in my github page contains a concurrent DAG data structure.
The README file of the repository presents a detailed discussion about the above issues.

# 3. Languages & Tools
- C/C++, FORTRAN, PATRAN PCL, Java, Python, Visual Basic
- CMake
- git, TortoiseSVN
- Google Test
- MS Visual Studio, VS Code, Anaconda, Netbeans

# 4. C/C++ Skills
*SW:* Synchronizes-with\
*ITHB:* Inter-thread-happens-before\
*EBC:* Empty base class\
*NVI:* Non-virtual interface

- **Experience:** Long-term experience with C++99/03/11/14/17/20
- **OOP:** Abstract base class and virtual functions, dynamic polymorphism, single dispatch, RTTI, special/defaulted functions, memory management, etc.
- **C++11:** Evaluation of C++ with C++11 (move semantics, smart pointers, std::thread and concurrency, type traits, lambdas, etc.)
- **Keep up to date:** Current trend toward FP (virtual polymorphism to templated class families, template metaprogramming, value-based architecture, immutability, persistent data structures)
- **Libraries:** STL, boost, OpenCascade, gtest
- **C++ memory model and DOD:** Everything is an object, cache lines, atomic operations, concurrency
- **Value categories:** lvalue/rvalue/xvalue/glvalue/prvalue, universal references and perfect forwarding
- **Pointers and references:** Dynamic memory allocation, source ownership, handle body idiom, smart pointers, RAII, exception, thread safety, dangling pointers, memory leaks
- **STL algorithms:** Categories, unary/binary/ternary functions, implementation details, complexity analysis, function objects, and lambdas
- **Type deduction rules:** Template and auto type deductions, C++11/14/17 rules with auto and decltype, perfect forwarding
- **Idioms:** RAII, handle body idiom, copy and swap, swap and pop, lazy initialization, copy on write, EBC, double dispatch, SFINAE, CRTP, Pimpl, execute around pointer, NVI
- **Optimization techniques:** inlining, bit manipulation, bitwise copy, RVO and NRVO, loop unrolling, vectorization, etc.
- **Template metaprogramming:** Concepts, template specializations, template type deduction rules, traits and type manipulation, static type checking
- **Lambda expressions:** Anonymous functions, capture modes, capture auto type deduction rules, return type deduction rules, STL algorithms
- **Multithreading vs multitasking:** std::thread/std::jthread vs std::async, task parallelism vs data parallelism, hardware thread management, oversubscription and task switching
- **memory_order_seq_cst:** Sequentially consistent ordering: All threads see the same order of operations, obeys SW relationships, the default and the easiest one
- **memory_order_relaxed:** Relaxed ordering: Stores and loads are not synchronized, obeys happens-before relationships but does not obey SW relationships
- **memory_order_acquire-memory_order_release-memory_order_acq_rel:** Acquire-release ordering: One step synchronization over relaxed ordering, release operation SW/ITHB an acquire operation

# 5. Repositories
1. A concurrent persistent DAG in C++ [github](https://github.com/BarisAlbayrakIEEE/PersistentDAG)
2. Two geometry libraries in C++03 and C++20 **(buggy)** [github](https://github.com/BarisAlbayrakIEEE/cpp)
3. Some java projects [github](https://github.com/BarisAlbayrakIEEE/java)
4. Some python modules [github](https://github.com/BarisAlbayrakIEEE/python)

# 6. Some References
1. Alexandrescu, Modern C++ Design
2. Anthony Williams, C++ Concurrency in Action
3. Edouard Alligand & Joel Falcou, Practical C++ Metaprogramming
4. Loki [github](https://github.com/dutor/loki)
5. C++ concurrency library [github](https://github.com/David-Haim/concurrencpp)
6. Data oriented design resources [github](https://github.com/dbartolini/data-oriented-design)
7. Data-oriented design book source code [github](https://github.com/raspofabs/dodbooksourcecode)
8. DOD Performance Benchmarks [github](https://github.com/KamilVDono/DOD_Performance_Benchmarks)
9.  DOD optimizations [github](https://github.com/etuckerman/Data_Oriented_Design_Optimizations)
10. DOD vs OOD performance stats [github](https://github.com/jeuxdemains/DataOriented_vs_ObjectOriented)
11. Ivan Cukic, Functional Programming in C++
12. FP ebook [github](https://github.com/imteekay/functional-programming-learning-path)
13. Immer: A library of persistent and immutable data structures written in C++ [github](https://github.com/arximboldi/immer)
14. FP tutorials and articles [github](https://github.com/xgrommx/awesome-functional-programming)
15. List of materials and links about FP in C++ [github](https://github.com/graninas/cpp_functional_programming)
16. FP suggestions to reduce code noise and how to dealg with only one single level of abstraction at a time [github](https://github.com/Dobiasd/FunctionalPlus)
17. C++ persistent data structures [github](https://github.com/arximboldi/immer)
18. A C++ implementation of a immutable vector following Rich Hickey's clojure implementation [github](https://github.com/andrewrothstein/cpp-persistent-vector)
19. A fast and reliable persistent (immutable) vector class for C++ [github](https://github.com/marcusz/steady)
20. Phil Bagwell, Ideal Hash Tries
21. A hash array-mapped trie (HAMT) implementation in C99 [github](https://github.com/mkirchner/hamt)
22. C++ Template class implementation of Hash Array Mapped Trie [github](https://github.com/chaelim/HAMT)
23. C++ Template class implementation of Hash Array Mapped Trie [github](https://github.com/chaelim/HAMT)

# 7. Current Studies
1. Kernel development
- K. C. Wang; Systems Programming in Unix/Linux; 2017
- Robert Love; Linux Kernel Development; 2010
- P. Raghavan, Amol Lad and Sriram Neelakandan; Embedded Linux System Design and Development; 2006
- Mark Mitchell, Jeffrey Oldham and Alex Samuel; Advanced Linux Programming; 2001
2. Assembly language
- Randall Hyde; The Art of Assembly Language, 2010
- Randall Hyde; The Art of 64-bit Assembly, 2020
- Sivarama P. Dandamudi; Introduction to Assembly Language Programming; 2005
