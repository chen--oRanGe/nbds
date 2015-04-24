# nbds
non-blocking hash table, lock-free skiplist and other non-blocking data structures

Lock-Free Transactional Map
Lock-free transactional key-value store. The transactional semantics follow database-style snapshot isolation using multi-version concurrency control.

With snapshot isolation updates are versioned. Transactions are isolated from changes after they begin. They always see a consistent view of the structure. Conversely, a transaction's updates are invisible to all other transactions until it commits. When a transaction tries to commit its writes are checked for conflicts against any committed concurrent transactions. If the system detects a conflict then the committing transaction rolls back. Otherwise its updates become visible to future transactions.

Lock-Free Skiplist
The lock-free skiplist data structure created by Maurice Herlihy, Yossi Lev, and Nir Shavit. See Herlihy's and Shavit's book "The Art of Multiprocessor Programming" and Kir Fraser's dissertation "Practical Lock Freedom"

http://www.amazon.com/Art-Multiprocessor-Programming-Maurice-Herlihy/dp/0123705916/
http://www.cl.cam.ac.uk/techreports/UCAM-CL-TR-579.pdf
I've generalized the data structure to support update operations like set() and CAS() in addition to the normal add() and remove() operations, while preserving the lock-free property and linearizability.

Lock-Free Hashtable
Cliff Click's lock-free hash table from

http://www.azulsystems.com/events/javaone_2008/2008_CodingNonBlock.pdf
http://sourceforge.net/projects/high-scale-lib
