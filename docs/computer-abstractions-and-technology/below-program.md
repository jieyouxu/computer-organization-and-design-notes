# Below a Typical Program

Multiple layers of abstractions are put in place between the user-space program
and the hardware to *abstract* away some lower-level details.

Typically, between the application sofware and hardware, there exists
**systems software**, that either come as **Operating Systems** (OSes) and/or
**Hardware Abstraction Layers** (HALs).

For PCs and servers, it is typically the case that the OS serves as the
intermediate layer between the user's program and the hardware that the OS
runs on. Typically, important operations (APIs) that are provided by the OS
includes:

- Basic I/O operations.
- Storage and memory allocation.
- Disciplined sharing of common resources between multiple applications that
  may try to use the simultaneously.

To *translate* human-readable programs (think program source code) into programs
that the hardware can understand, **compilers** transform high-level source
code into processor instructions that the processor can understand and execute.

## From High-Level Language to Hardware Language

The digital hardware only understands binary signals, either *on* or *off*,
typically encoded as `0` and `1` respectively. Each of such individual signal
is referred to as a **binary digit** or **bit**. The processor can understand
a specific set of **instructions**, which are fixed-width bits that are
organized to rules specified by the **instruction set** (IS).

An important oberservation to make is that both data and instructions are
stored and encoded using the same representation – bits.

But it is *tedius* and *error-prone* to hand write long sequences of `0`s and
`1`s, so **assemblers** were developed to translate symbolic languages
(**Assembly** languages) into these sequences of `0`s and `1`s, to set in place
a thin layer of abstraction that makes these sequences of `0`s and `1`s more
readable to humans.

But the Assembly languages are still too primitive and tedious to write, so
Computer Scientists invented **high-level programming languages** such as C
or Rust, so that more domain-specific abstractions can be used to help aid
understanding of the program and reduce repetition.

!!! example "High-level language, assembly language and machine language"

    The same program, but in different languages (no optimizations performed),
    assume no reordering, caching or speculative execution.

    === "High-level Language (Rust)"

        ```rust
        #![no_std]
        pub fn square(num: i32) -> i32 {
            num * num
        }
        ```
    
    === "Assembly (riscv64gc-unknown-none-elf)"

        Compiled with `rustc` (`rustc 1.48.0-nightly (8fe73e80d 2020-10-01)`)
        via

        ```
        rustc +nightly --target=riscv64gc-unknown-none-elf
        ```

        for bare RISC-V (RV64IMAFDC ISA).

        ```asm
        square:
            addi    sp, sp, -16
            sext.w  a1, a0
            mul     a2, a1, a1
            mulw    a3, a1, a1
            xor     a3, a3, a2
            mulh    a1, a1, a1
            srai    a4, a2, 63
            xor     a1, a1, a4
            or      a1, a1, a3
            mv      a3, zero
            sd      a2, 8(sp)
            bne     a1, a3, .LBB0_2
            j       .LBB0_1
        ```

    === "Machine Language"

        Omitted for brevity. You can hand-translate this with RISC-V 64 bit
        ISA.

Now, while high-level programming languages are so often used instead of bare
assembly due to many benefits, such as better abstraction and readibility,
use cases for assembly still exists:

- Inline assembly (may call-out to platform-specific intrinsics).
- Extremely performance-critical parts (that the compiler's optimization passes
  may have missed or is too conservative).
