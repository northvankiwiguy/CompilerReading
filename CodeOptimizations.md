# Code Optimization Techniques

#### PLDI Most Influential Paper - [Profile guided code positioning]( https://dl.acm.org/citation.cfm?id=93550&coll=portal&dl=ACM), by Karl Pettis and Robert C Hansen, 1990.

This paper presents the results of our investigation of code positioning techniques using execution profile data as input into the compilation process. The primary objective of the positioning is to reduce the overhead of the instruction memory hierarchy. After initial investigation in the literature, we decided to implement two prototypes for the Hewlett-Packard Precision Architecture (PA-RISC). The first, built on top of the linker, positions code based on whole procedures. This prototype has the ability to move procedures into an order that is determined by a “closest is best” strategy. The second prototype, built on top of an existing optimizer package, positions code based on basic blocks within procedures. Groups of basic blocks that would be better as straight-line sequences are identified as chains. These chains are then ordered according to branch heuristics. Code that is never executed during the data collection runs can be physically separated from the primary code of a procedure by a technique we devised called procedure splitting. The algorithms we implemented are described through examples in this paper. The performance improvements from our work are also summarized in various tables and charts.

#### [Memento mori: dynamic allocation-site-based optimizations]( https://dl.acm.org/citation.cfm?id=2754181), by Daniel Clifford, Hannes Payer, Michael Stanton, Ben Titzer.

Languages that lack static typing are ubiquitous in the world of mobile and web applications. The rapid rise of larger applications like interactive web GUIs, games, and cryptography presents a new range of implementation challenges for modern virtual machines to close the performance gap between typed and untyped languages. While all languages can benefit from efficient automatic memory management, languages like JavaScript present extra thrill with innocent-looking but difficult features like dynamically-sized arrays, deletable properties, and prototypes. Optimizing such languages requires complex dynamic techniques with more radical object layout strategies such as dynamically evolving representations for arrays. This paper presents a general approach for gathering temporal allocation site feedback that tackles both the general problem of object lifetime estimation and improves optimization of these problematic language features. We introduce a new implementation technique where allocation mementos processed by the garbage collector and runtime system efficiently tie objects back to allocation sites in the program and dynamically estimate object lifetime, representation, and size to inform three optimizations: pretenuring, pretransitioning, and presizing. Unlike previous work on pretenuring, our system utilizes allocation mementos to achieve fully dynamic allocation-site-based pretenuring in a production system. We implement all of our techniques in V8, a high performance virtual machine for JavaScript, and demonstrate solid performance improvements across a range of benchmarks.

#### [What's up with monomorphism?]( https://mrale.ph/blog/2015/01/11/whats-up-with-monomorphism.html), by Vyacheslav Egorov.

Excellent discussion about Monomorphism, Polymorphism, and Megamorphism for Inline Caching (IC) in the V8 JavaScript engine. Gives lots of examples with diagrams and code samples.

#### [Garbage Collection as a Joint Venture] ( https://dl.acm.org/citation.cfm?id=332, by Ulan Degenbaev, Michael Lippautz, Hannes Payer.

Describes the implementation of "Cross-Component Garbage Collection" as used by V8 and Blink which hold references to each other's data structures. Therefore, garbage collection
must cleverly avoid creating islands due to each component holding lingering references to the other component's objects.

#### PLDI 2019 [Accelerating Sequential Consistency for Java with Speculative Compilation]( https://dl.acm.org/citation.cfm?id=3314611) by Lun Liu, Todd Millstein, Madanlal Musuvathi

Describes a modified Java HotSpot compiler that generates VBD (Volatile By Default) code to help with concurrent access to data in different threads. The optimize performance, they assume that all data is thread-safe, but also identify which classes of objects are accessed from multiple threads, then deoptimize those methods and field access to add memory barriers.

