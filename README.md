# 1. Introduction
I created this github page in order to give a reference in my job applications.
Please consider this README file as an extension of my resume.

This github page presents some of my works written in C++, python and java.

The following sections summarizes my software engineering background and experience.

# 2. Fundamentals of the Software Engineering

## 2.1. Software Design
- **Modularity:** A design solution is highly modular if the high cohesion/low coupling principle is satisfied among the modules.
- **Layered Design:** The modules are arranged in a hierarchy of layers forming a tree-like diagram.
- **Function-Oriented Design:** The design is decomposed into a set of interacting units where each unit has a clearly defined function.
- **Object-Oriented Design:** The system is viewed as being made up of a collection of objects.

## 2.2. Abstraction and Modeling
- **The biggest mistake:** Designing the software which represents the real-life problem as it is without designing structural or behavioral abstractions.
- **Two Types:** Data abstraction should be considered together with the process abstraction.
- **Factors:** Many issues such as the data structures and the concurrency should be evaluated:
- Separation of concerns
- Maintainability and extendibility

Abstraction is at the center of software design.
The approaches/methods and the factors considered during the design affect the structure and functionality of the product.

For example, the resultant product would be different if the function-oriented approach is preferred over the object-oriented approach.
Similarly, a concurrent system would have a different structure than a single-threaded system.

Most beginner developers think that OOP is the best solution for every problem.
Besides, many developers unfortunately apply OOP in the wrong way.
One of the biggest mistakes, in this respect, is to design a class as the exact copy of the real life object.
Consider the vectors and the points in geometry.
The geometric definition of a point is based on a vector.
So, the 1st choice for a point class is to put a vector in the point class as a member or inherit the point from the vector class.
However, a vector has an invariant that at least one component should be non-zero which does not apply to a point.

The above point example inspects the **WHAT** question only.
Consider two other geometric entities: axis and line piece.
An axis is the set of points achieved by infinitely translating a point along a vector in both directions.
A line piece, on the other hand, excludes the points of the axis those are out of the two boundary points.
So, why not defining the line piece class by inheritting from the axis class?
Then, adding the two boundary points would finish the definition of the line piece.
Again, this looks like a good design solution based on the famous **IS A** relation.
The above two examples do not consider the functionality (i.e. the behavior) of the objects at all.
For example, how to perform the intersection operations involving an axis or a line piece?
The above design would require four overloads for the intersection.
Even worst, the intersection operation for axis-line piece combination would require double dispatching which is not supported by C++.
Although, the strategy (or visitor) design pattern or double dispatch idiom could easily solve the problem,
these kind of problems are the sign of a bad design practice.
This is the 2nd biggest mistake that the behavioral analysis is considered to be belonging to the function-oriented approach
and is forgotten/neglected during the object-oriented approach.
If the developer has considered the behaviors of the two entities,
she would have realized that the line piece is a bounded geometry
and the bounded geometries have common properties under many geometric operations.
A line piece acts very similarly with a surface or a solid as they are all bounded geometries.
Similarly, an axis is similar with a circle or an ellipse while perforrming a translation.
Hence, the term boundary would have an important role in the design of a geometric library
together with other issues such as pivot/anchor or analytically definability.
As a result, the interface of a geometric library would start by defining the abstractions which simulate the boundaries, anchors and some analytical definitions
considering the geometric operations such as transformations and intersection.

Another mistake in the above line piece class is the boundary points defined as members of the line piece.
The line piece objects are aware of the boundary points while the points are not aware of the line using them.
Again, an unexperienced developer would solve this issue by creating an abstract base class for all entities and storing the pointers to the entities using the object.
The boundary points store a shared pointer to the line piece object.
This approach looks enough to define the relations between the objects in our geometry library.
However, what we did is re-implementing an existing data structure: directed acyclic graph (DAG).
A DAG can easily manage the ancestor and descendant relations in a geometry library.
Hence, we neither need to store the raw pointers to the boundary points in the line piece object nor the shared pointer to the line piece in the boundary point objects.

Finally, by managing the geometric objects by the help of a DAG structure, the concurrency can be applied to the application very easily.
Actually, after having a multithreaded DAG, not much remains.

## 2.3. Programming Paradigms
- Structured programming (C, C++, FORTRAN, PATRAN PCL)
- Object-Oriented Programming, OOP (C++, Python, Java, Visual Basic)
- Functional Programming, FP (purity, higher-level functions, ranges, monads, template metaprogramming, currying)

**Personal Background**

I started creating software programs in the beginning of 2000s during my undergraduate period with FORTRAN.
For a long time, I developed using structured languages: FORTRAN, PATRAN PCL, and Visual Basic.
Later, in 2016, I started studying OOP using Python.
I have developed a number of projects using python, java and C++ later in my professional life.
For the last two years, like many other software engineers, I have been studying FP from books and by inspecting public works of other people from GitHub.
I already had a good background in template metaprogramming, hence, I did not have a big trouble during my studies.

Please see [PersistentDAG](https://github.com/BarisAlbayrakIEEE/PersistentDAG) repository in my GitHub page as an example of my FP background.

I had some earlier work on a geometry library which is currently not a structured mixture.
I will publish two libraries from this work:

- *GeometryLibrary_OCCT:* C++03 relying on OCCT smart pointers (i.e., handles): Presents the wrong designs covered in [Abstraction and Modeling](#2.2-Abstraction-and-Modeling)
- *GeometryLibrary_Modern:* C++20: A well-designed concurrent library

Please see [Geometry Library](https://github.com/BarisAlbayrakIEEE/cpp) repository in my GitHub page for my skills in OOP and FP.

## 2.4. Data Structures and Algorithms
- Memory management
- All basic data structures (static and dynamic arrays, linked lists, queues, stacks, trees, binary trees, red-black trees, sets, graphs, hash maps/tables, etc.)
- Persistent data structures (partial, full, and functional)
- Multithreading (lock-based and lock-free design, fine and coarse-grained locking)
- Iterator design pattern (iterator categories, traversal algorithms like BFS and DFS)
- Problem-solving techniques: divide and conquer (recursion, thread pools or task parallelism), dynamic programming (caching)
- Fundamental algorithms for any container (insert, erase, traversal, sort, partition, etc.)
- Time and space complexity analysis (best and worst cases, amortized analysis)

## 2.5. OOP Concepts
- Basic concepts (abstraction, encapsulation, inheritance, delegation, polymorphism)
- High cohesion, low coupling (fully orthogonal interfaces, dependency inversion)
- SOLID principles
- Design patterns (GoF, structural and behavioral design patterns, dependency inversion, orthogonality, abstract base classes, runtime polymorphism, delegation)
- Single dispatch (polymorphism) and double dispatch (C++ does not support, but can be implemented, sign of a bad design)
- Memory management (handle body idiom, exclusive and shared ownership, stack and heap memories, RAII, C++ value categories)
- Stack memory vs heap memory (scope of an object, static vs dynamic containers, source ownership)
- Memory leaks and dangling pointers (pointer/reference invalidation, functions returning local variables, RAII, smart pointers)
- Generic programming (templated interfaces vs runtime polymorphism, template specialization vs virtual tables, template metaprogramming, type traits, concepts)
- Declaration vs definition, instantiation vs initialization vs assignment
- Exception and thread safety (pure member functions, at least strong exception safety, preconditions and invariants, race conditions, RAII)

The traditional software design relies heavily on dynamic polymorphism and encapsulation based on SOLID principles and design patterns.
The dependency inversion principle plays a central role in this configuration.
The dependencies are redirected by the interfaces, which terminates the coupling and results in orthogonal modules.
This methodology is highly based on abstract base classes (or interfaces) and dynamic polymorphism.
However, since C++99, with the lead of Stroustrup, C++ has been introducing new tools with every new standard, replacing dynamic polymorphism with static definitions.
Currently, many design patterns can be implemented generically, maybe with some additional help from template metaprogramming.

## 2.6. Functional Programming (FP)
- Immutable state and purity (functions lack side effects)
- Higher-level functions (partial functions, function composition, function lifting, currying)
- Laziness (lazy initialization, copy on write idiom, memoization)
- Functors and monads (category theory, transformations, handling state)
- Persistent data structures (free exception safety, free concurrency, free history)

[PersistentDAG](https://github.com/BarisAlbayrakIEEE/PersistentDAG) repository in my GitHub page contains a persistent DAG data structure.
The README file of the repository presents a detailed discussion about the persistent data structures.

## 2.7. Template Metaprogramming
C++ provides a compile-time (i.e., static) template definition,
while for other languages (e.g., Java), template definitions result in a class hierarchy
as all objects inherit from the language's base object (e.g., JavaObject).
Hence, the following issues are related mostly to C++:
- Template specializations
- Template type deduction rules
- Traits and type manipulation
- Static type checking (better debugging and compile-time error detection)
- Removes a lot of boilerplate code

## 2.8. Concurrency
- Separation of concerns, task parallelism, and data parallelism
- Oversubscription (more threads than the hardware can support)
- Scalability and Amdahl’s law
- Race condition and data race (undefined behavior)
- Atomic operation (indivisible operation: You can’t observe such an operation half-done from any thread in the system; it’s either done or not done)
- Lock-based programming and mutex (mutual exclusion)
- Lock-based and lock-free concurrent data structures
- Deadlocks (define a lock order, avoid nested locks, define lock hierarchy)
- Synchronizes-with and happens-before relationships
- Modification ordering: sequentially consistent ordering, relaxed ordering, and acquire-release ordering
- Serialization: threads access the data serially rather than concurrently (e.g., in case of a mutex lock)
- High contention: If the processors rarely have to wait for each other, you have low contention
- Cache line: blocks of memory dealt with by the processors (typically 32 or 64 bytes)
- False sharing: The cache line is shared, even though none of the data is shared
- Data proximity: if the data is spread out in memory, the related cache lines must be loaded from memory onto the processor cache

## 2.9. Rules for Concurrent Data Structures
- Decide fine/coarse-grained locking (lock-based approach)
- Ensure that no thread can see a state where the invariants of the data structure have been broken by the actions of another thread
- Avoid race conditions inherent in the interface by providing functions for complete operations (e.g., top_and_pop) rather than for operation steps (e.g., top, pop)
- Pay attention to how the data structure behaves in the presence of exceptions to ensure that the invariants are not broken
- Minimize the opportunities for deadlocks by avoiding nested locks
- Optimize the cache usage while avoiding the false sharing

[PersistentDAG](https://github.com/BarisAlbayrakIEEE/PersistentDAG) repository in my GitHub page contains a concurrent DAG data structure.
The README file of the repository presents a detailed discussion about the above issues.

# 3. Languages & Tools
- C/C++, FORTRAN, PATRAN PCL, Java, Python, Visual Basic
- CMake
- git, TortoiseSVN
- Google Test
- MS Visual Studio, VS Code, Anaconda, Netbeans

# 4. C/C++ Skills
SW: Synchronizes-with
ITHB: Inter-thread-happens-before
EBC: Empty base class
NVI: Non-virtual interface
- Long-term experience with C++99/03/11/14/17/20
- OOP basics (abstract base class and virtual functions, dynamic polymorphism, single dispatch, RTTI, special/defaulted functions, memory management, etc.)
- Evaluation of C++ with C++11 (move semantics, smart pointers, std::thread and concurrency, type traits, lambdas, etc.)
- Current trend toward FP (virtual polymorphism to templated class families, template metaprogramming, value-based architecture, immutability, persistent data structures)
- C++ memory model (everything is an object), cache lines, atomic operations, concurrency
- C++ value categories (lvalue/rvalue/xvalue/glvalue/prvalue)
- Pointers and references (dynamic memory allocation, source ownership, handle body idiom, smart pointers, RAII, exception, thread safety, dangling pointers, memory leaks)
- STL algorithms (categories, implementation details, complexity analysis, function objects, and lambdas)
- Type deduction rules (template and auto type deductions, C++11/14/17 rules with auto and decltype, perfect forwarding)
- C++ idioms (RAII, handle body idiom, copy and swap, swap and pop, lazy initialization, copy on write, EBC, double dispatch, SFINAE, CRTP, Pimpl, execute around pointer, NVI)
- Optimization techniques (inlining, bit manipulation, bitwise copy, RVO and NRVO, loop unrolling, vectorization, etc.)
- Lambda expressions (capture modes, auto and type deduction rules)
- Multithreading vs multitasking (std::thread/std::jthread vs std::async, task parallelism vs data parallelism, hardware thread management, oversubscription, and task switching)
- memory_order_seq_cst: Sequentially consistent ordering; all threads see the same order of operations, obeys SW relationships, the default and the easiest one
- memory_order_relaxed: Relaxed ordering; stores and loads are not synchronized, obeys happens-before relationships but does not obey SW relationships
- memory_order_acquire-memory_order_release-memory_order_acq_rel: Acquire-release ordering; one step synchronization over relaxed ordering, release operation SW/ITHB an acquire operation
- Template metaprogramming: Concepts, template specializations, template type deduction rules, traits, and type manipulation, static type checking
