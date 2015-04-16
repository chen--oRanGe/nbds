C implementations of several scalable non-blocking data structures for x86 and x86-64.


---


## Status ##
Overall the package is **pre-alpha**. It is still under development.

  * The skiplist is beta. There are no known bugs and it is feature complete.
  * The hashtable is alpha. It has not been tuned for memory usage. There are no known bugs and it is feature complete.
  * The lock-free memory management and runtime support is pre-alpha. It is not feature complete.
  * The transactional system is a toy implementation for now. Developers will find it mostly interesting for the concepts.

Tested under Linux with gcc 4.1-4.3 with Ubuntu 8.10. Probably works on Mac OS 10.5 with gcc 4.1-4.2.


---


## News ##
  * Version 0.4.3 - 4/7/09 - bug fix in hash table iterator. bug fix for OS X in memory manager. add performance tests to measure steady state behavior. major performance tuning for skiplist.
  * Version 0.4.2 - 1/18/09 - Linux support, gcc 4.1-4.3. Fixed major bug in skiplist. Memory manager re-write.
  * Version 0.4.1 - 12/16/08 - support for 32 bit x86. iterators for hashtable, list, and skiplist
  * Version 0.4.0 - 12/10/08 - lock-free transactional map
  * Version 0.3.2 - 12/3/08 - support for arbitrary key types, with a fast path for integer keys.
  * Version 0.3.1 - 11/29/08 - list and skiplist now support update operations and string type keys
  * Version 0.3.0 - 11/23/08 - lock-free skiplist
  * Version 0.2.1 - 11/15/08 - Started work on making the hash table transactional. Bug fixes too.
  * Version 0.2.0 - 11/07/08 - Initial public release


---

# What's Inside #
### Lock-Free Transactional Map ###
Lock-free transactional key-value store. The transactional semantics follow database-style _snapshot isolation_ using multi-version concurrency control.

With snapshot isolation updates are versioned. Transactions are isolated from changes after they begin. They always see a consistent view of the structure. Conversely, a transaction's updates are invisible to all other transactions until it commits. When a transaction tries to commit its writes are checked for conflicts against any committed concurrent transactions. If the system detects a conflict then the committing transaction rolls back. Otherwise its updates become visible to future transactions.

### Lock-Free Skiplist ###
The lock-free skiplist data structure created by Maurice Herlihy, Yossi Lev, and Nir Shavit. See Herlihy's and Shavit's book "The Art of Multiprocessor Programming" and Kir Fraser's dissertation "Practical Lock Freedom"

> http://www.amazon.com/Art-Multiprocessor-Programming-Maurice-Herlihy/dp/0123705916/

> http://www.cl.cam.ac.uk/techreports/UCAM-CL-TR-579.pdf

I've generalized the data structure to support update operations like set() and CAS() in addition to the normal add() and remove() operations, while preserving the lock-free property and linearizability.

### Lock-Free Hashtable ###
Cliff Click's lock-free hash table from

> http://www.azulsystems.com/events/javaone_2008/2008_CodingNonBlock.pdf

> http://sourceforge.net/projects/high-scale-lib


---


## License ##
All code in this project is public domain, except the unit test framework (which was not written by me). The hash function (murmur hash 2.0) is not written by me, but is public domain.


---


## Contact ##
Feel free to email me with comments or questions: jdybnis at gmail.