

ConcurrentHashMap的table 是一个Mode数组，  数组的长度默认为 16。

HashMap的Node[]默认长度也是16

jdk8里ConcurrentHashMap里线程安全的实现，没有用jdk1.6的段锁的原理，而用的是CAS (Unsafe.compareAndSwapXXX)



