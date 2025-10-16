**Contents**
- [1. Introduction](#sec1)
- [2. Fundamentals of the Software Engineering](#sec2)
  - [2.1. Software Architecture & Design](#sec21)
  - [2.2. Abstraction, Encapsulation and Polymorphism](#sec22)
  - [2.3. Programming Paradigms](#sec23)
  - [2.4. Data Structures and Algorithms](#sec24)
  - [2.5. OOP](#sec25)
  - [2.6. Functional Programming (FP)](#sec26)
  - [2.7. Data Oriented Design (DOD)](#sec27)
  - [2.8. Template Metaprogramming](#sec28)
  - [2.9. Concurrency](#sec29)
- [3. Languages & Tools](#sec3)
- [4. C/C++ Skills](#sec4)
- [5. Repositories](#sec5)
- [6. Some References](#sec6)
- [7. Current Studies](#sec7)

**PREFACE**\
I created this github page as a reference for my job applications.
The page presents some of my works written in C++, python and java.
Please consider this README file as an extension to my resume.
Hence, here, I will try to **summarize** my knowledge and skills without falling into details.

# 1. Introduction <a id='sec1'></a>
The main approach in this README is to provide a description at the beginning of each heading followed by the categorized list of details.

I will skip basic issues (e.g. inheritance in OOP).
Yet, some topics (e.g. GoF design patterns or SOLID design rules) are only covered in the lists
without giving any detail because those are the fundamentals and obligatory for a software engineer.

Some aspects are considered significant and explained with formal statements
while some others are covered by a list of the related issues that I have full power such as the following:\
*memory leaks and dangling pointers:*\
*Ownership semantics, RAII, compiler-generated special functions and rule of 0/3/5/7, bugs in the special functions,*
*raw pointers and smart pointers,*
*pointer/reference invalidation, shallow copy and double delete, pointer to a moved-from object,*
*functions returning pointer/reference to a local variable,*
*unsecured shared data and race conditions.*

As a note, **the list of related issues** may describe various aspects of the topic.
In the above example, the causes (e.g. bugs in the special functions) and the cures (e.g. RAII) are listed together.
Thus, please, consider the lists as *the related issues* without expecting a conceptual completeness.

**Brief History**\
I started creating software programs in the beginning of 2000s during my undergraduate period with FORTRAN.
For a long time, I developed using structured languages: FORTRAN, PATRAN PCL and Visual Basic.
Later, in 2016, I started studying OOP using Python.
I have developed a number of projects using python, java and C++ later in my professional life.
For the last three years, like many other software engineers, I have been studying FP and DOD from books and by inspecting public works of other people from github.

**Two Incidents**\
An incident made a great effect on my vision for software engineering.
I implemented a sorting algorithm in 2000s for my PATRAN PCL libraries which was *quite fast* comparing to a *traditional sorting algorithm* based on comparison.
I was realy proud of that algorithm. One day, after a decade around 2017, I decided to make a review of the sorting algorithms *other people generated*.
I was shocked that my algorithm was one of the well known sorting algorithms named as *counting sort* and dated back to **1950s**.
Although I was disappointed, this event was a milestone for me to learn the software engineering starting from the fundamentals and following the strong references.

Two years ago, I had a similar incident.
I created a solution for a problem related to one of my data structures.
Later, I made a literature review.
The result was not surprising for me this time that the formal solution and even the name were exactly the same as I defined: *swap and pop idiom*.

**See**\
I have repositories for C++, Java and Python in order to provide a picture of this profile readme.
See [Repositories](#sec5) section to trace these repositories.
Following sections summarize my software engineering skills under the headings listed in the *Contents*.

# 2. Fundamentals of the Software Engineering <a id='sec2'></a>

## 2.1. Software Architecture & Design <a id='sec21'></a>
Several fundamental principles guide the development of a scalable, maintainable and efficient software:
Modularity, high cohesion, low coupling, separation of concerns, SOLID principles, testability, DRY, YAGNI, KISS, etc.

Most of the cases, the application of the above principles and guidelines yield a system which circulates around well-defined interfaces.
In other words, for complex systems, the software design is designing the interfaces which define the interaction of the components involved in the system.

Please see the [Structural Analysis Application](https://github.com/BarisAlbayrakIEEE/StructuralAnalysis.git) repository which
demonstrates my experience with the software architecture and design.

## 2.2. Abstraction, Encapsulation and Polymorphism <a id='sec22'></a>
These three concepts forms the basis of software engineering in all programming paradigms.

Similar to the math, any type in a software program abstracts and encapsulates the structure and behavior of a concept.
For example, integer data type abstracts the integer numbers in the number theory limited by lower and upper bounds.
A function is also an abstraction.
The abstraction, in summary, encapsulates (i.e. hides) some data and/or procedures and defines an interface which represents the encapsulated data and procedures.
For example, the `emplace_back` function of `std::vector`.
**Lets start with a simple definition:**\
`emplace_back` **abstracts the inplace construction of a new element in the dynamically allocated array.**

The signature of `emplace_back` corresponds to the following statements:
- The element is created in-place (as the name emplace suggests) instead of copying an already existing object into the container (as the name push_back suggests).
- The element is constructed at the end of the container.

**An experienced engineer would easily deduce the followings from the signature:**
- Its more efficient to work at the end of a `std::vector`.
- The size of the container is incremented.
- `emplace_back` may result with reallocation of the `std::vector` which means that all the pointers/references to the existing elements are invalidated.

**Hence, refining the 1st definition:**\
`emplace_back` **abstracts the in-place construction of a new element at the and of a dynamically allocated array for which the size is increased.**
Now, this process is encapsulated so that the user do not need to know the details like when and how the resize operation is needed and allocates the new memory.
Some of the details are described in the documentation of the method (e.g. possibility of the reference/pointer invalidation)
because not all users would be able to visualize the details of the algorithm.

Polymorphism is a fundamental concept that allows defining a uniform interface to a set of functions.
The uniformity can be achieved by other approaches/tools as well such as function overloading.
The keyword here is the **uniform interface** which is indispensable in the design of a system.
Single and double dispatch are the two types while double dispatch is not supported by C++ and its successors.
Function overloading has nothing to do with the polymorphism as a function is defined by its full signature including the name, arguments and return value
while the arguments are not the same for an overload function.

The term **uniform interface** is crucial such that all design patterns rely on interfaces.
For example, the strategy design pattern defines the signature of a behavior
while the implementation differs for each of the concrete classes.
Consider a Shape class which is the base for some geometric entities such as Circle and Ellipse.
The `void draw()` is the interface to draw a shape on the display window.
The function would be implemented differently in Circle and Ellipse
but the clients can easily call the function on all Shape objects including the Circle and Ellipse.

Polymorphism can be designed **statically** or **dynamically** in C++
while the languages like java and python are based on a universal abstract base type (e.g. JavaObject)
which does not allow polymorphism to be defined statically.
Static polymorphism is achieved by the tools coming from the generic programming such as template specializations and CRTP
while dynamic polymorphism is achieved by overriding virtaul functions of abstract base classes.
The differences between the two are described in the following sections.

## 2.3. Programming Paradigms <a id='sec23'></a>
I am well-experienced with the following programming paradigms and the corresponding languages accept for Clojure and Haskel:
- **Structured programming:** C, C++, FORTRAN, PATRAN PCL, Visual Basic
- **Object-Oriented Programming, OOP:** C++, Python, Java, Visual Basic
- **Functional Programming, FP:** C++, Clojure, Haskel, etc.

[VectorTree](https://github.com/BarisAlbayrakIEEE/VectorTree.git) repository in my github page contains a persistent vector tree data structure.
The README file of the repository presents a detailed discussion about the FP principles.

[PersistentDAG](https://github.com/BarisAlbayrakIEEE/PersistentDAG.git) repository in my github page contains a persistent DAG data structure.
The README file of the repository presents a detailed discussion about the FP and DOD principles.

## 2.4. Data Structures and Algorithms <a id='sec24'></a>
The complexity analysis was the main issue under this topic.
For example, inserting an element at the middle of a vector is O(N) while the same operation is O(1) for a linked list.
Hence, if one needs a container which will be subjected to frequent inserts, the correct answer would be a linked list.
However, **this is only the half of the reality** as the modern computers utilized the caches to improve the performance for memory access.

FP and DOD have been dominating the software development in especially performance critical applications.
Former tends to decrease the runtime load by increasing the purity while later optimizes the memory allocations and data access patterns.
At the end of the day, both rely on the same argument: **use almost always vector**.
FP searches for better vector designs (e.g. vector trie, vector tree, etc.) which covers the persistency as well.
DOD tries to maximize the benefit of the contiguous memory allocation of the vector (e.g. indices instead of pointers and struct of arrays instead of arrays of structs).

Another issue under this topic is of course the concurrency.
Current tendency in the industry is to achieve asynchronous tasking by replacing the lock-based systems with lock-free equivalents.
A further step is being achieved by the wait-free access which currently I have very little experience.

Below are the key points when data structures are considered:
- **Allocation:** Contiguous vs pointer-based, static (stack) vs dynamic (heap), sequence vs set, etc.
- **Basic data structures:** Static and dynamic arrays, linked lists, queues, stacks, trees, tries, binary trees, red-black trees, sets, graphs, hash maps/tables, etc.
- **Persistent data structures:** Partial vs full vs functional persistency, persistent implementations of the basic data structures (e.g. persistent vector)
- **Iterator design pattern:** Iterator categories, traversal algorithms (e.g. BFS and DFS)
- **Problem-solving techniques:** Divide and conquer (recursion, thread pools or task parallelism), dynamic programming (caching, memoization and laziness)
- **Fundamental algorithms:** Insert, erase, traversal, sort, partition, etc.
- **Time and space complexity analysis:** Best and worst cases, amortized analysis
- **Concurrency:** Lock-based vs lock-free designs, fine vs coarse-grained locking schemes, persistency
- **DOD principles:** Better memory allocation (size and alignment studies), improved cache effectivity and increased capacity for lock-free concurrency

## 2.5. OOP <a id='sec25'></a>
The traditional approach in OOP relies highly on the dynamic/virtual polymorphism.
Decades of software development based on the dynamic polymorphism gathered many design principles, patterns and idioms such as SOLID design rules, GoF design patterns, etc.
Currently, the approach has standard solutions to almost any problem.
The corresponding specifications provide a consensus and a common language among the developers
such that a code written by an engineer can easily be traced by another.

On the other hand, the dynamic polymorphism comes with a fall in the performance mainly due to three reasons:
- **Extra pointer indirection:** The virtual pointer table, vptr
- **Optimization loss:** The dynamic dispatch prevents the compiler making optimizations like inlining
- **Cache misses:** Containers need to store the pointers to the base class which prevents storing the objects contiguously.

In addition to the performance problems, virtual polymorphism has secondary issues in case of C++:
- virtual destructor terminates rule of zero which means steping to one of rule of 3/5/7
- need for a **polymorphic clone** member function
- endangers the definitions like EBC optimization, trivially copyability, etc.

**Static polymorphism provides solutions to all with the cost of longer compilation times and more complex code.**
However, some template metaprogramming methods would enable the type transformations to simplify the code.
Yet, the static polymorphism requires a design perspective in order to produce the expected results.
In other words, the transformation from a dynamically polymorphic system to a statically polymorphic system usually requires redesigning the whole system.
**The static solutions would work similar to the counterpart if the problem remains dynamic.**
For example, consider we have a container storing the std::variant objects
and the container is traversed to apply visitor pattern (std::visit) on each variant.
In this case, the variant would perform similar to a dynamic dispatch if the current type in the variant is resolved at runtime.
The compiler is not able to deduce the type at compile-time; so no optimization.
Even worst, the allocated memory would contain paddings if the types in the variant has varying sizes.
Lets consider the variant stores geometry objects like point and line.
The objects would associate to each other such as a line is formed by two points.
Hence, some classes have a number of members while others (e.g. point) does not.
We can have a member-wise uniform interface for all definitions by integrating a graph data structure
such that all elements aggregates a graph node to define the dependencies.
This would solve the third problem.
However, there is not an efficient solution to the 2nd one (i.e. optimizations).
It would require **linearizing the relations of the nonlinear graph structure**
which as far as I know cannot be implemented efficiently as such a solution would require an insert operation for every new element (i.e. no push_back).
So, each problem should be studied separately so that an optimum solution based on the requirements can be achieved.
In summary, **static polymorphism has full effect only when the compiler is supplied with all the informations it needs for the compilation.**

Below are the key points when OOP is considered:
- **Basic concepts:** Abstraction, encapsulation, inheritance, composition/association/aggregation, polymorphism
- **Class/object:** Declaration vs definition, instantiation vs initialization vs assignment
- **High cohesion, low coupling:** Toward fully orthogonal interfaces, dependency inversion
- **SOLID principles:** Fundamental rules for all design methodologies (OOD, FOD, DOD, flow-oriented design or else), maintainable/flexible/extendible systems
- **Design patterns:** GoF's 24, creational/structural/behavioral patterns, MVC, CRTP
- **Mixin classes:** Usually templated, rarely introduces new data but new functionality, usually multiple mixins can be used together, layered application, orthogonality
- **Proxy classes:** Loki's approach, similar to mixins, templated inheritance like CRTP, usually multiple inheritance, orthogonality
- **Dispatching:** Single dispatch (dynamic polymorphism in C++) and double dispatch (C++ does not support, but can be implemented, sign of a bad design)
- **Memory management:** RAII, C++ value categories, stack and heap memories, handle body idiom, exclusive and shared ownership,
memory leaks and dangling pointers, caches, DOD, etc.
- **Stack vs heap memories:** Scope of an object, static vs dynamic containers, source ownership
- **Memory leaks and dangling pointers:** Ownership semantics, RAII, compiler generated special functions and rule of 0/3/5/7,
bugs in the special functions, working with the raw pointers instead of the smart pointers,
pointer/reference invalidation, shallow copy and double delete, pointer to a moved from object,
functions returning pointer/reference to a local variable, unsecured shared data and race conditions
- **Generic programming:** Templated interfaces, template specializations, template metaprogramming, type traits, concepts
- **Exception and thread safety:** Pure member functions, at least strong exception safety, preconditions and invariants, race conditions, RAII

## 2.6. Functional Programming (FP) <a id='sec26'></a>
Although the FP languages (e.g. Haskell) are not widely used in the industry,
FP has influenced the industry by guiding the OOP with its principles.

Especially C++ community has been affected by this movement.
Every year, a couple of talks in [CppCon](https://www.youtube.com/@CppCon) are related to the applications of FP.
Actually, C++ had this tendency since the introduction of the templates.
STL algorithms have followed the higher order function concept of FP since they were first released.
Later, every new C++ standard has introduced new concepts from FP such as:
- lambdas (C++11)
- sum and product types like std::variant, std::tuple and std::optional (C++17)
- ranges and views (C++20), etc.

Now STL algorithms support the basic concepts of FP very well:
- first-class functions
- function composition
- lazy evaluation
- etc.

Below are the key points when FP is considered:
- **Immutability:** Functions keep the state unchanged, functions follow pass by value
- **Purity:** Toward the functions in math, functions lacking side effects
- **Functions as first class citizens:** Required to achieve a function hierarchy
- **Function hierarchy:** Higher-level functions, partial functions, function composition, function lifting, currying
- **Laziness:** Lazy initialization, copy on write idiom, caching and memoization
- **Algebraic data types:** Sum (holding either type, e.g. std::variant) and product (holding all types, e.g. std::tuple)
- **Functors and monads:** Category theory, transformations, handling state
- **Persistent data structures:** Free exception safety, free concurrency, free history

[VectorTree](https://github.com/BarisAlbayrakIEEE/VectorTree.git) repository in my github page contains a persistent vector tree data structure.
The README file of the repository presents a detailed discussion about the persistency.

[PersistentDAG](https://github.com/BarisAlbayrakIEEE/PersistentDAG.git) repository in my github page contains a persistent DAG data structure.
The README file of the repository presents a detailed discussion about the persistency and concurrency.

## 2.7. Data Oriented Design (DOD) <a id='sec27'></a>
In the last decade, the clock frequency of CPUs did not improved significantly
while the memory instructions did alot on behalf of the cache improvement (up to 100 times increase in cache size).
This evolution forces the developers to evaluate more efficient cache usage as a crucial design parameter.
Hence, the cache optimization is one of the hot topics in the industry.
For example, currently, almost half of the talks in [CppCon](https://www.youtube.com/@CppCon) contains at least one slide about the issue.
An interesting highlight from CppCon:
- The complexity analysis is useless(!) comparing to the cache efficiency
- **almost always use vector!**

Below are the key points when DOD is considered:
- **Focus:** How data is stored, accessed and transformed
- **Separate data from behavior:** Relies on data transformations as the behaviors are secondary while defining the types
- **Abstraction vs concrete:** As opposed to OOD, emphasis on the concrete data structures and access patterns
- **Memory:** Optimized memory accessed through L1/L2/L3 caches, design to access memory sequencially to minimize the cache misses
- **Locality:** Spatial (the data accessed together is stored close to each other) and temporal (frequently used data remains in the cache)
- **AoS vs SoA:** DOD prefers mostly **struct of arrays** as it is more efficient in terms of spatial locality
- **Optimization:** Avoid branching and dereferencing the pointers
- **Concurrency:** Design data for concurrency, design data for lock-free concurrency
- **Usage:** Especially in the game industry, HPC, finance

[PersistentDAG](https://github.com/BarisAlbayrakIEEE/PersistentDAG.git) repository in my github page contains a persistent DAG data structure.
The README file of the repository presents a detailed discussion about the DOD principles.

## 2.8. Template Metaprogramming <a id='sec28'></a>
Template metaprogramming helps removing a lot of boilerplate code.

C++ provides a compile-time (i.e., static) template definition,
while for other languages (e.g., Java), template definitions result in a class hierarchy
as all objects inherit from a universal base object (e.g., JavaObject).
Hence, the template metaprogramming is a branch related to C++.

Below are the key points when the template metaprogramming is considered:
- enable_if, void_t, SFINAE, if constexpr
- constexpr
- Type and value aliasing
- Compile-time recursion
- Variadic templates
- Template specializations
- Template type deduction rules
- Compile-time type and value determination
- Traits and type manipulation
- Static type checking (better debugging and compile-time error detection)
- Domain Specific Languages (DSLs)
- **STL:** constexpr, type traits library (enable_if/void_t, conditional, is_same, etc.), tuple, integer_sequence and index_sequence, etc.

## 2.9. Concurrency <a id='sec29'></a>
First of all, the performance is not the only reason for concurrent programming.
The need for the concurrent programming may arise to separate different concerns of an application.
For example, any application having a user interface would need to spare a thread for the GUI interaction.

The second use is the obvious one: to increase the performance of the application.
The are two approaches: data parallelism and task parallelism.
Data parallelism is straight forward: each thread executes the same operation on a different portion of the data.
Task parallelism, on the other hand, divides a single task into parts and run each in parallel.

Both approaches look straight forward but can be quite complex when there exist dependencies between the various parts of the data or the task.
One of the dependecies is the shared data.
Both data and task parallelism need to deal with the shared data in order to prevent the race conditions.
However, the best solution is to design without shared data.
For the task parallelism, the side effects are the second source of dependencies.
The side effects are signs of bad practice and should not exist in a concurrent code.

Lock-based, lock-free and wait-free strategies are the three ways of dealing with the shared data.
Despite its' easy use, lock-based concurrency has a number of drawbacks.
First of all, it does not guarantee that at least one thread makes progress (i.e. deadlocks).
Race conditions, deadlocks, serialization and cache ping-pong are some of the problems to be escaped in this case.

The lock-free approach, on the other hand, ensures at least one thread will make progress.
The atomic operations are indispensable so that a **true race condition** cannot occur in a lock-free data structure.
However, there are some related pitfalls with the lock-free data structures such as ABA problem, livelocks and memory issues like dangling pointers.

The wait-free approach is the most complex of the three approaches.
**While I am very confident in the lock-based and lock-free concurrencies, I have a little background about the wait-free approach.**
However, its one of the issues I currently study.
This approach is one of the mostly discussed topics in the last decade.
Studies and applications are quite alot related to the wait-free queues, stacks and even vectors (e.g. by Stroustrup et al.).

I mastered in the following fundamental strategies of multithreading:
- Master/worker
- Producer/consumer
- Divide and conquer
- Pipeline
- Futures and promises
- Partition vs elementwise parallellism
- Partition, reduction, etc.

I currently have no experience with the DAG scheduling strategy.
However, its one of the items in my future studies list.

I also have some experience with the GPU parallelism.
[GeneticLaminate](https://github.com/BarisAlbayrakIEEE/GeneticLaminate.git) repository in my github page contains a genetic algorithm 
to optimize a composite laminate written in CUDA C.
The README file of the repository presents a detailed discussion about data and task parallelism approaches and GPU parallelism using CUDA C.

Below are the key points when the concurrency is considered:
- **Why:** Separation of concerns, pereformance
- **Amdahl’s law:** Scalability
- **Race conditions:** Accessing shared data concurrently while at least one thread writes to the data; data race = undefined behavior
- **Atomic operation:** An indivisible operation which cannot be observed half-done from any thread in the system; it’s either done or not done
- **Data structure classification:** Lock-based, lock-free and wait-free concurrent data structures
- **Deadlocks:** Define a lock order, avoid nested locks, define lock hierarchy, **design for no deadlock**
- **Proccess relationship types:** Synchronizes-with and happens-before relationships
- **Modification ordering:** Sequentially consistent ordering, relaxed ordering and acquire-release ordering
- **Serialization:** Threads access the data serially rather than concurrently (e.g. in case of a mutex lock)
- **Oversubscription:** More threads than the hardware can support
- **Contention:** If the processors rarely have to wait for each other, you have low contention
- **Cache ping-pong:** The data is passed back and forth between the caches many times (e.g. locking a mutex in a loop)
- **L1/L2/L3 caches:** Memory segments designed to speed up access
- **Cache line:** Blocks of memory dealt by the processors (typically 32 or 64 bytes)
- **False sharing:** The cache line is shared, even though the data is not shared
- **Data proximity:** If the data is spread out in memory, the related cache lines must be loaded from memory onto the processor cache

**Rules for Concurrent Data Structures:**
- **Thread Safety:** Ensure that no thread can see a state where the invariants of the data structure have been broken by the actions of another thread
- **Exception Safety:** Pay attention to how the data structure behaves in the presence of exceptions to ensure that the invariants are not broken
- **Shared data:** Design without shared data as much as possible, otherwise decide about how to secure the shared data
- **Race conditions:** Avoid race conditions inherent in the interface by providing functions for complete operations (e.g., top_and_pop) rather than for operation steps (e.g., top, pop)
- **Deadlocks:** Minimize the opportunities for deadlocks by designing the data structure, the interface and locking scheme carefully and avoiding nested locks
- **Serialization:** If its worth design wait-free, otherwise lock-free, otherwise with fine-grained locks, otherwise consider redesigning
- **Granularity:** Achieve the deepest possible level of granularity in case of lock-based approach
- **Cache effectivity and false sharing:** Optimize the cache usage while avoiding the false sharing

[VectorTree](https://github.com/BarisAlbayrakIEEE/VectorTree.git) repository in my github page contains a persistent vector tree data structure.
The README file of the repository presents a detailed discussion about the relation between the persistency and the concurrency.

[PersistentDAG](https://github.com/BarisAlbayrakIEEE/PersistentDAG.git) repository in my github page contains a persistent DAG data structure.
The README file of the repository presents a detailed discussion about the above issues related to the concurrency.

[GeneticLaminate](https://github.com/BarisAlbayrakIEEE/GeneticLaminate.git) repository in my github page contains a genetic algorithm 
to optimize a composite laminate written in CUDA C.
The README file of the repository presents a detailed discussion about data and task parallelism approaches and GPU parallelism using CUDA C.

# 3. Languages & Tools <a id='sec3'></a>
- C/C++, FORTRAN, PATRAN PCL, Java, Python, Visual Basic
- CMake
- CUDA C
- SQL (MySQL)
- Linux shell
- git, gitlab, TortoiseSVN
- Google Test, Google benchmark
- MS Visual Studio, VS Code, Anaconda, Netbeans

# 4. C/C++ Skills <a id='sec4'></a>
*SW:* Synchronizes-with\
*ITHB:* Inter-thread-happens-before\
*EBC:* Empty base class\
*NVI:* Non-virtual interface

- **Experience:** Long-term experience with C++99/03/11/14/17/20
- **OOP:** Abstract base class and virtual functions, dynamic polymorphism, single dispatch, RTTI, special/defaulted functions, memory management, rule of 0/3/5/7, etc.
- **C++11:** Evaluation of C++ with C++11: Move semantics, smart pointers, concurrency (std::thread, std::mutex, std::atomic, etc.), type traits, lambdas, etc.
- **Keep up to date:** Current trend toward FP: Dynamic to static polymorphism, template metaprogramming, value semantics, immutability, persistent data structures, lazyness, etc.
- **Libraries:** STL, boost, CUDA C, gtest, Google Benchmark, OpenCascade
- **C++ memory model:** Everything is an object, cache lines, atomic operations, concurrency
- **Value categories:** lvalue/rvalue/xvalue/glvalue/prvalue, universal references and perfect forwarding, rvalue semantics, RVO and NRVO, pass by value vs pass by reference
- **Pointers and references:** Dynamic memory allocation, resource ownership, handle body idiom, smart pointers, RAII, exception, thread safety, dangling pointers, memory leaks, thread and exception safety
- **STL algorithms:** FP high level functions, pipes, ranges and views, categories, unary/binary/ternary functions, implementation details, complexity analysis, function objects and lambdas
- **Type deduction rules:** Template and auto type deductions, C++11/14/17 rules with auto and decltype, perfect forwarding
- **Idioms:** RAII, handle body idiom, copy and swap, swap and pop, lazy initialization, copy on write, EBC, double dispatch, SFINAE, CRTP, Pimpl, execute around pointer, NVI
- **Optimization techniques:** Inlining, bit manipulation, bitwise copy, RVO and NRVO, loop unrolling, vectorization, etc.
- **Template metaprogramming:** See [Template Metaprogramming](#sec28)
- **Lambda expressions:** Anonymous functions, capture modes, capture auto type deduction rules, return type deduction rules, STL algorithms
- **Multithreading vs multitasking:** std::thread/std::jthread vs std::async, std::atomic vs std::mutex, std::lock_guard vs std::scoped_lock vs std::unique_lock/std::shared_lock, std::condition_variable vs std::promise
- **memory_order_seq_cst:** Sequentially consistent ordering: All threads see the same order of operations, obeys SW relationships, the default and the easiest one
- **memory_order_relaxed:** Relaxed ordering: Stores and loads are not synchronized, obeys happens-before relationships but does not obey SW relationships
- **memory_order_acquire-memory_order_release-memory_order_acq_rel:** Acquire-release ordering: One step synchronization over relaxed ordering, release operation SW/ITHB an acquire operation

# 5. Repositories <a id='sec5'></a>
1. The architecture and design of an application for the structural aanalyses: [github](https://github.com/BarisAlbayrakIEEE/StructuralAnalysis.git)
2. A functionally persistent vector tree in C++: [github](https://github.com/BarisAlbayrakIEEE/VectorTree.git)
3. A functionally persistent DAG in C++: [github](https://github.com/BarisAlbayrakIEEE/PersistentDAG.git)
4. A genetic algorithm for composite laminate optimization in CUDA C: [github](https://github.com/BarisAlbayrakIEEE/GeneticLaminate.git)
5. Some python modules: [github](https://github.com/BarisAlbayrakIEEE/python.git)

# 6. Some References <a id='sec6'></a>
1. Alexandrescu, Modern C++ Design
2. Anthony Williams, C++ Concurrency in Action
3. Edouard Alligand & Joel Falcou, Practical C++ Metaprogramming
4. Loki [github](https://github.com/dutor/loki)
5. C++ concurrency library [github](https://github.com/David-Haim/concurrencpp)
6. Data-oriented design resources [github](https://github.com/dbartolini/data-oriented-design)
7. Data-oriented design book source code [github](https://github.com/raspofabs/dodbooksourcecode)
8. DOD Performance Benchmarks [github](https://github.com/KamilVDono/DOD_Performance_Benchmarks)
9.  DOD optimizations [github](https://github.com/etuckerman/Data_Oriented_Design_Optimizations)
10. DOD vs OOD performance stats [github](https://github.com/jeuxdemains/DataOriented_vs_ObjectOriented)
11. Ivan Cukic, Functional Programming in C++
12. FP ebook [github](https://github.com/imteekay/functional-programming-learning-path)
13. Immer: A library of persistent and immutable data structures written in C++ [github](https://github.com/arximboldi/immer)
14. FP tutorials and articles [github](https://github.com/xgrommx/awesome-functional-programming)
15. List of materials and links about FP in C++ [github](https://github.com/graninas/cpp_functional_programming)
16. FP suggestions to reduce code noise and how to deal with only one single level of abstraction at a time [github](https://github.com/Dobiasd/FunctionalPlus)
17. C++ persistent data structures [github](https://github.com/arximboldi/immer)
18. A C++ implementation of an immutable vector following Rich Hickey's clojure implementation [github](https://github.com/andrewrothstein/cpp-persistent-vector)
19. A fast and reliable persistent (immutable) vector class for C++ [github](https://github.com/marcusz/steady)
20. Phil Bagwell, Ideal Hash Tries
21. A hash array-mapped trie (HAMT) implementation in C99 [github](https://github.com/mkirchner/hamt)
22. C++ Template class implementation of Hash Array Mapped Trie [github](https://github.com/chaelim/HAMT)

# 7. Current Studies <a id='sec7'></a>
1. Socket programming
- Brian (Beej Jorgensen) Hall; Beej’s Guide to Network Programming (C); 2020
- Michael J. Donahoo & Kenneth L. Calvert; TCP-IP Sockets in C; 2009
- Gay W. Warren; Linux Socket Programming by Example; 2000
- W. Richard Stevens; UNIX Network Programming; 1990
2. Lock-free and wait-free programming papers and code reviews
- Lock-free dynamically resizable arrays, Stroustrup et al.
- A collection of resources on wait-free and lock-free programming [github](https://github.com/rigtorp/awesome-lockfree.git)
- Wait-free data structure for single-writer/multi-reader [github](https://github.com/gnu-enjoyer/LeftWrite.git)
- Library of lock-free and wait-free algorithms [github](https://github.com/hayabusa-cloud/concurrent.git)
- Single header, wait-free queues for C++ [github](https://github.com/marcusspangenberg/waitfreequeue.git)
- ...
3. Kernel development
- K. C. Wang; Systems Programming in Unix/Linux; 2017
- Robert Love; Linux Kernel Development; 2010
- P. Raghavan, Amol Lad and Sriram Neelakandan; Embedded Linux System Design and Development; 2006
- Mark Mitchell, Jeffrey Oldham and Alex Samuel; Advanced Linux Programming; 2001
4. Assembly language
- Randall Hyde; The Art of Assembly Language, 2010
- Randall Hyde; The Art of 64-bit Assembly, 2020
- Sivarama P. Dandamudi; Introduction to Assembly Language Programming; 2005
