# Great Ideas in Computer Architecture

1. Design for **Moore's Law**.

    - IC resources typically increases, so Computer Architecture need to take
      into account where the level of processing power lies when the
      architecture design is anticipated to complete by.

2. Use **abstractions** to simply the mental model.

    - Develop high-level abstractions to hide away distracting lower-level
      details.

3. Make the **common case** fast (optimize the hot path).

    - Most performance gain is achieved through optimizing the common paths.
    - Optimization should *always* be driven by empirical measurements to both
      identify the areas where optimization is needed and if substantial
      performance is gained by the optimization applied.

4. Performance via **parallelism**.

    - By exploiting multiple processors, we may be able to complete tasks
      faster by executing code in parallel.

5. Performance via **pipelining**.

    - Through cooperative scheduling and instruction reordering, we may be
      able to execute more instructions in the same number of CPU cycles.

6. Performance via **prediction**.

    - We try to execute instructions that are *likely* to be run, by guessing
      and try to start work before it's actually demanded, assuming
      misprediction can be recovered and is not too costly.

7. **Memory hierarchy**.

    - Organize memory and caches in a hierarhical fashion: the smallest, fastest
      and most expensive memory resides near the processor, whereas the largest,
      slowest and least expensive memory resides further away.

8. Dependability via **redundancy**.

    - Include duplicate components to facilitate error detection and graceful
      error recovery via fallback to the backup hardware components.
