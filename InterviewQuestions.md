## CUDA
1. 与CUDA相关的几个概念：thread，block，grid，warp，sp，sm。
- sp: 小核（流处理器）最基本的处理单元，streaming processor 最后具体的指令和任务都是在sp上处理的。GPU进行并行计算，也就是很多个sp同时做处理.
- sm: 大核（流多处理器）多个sp加上其他的一些资源组成一个sm, streaming multiprocessor. 其他资源也就是存储资源，共享内存，寄储器等。
- Warp：（线程束）GPU执行程序时的调度单位，一起执行。目前cuda的warp的大小为32，同在一个warp的线程，以不同数据资源执行相同的指令。
- grid、block、thread：在利用cuda进行编程时，一个grid分为多个block(最多1024)，而一个block分为多个thread.其中任务划分到是否影响最后的执行效果。。
- 每个GPU有很多core，每个core有相应的16-32个SIMD ALU
2. 利用图形API 和CUDA进行GPU通用计算的性能区别？
- 利用图形API需要把问题转化为图形学的变化；而CUDA是C语言的扩展，比较适合做通用计算
3. GPU的指令和CPU指令的最大区别？
- CPU需要运行OS，不但要处理中断，还要负责存储器空间分配与回收，CPU指令有很多都是操作特权寄存器；GPU目前还做不到这一点

3. 你怎么样知道是否达到了GPU的理论加速倍数？怎么计算？
    通过成千上万线程来隐藏访问延迟
4. GPU架构的缺点？如果让你设计，你会怎么改进？
    a.精度问题，b.编程模式不太灵活
5. GPU有通过成千上万线程来隐藏访问延迟，CPU也有隐藏访问延迟的优化，最大的区别是什么？
    CPU的线程切换开销是昂贵的，一般都是需要1000cycle而gpu的线程切换只有1个cycle
6. 请你列举出一些常用的优化方法
-（线程束->线程块）对于block和thread的分配问题，有这么一个技巧，每个block里面的thread个数最好是32的倍数，因为，这样可以让线程束一起执行，计算效率更高，促进memory coalescing
- (线程块)一个sm只会执行一个block里的warp，当该block里warp执行完才会执行其他block里的warp。进行划分时，最好保证每个block里的warp比较合理，那样可以一个sm可以交替执行里面的warp，从而提高效率，此外，在分配block时，要根据GPU的sm个数，分配出合理的block数，让GPU的sm都利用起来，提利用率。分配时，也要考虑到同一个线程block的资源问题，不要出现对应的资源不够。
-（内存）共享内存的使用量也是影响occupancy的一个重要因子，一块大核拥有一块共享内存。shared添加到变量声明中，这将使这个变量驻留在共享内存中。在声明共享内存变量后，线程块中的每个线程都共享这块内存，使得一个线程块中的多个线程能够在计算上进行通信和协作。
- (内存）纹理缓存是只读的内存，专门为内存访问存在大量空间局部性的设计，核函数需要特殊的函数告诉GPU读取纹理内存而不是全局内存。使用纹理内存，如果同一个线程束内的thread的访问地址很近的话，那么性能更高。

## Tricks
2^64 = 16 * 2 ^60 = 16 * 10^6
64 = 2^6
256 = 2^8

## Parallel Computing Lecture Takeaways
- simple processor: executes one instruction per clock = Decode + ALU + Execution Context.
- More transistors = larger cache, smarter out-of-order logic, smarter branch predictor, etc.
- SIMD processing: needs more ALUs -> should handle conditional execution/branching
  - SSE instructions: 128-bit operations: 4x32 bits or 2x64 bits (4-wide float vectors)
  - AVX instructions: 256-bit operations: 8x32 bits or 4x64 bits (8-wide float vectors)
  - SIMD parallelization is performed at compile time
- Several forms of parallel execution in modern processors
  - 1) multi-core. 2) SIMD. 3) Superscalar 
  多线程是指一个程序中产生多个线程来完成工作。在单核处理器上，多线程通过交替执行来完成，线程来回切换时【不同线程的指令、数据需要载入寄存器】，需要浪费一定的时间。多核处理器上，多线程真正的是同时运行。SMT 同时多线程，也叫超线程，是Intel提出的。 是指一个核心同时拥有两套寄存器、缓存，保存两个线程工作的现场。 线程之间切换几乎没有成本。可以有效的支持多线程程序。
  
 - Prefetching reduces stalls (hides latency) while multi-threading hides stalls
 - GPUs: Extreme throughput-oriented processors v.s CPU: a lot of resource control, scheduling and managin many components of the syste,
 - CPU: Big caches, few threads, modest memory BW. Rely mainly on caches and prefetching
   - Fetch -> Decode -> Execute -> Commit
 - GPU: Small caches, many threads, huge memory BW. Rely mainly on multi-threading
 - Bandwidth bound: If processors request data at too high a rate, the memory system cannot keep up. No amount of latency hiding helps this. 
   - Data re-use. 
   - Share data across threads
   - Arithmetic intensity
