# V8 Behaviour-Modifying Options

## Modifications to the JavaScript Language

  --use-strict (enforce strict mode)
        type: bool  default: false

## Modifications to the Code Optimization

## Modifications to Garbage Collection Behaviour


# TBD:
  --expose-wasm (expose wasm interface to JavaScript)
        type: bool  default: true
  --wasm-disable-structured-cloning (disable wasm structured cloning)
        type: bool  default: false
  --wasm-num-compilation-tasks (number of parallel compilation tasks for wasm)
        type: int  default: 10
  --wasm-write-protect-code-memory (write protect code memory on the wasm native heap)
        type: bool  default: false
  --wasm-async-compilation (enable actual asynchronous compilation for WebAssembly.compile)
        type: bool  default: true
  --wasm-test-streaming (use streaming compilation instead of async compilation for tests)
        type: bool  default: false
  --wasm-max-mem-pages (maximum number of 64KiB memory pages of a wasm instance)
        type: uint  default: 32767
  --wasm-max-table-size (maximum table size of a wasm instance)
        type: uint  default: 10000000
  --wasm-max-code-space (maximum committed code space for wasm (in MB))
        type: uint  default: 1024
  --wasm-tier-up (enable wasm baseline compilation and tier up to the optimizing compiler)
        type: bool  default: true
  --liftoff (enable Liftoff, the baseline compiler for WebAssembly)
        type: bool  default: false
  --wasm-break-on-decoder-error (debug break when wasm decoder encounters an error)
        type: bool  default: false
  --wasm-tier-mask-for-testing (bitmask of functions to compile with TurboFan instead of Liftoff)
        type: int  default: 0
  --assume-asmjs-origin (force wasm decoder to assume input is internal asm-wasm format)
        type: bool  default: false
  --validate-asm (validate asm.js modules before compiling)
        type: bool  default: true
  --suppress-asm-messages (don't emit asm.js related messages (for golden file testing))
        type: bool  default: false
  --stress-validate-asm (try to validate everything as asm.js)
        type: bool  default: false
 --turbo-sp-frame-access (use stack pointer-relative access to frame wherever possible)
        type: bool  default: false
  --turbo-control-flow-aware-allocation (consider control flow while allocating registers)
        type: bool  default: false
  --turbo-filter (optimization filter for TurboFan compiler)
        type: string  default: *
  --turbo-verify (verify TurboFan graphs at each phase)
        type: bool  default: true
  --turbo-verify-machine-graph (verify TurboFan machine graph before instruction selection)
        type: string  default: nullptr
  --turbo-stats (print TurboFan statistics)
        type: bool  default: false
  --turbo-stats-nvp (print TurboFan statistics in machine-readable format)
        type: bool  default: false
  --turbo-stats-wasm (print TurboFan statistics of wasm compilations)
        type: bool  default: false
  --turbo-splitting (split nodes during scheduling in TurboFan)
        type: bool  default: true
  --function-context-specialization (enable function context specialization in TurboFan)
        type: bool  default: false
  --turbo-inlining (enable inlining in TurboFan)
        type: bool  default: true
  --turbo-inline-array-builtins (inline array builtins in TurboFan code)
        type: bool  default: true
  --turbo-load-elimination (enable load elimination in TurboFan)
        type: bool  default: true
  --turbo-profiling (enable profiling in TurboFan)
        type: bool  default: false
  --turbo-verify-allocation (verify register allocation in TurboFan)
        type: bool  default: true
  --turbo-move-optimization (optimize gap moves in TurboFan)
        type: bool  default: true
  --turbo-jt (enable jump threading in TurboFan)
        type: bool  default: true
  --turbo-loop-peeling (Turbofan loop peeling)
        type: bool  default: true
  --turbo-loop-variable (Turbofan loop variable optimization)
        type: bool  default: true
  --turbo-loop-rotation (Turbofan loop rotation)
        type: bool  default: true
  --turbo-cf-optimization (optimize control flow in TurboFan)
        type: bool  default: true
  --turbo-escape (enable escape analysis)
        type: bool  default: true
  --turbo-allocation-folding (Turbofan allocation folding)
        type: bool  default: true
  --turbo-instruction-scheduling (enable instruction scheduling in TurboFan)
        type: bool  default: false
  --turbo-stress-instruction-scheduling (randomly schedule instructions to stress dependency tracking)
        type: bool  default: false
  --turbo-store-elimination (enable store-store elimination in TurboFan)
        type: bool  default: true
  --turbo-rewrite-far-jumps (rewrite far to near jumps (ia32,x64))
        type: bool  default: true
  --experimental-inline-promise-constructor (inline the Promise constructor in TurboFan)
        type: bool  default: true

  --es-staging (enable test-worthy harmony features (for internal use only))
        type: bool  default: false
  --harmony (enable all completed harmony features)
        type: bool  default: false
  --harmony-shipping (enable all shipped harmony features)
        type: bool  default: true
  --harmony-private-methods (enable "harmony private methods in class literals" (in progress))
        type: bool  default: false
  --harmony-regexp-sequence (enable "RegExp Unicode sequence properties" (in progress))
        type: bool  default: false
  --harmony-weak-refs (enable "harmony weak references" (in progress))
        type: bool  default: false
  --harmony-intl-add-calendar-numbering-system (enable "Add calendar and numberingSystem to DateTimeFormat")
        type: bool  default: false
  --harmony-intl-numberformat-unified (enable "Unified Intl.NumberFormat Features")
        type: bool  default: false
  --harmony-intl-segmenter (enable "Intl.Segmenter")
        type: bool  default: false
  --harmony-namespace-exports (enable "harmony namespace exports (export * as foo from 'bar')")
        type: bool  default: true
  --harmony-sharedarraybuffer (enable "harmony sharedarraybuffer")
        type: bool  default: true
  --harmony-import-meta (enable "harmony import.meta property")
        type: bool  default: true
  --harmony-dynamic-import (enable "harmony dynamic import")
        type: bool  default: true
  --harmony-global (enable "harmony global")
        type: bool  default: true
  --harmony-object-from-entries (enable "harmony Object.fromEntries()")
        type: bool  default: true
  --harmony-hashbang (enable "harmony hashbang syntax")
        type: bool  default: true
  --harmony-numeric-separator (enable "harmony numeric separator between digits")
        type: bool  default: true
  --harmony-promise-all-settled (enable "harmony Promise.allSettled")
        type: bool  default: true
  --harmony-intl-bigint (enable "BigInt.prototype.toLocaleString")
        type: bool  default: true
  --harmony-intl-date-format-range (enable "DateTimeFormat formatRange")
        type: bool  default: true
  --harmony-intl-datetime-style (enable "dateStyle timeStyle for DateTimeFormat")
        type: bool  default: true
  --icu-timezone-data (get information about timezones from ICU)
        type: bool  default: true
  --lite-mode (enables trade-off of performance for memory savings)
        type: bool  default: false
  --future (Implies all staged features that we want to ship in the not-too-far future)
        type: bool  default: false
  --allocation-site-pretenuring (pretenure with allocation sites)
        type: bool  default: true
  --page-promotion (promote pages based on utilization)
        type: bool  default: true
  --page-promotion-threshold (min percentage of live bytes on a page to enable fast evacuation)
        type: int  default: 70
  --track-fields (track fields with only smi values)
        type: bool  default: true
  --track-double-fields (track fields with double values)
        type: bool  default: true
  --track-heap-object-fields (track fields with heap values)
        type: bool  default: true
  --track-computed-fields (track computed boilerplate fields)
        type: bool  default: true
  --track-field-types (track field types)
        type: bool  default: true
  --feedback-normalization (feed back normalization to constructors)
        type: bool  default: false
  --fast-calls-with-arguments-mismatches (skip arguments adaptor frames when it's provably safe)
        type: bool  default: true
  --enable-one-shot-optimization (Enable size optimizations for the code that will only be executed once)
        type: bool  default: true
  --enable-sealed-frozen-elements-kind (Enable sealed, frozen elements kind)
        type: bool  default: true
  --unbox-double-arrays (automatically unbox arrays of doubles)
        type: bool  default: true
  --interrupt-budget (interrupt budget which should be used for the profiler counter)
        type: int  default: 147456
  --jitless (Disable runtime allocation of executable memory.)
        type: bool  default: false
  --use-ic (use inline caching)
        type: bool  default: true
  --budget-for-feedback-vector-allocation (The budget in amount of bytecode executed by a function before we decide to allocate feedback vectors)
        type: int  default: 1024
  --lazy-feedback-allocation (Allocate feedback vectors lazily)
        type: bool  default: false
  --ignition-elide-noneffectful-bytecodes (elide bytecodes which won't have any external effect)
        type: bool  default: true
  --ignition-reo (use ignition register equivalence optimizer)
        type: bool  default: true
  --ignition-filter-expression-positions (filter expression positions before the bytecode pipeline)
        type: bool  default: true
  --ignition-share-named-property-feedback (share feedback slots when loading the same named property from the same object)
        type: bool  default: true
  --enable-lazy-source-positions (skip generating source positions during initial compile but regenerate when actually required)
        type: bool  default: false
  --fast-math (faster (but maybe less accurate) math functions)
        type: bool  default: true
  --concurrent-recompilation (optimizing hot functions asynchronously on a separate thread)
        type: bool  default: true
  --concurrent-recompilation-queue-length (the length of the concurrent compilation queue)
        type: int  default: 8
  --concurrent-recompilation-delay (artificial compilation delay in ms)
        type: int  default: 0
  --block-concurrent-recompilation (block queued jobs until released)
        type: bool  default: false
  --concurrent-inlining (run optimizing compiler's inlining phase on a separate thread)
        type: bool  default: false
  --stress-runs (number of stress runs)
        type: int  default: 0
  --deopt-every-n-times (deoptimize every n times a deopt point is passed)
        type: int  default: 0
  --opt (use adaptive optimizations)
        type: bool  default: true
  --csa-trap-on-node (trigger break point when a node with given id is created in given stub. The format is: StubName,NodeId)
        type: string  default: nullptr
  --max-inlined-bytecode-size (maximum size of bytecode for a single inlining)
        type: int  default: 500
  --max-inlined-bytecode-size-cumulative (maximum cumulative size of bytecode considered for inlining)
        type: int  default: 1000
  --max-inlined-bytecode-size-absolute (maximum cumulative size of bytecode considered for inlining)
        type: int  default: 5000
  --reserve-inline-budget-scale-factor (maximum cumulative size of bytecode considered for inlining)
        type: float  default: 1.2
  --max-inlined-bytecode-size-small (maximum size of bytecode considered for small function inlining)
        type: int  default: 30
  --max-optimized-bytecode-size (maximum bytecode size to be considered for optimization; too high values may cause the compiler to hit (release) assertions)
        type: int  default: 61440
  --min-inlining-frequency (minimum frequency for inlining)
        type: float  default: 0.15
  --polymorphic-inlining (polymorphic inlining)
        type: bool  default: true
  --stress-inline (set high thresholds for inlining to inline as much as possible)
        type: bool  default: false
  --inline-accessors (inline JavaScript accessors)
        type: bool  default: true
  --use-osr (use on-stack replacement)
        type: bool  default: true
  --analyze-environment-liveness (analyze liveness of environment slots and zap dead values)
        type: bool  default: true   
  --stress-gc-during-compilation (simulate GC/compiler thread race related to https://crbug.com/v8/8520)
        type: bool  default: false
  --optimize-for-size (Enables optimizations which favor memory size over execution speed)
        type: bool  default: false
  --untrusted-code-mitigations (Enable mitigations for executing untrusted code)
        type: bool  default: false
  --experimental-wasm-mv (enable prototype multi-value support for wasm)
        type: bool  default: false
  --experimental-wasm-eh (enable prototype exception handling opcodes for wasm)
        type: bool  default: false
  --experimental-wasm-se (enable prototype sign extension opcodes for wasm)
        type: bool  default: true
  --experimental-wasm-sat-f2i-conversions (enable prototype saturating float conversion opcodes for wasm)
        type: bool  default: true
  --experimental-wasm-threads (enable prototype thread opcodes for wasm)
        type: bool  default: false
  --experimental-wasm-simd (enable prototype SIMD opcodes for wasm)
        type: bool  default: false
  --experimental-wasm-anyref (enable prototype anyref opcodes for wasm)
        type: bool  default: false
  --experimental-wasm-bigint (enable prototype JS BigInt support for wasm)
        type: bool  default: false
  --experimental-wasm-bulk-memory (enable prototype bulk memory opcodes for wasm)
        type: bool  default: true
  --experimental-wasm-return-call (enable prototype return call opcodes for wasm)
        type: bool  default: false
  --experimental-wasm-type-reflection (enable prototype wasm type reflection in JS for wasm)
        type: bool  default: false
  --experimental-wasm-compilation-hints (enable prototype compilation hints section for wasm)
        type: bool  default: false
  --wasm-opt (enable wasm optimization)
        type: bool  default: false
  --wasm-no-bounds-checks (disable bounds checks (performance testing only))
        type: bool  default: false
  --wasm-no-stack-checks (disable stack checks (performance testing only))
        type: bool  default: false
  --wasm-math-intrinsics (intrinsify some Math imports into wasm)
        type: bool  default: true
  --wasm-shared-engine (shares one wasm engine between all isolates within a process)
        type: bool  default: true
  --wasm-shared-code (shares code underlying a wasm module when it is transferred)
        type: bool  default: true
  --wasm-trap-handler (use signal handlers to catch out of bounds memory access in wasm (currently Linux x86_64 only))
        type: bool  default: true
  --wasm-fuzzer-gen-test (generate a test case when running a wasm fuzzer)
        type: bool  default: false

  --wasm-interpret-all (execute all wasm code in the wasm interpreter)
        type: bool  default: false
  --asm-wasm-lazy-compilation (enable lazy compilation for asm-wasm modules)
        type: bool  default: false
  --wasm-lazy-compilation (enable lazy compilation for all wasm modules)
        type: bool  default: false

  --wasm-grow-shared-memory (allow growing shared WebAssembly memory objects)
        type: bool  default: false
  --wasm-lazy-validation (enable lazy validation for lazily compiled wasm functions)
        type: bool  default: false
  --wasm-code-gc (enable garbage collection of wasm code)
        type: bool  default: false
  --stress-wasm-code-gc (stress test garbage collection of wasm code)
        type: bool  default: false
  --frame-count (number of stack frames inspected by the profiler)
        type: int  default: 1
  --stress-sampling-allocation-profiler (Enables sampling allocation profiler with X as a sample interval)
        type: int  default: 0
  --min-semi-space-size (min size of a semi-space (in MBytes), the new space consists of two semi-spaces)
        type: size_t  default: 0
  --max-semi-space-size (max size of a semi-space (in MBytes), the new space consists of two semi-spaces)
        type: size_t  default: 0
  --semi-space-growth-factor (factor by which to grow the new space)
        type: int  default: 2
  --experimental-new-space-growth-heuristic (Grow the new space based on the percentage of survivors instead of their absolute value.)
        type: bool  default: false
  --max-old-space-size (max size of the old space (in Mbytes))
        type: size_t  default: 0
  --huge-max-old-generation-size (Increase max size of the old space to 4 GB for x64 systems withthe physical memory bigger than 16 GB)
        type: bool  default: false
  --initial-old-space-size (initial old space size (in Mbytes))
        type: size_t  default: 0
  --global-gc-scheduling (enable GC scheduling based on global memory)
        type: bool  default: false
  --gc-global (always perform global GCs)
        type: bool  default: false
  --random-gc-interval (Collect garbage after random(0, X) allocations. It overrides gc_interval.)
        type: int  default: 0
  --gc-interval (garbage collect after <n> allocations)
        type: int  default: -1
  --retain-maps-for-n-gc (keeps maps alive for <n> old space garbage collections)
        type: int  default: 2
  --incremental-marking (use incremental marking)
        type: bool  default: true
  --incremental-marking-wrappers (use incremental marking for marking wrappers)
        type: bool  default: true
  --parallel-scavenge (parallel scavenge)
        type: bool  default: true
  --write-protect-code-memory (write protect code memory)
        type: bool  default: true
  --concurrent-marking (use concurrent marking)
        type: bool  default: true
  --parallel-marking (use parallel marking in atomic pause)
        type: bool  default: true
  --ephemeron-fixpoint-iterations (number of fixpoint iterations it takes to switch to linear ephemeron algorithm)
        type: int  default: 10
  --concurrent-store-buffer (use concurrent store buffer processing)
        type: bool  default: true
  --concurrent-sweeping (use concurrent sweeping)
        type: bool  default: true
  --parallel-compaction (use parallel compaction)
        type: bool  default: true
  --parallel-pointer-update (use parallel pointer update during compaction)
        type: bool  default: true
  --detect-ineffective-gcs-near-heap-limit (trigger out-of-memory failure to avoid GC storm near heap limit)
        type: bool  default: true
  --track-gc-object-stats (track object counts and memory usage)
        type: bool  default: false
  --track-retaining-path (enable support for tracking retaining path)
        type: bool  default: false
  --concurrent-array-buffer-freeing (free array buffer allocations on a background thread)
        type: bool  default: true
  --gc-stats (Used by tracing internally to enable gc statistics)
        type: int  default: 0
  --track-detached-contexts (track native contexts that are expected to be garbage collected)
        type: bool  default: true
  --verify-heap (verify heap pointers before and after GC)
        type: bool  default: false
  --verify-heap-skip-remembered-set (disable remembered set verification)
        type: bool  default: false
  --move-object-start (enable moving of object starts)
        type: bool  default: true
  --memory-reducer (use memory reducer)
        type: bool  default: true
  --memory-reducer-for-small-heaps (use memory reducer for small heaps)
        type: bool  default: true
  --heap-growing-percent (specifies heap growing factor as (1 + heap_growing_percent/100))
        type: int  default: 0
  --v8-os-page-size (override OS page size (in KBytes))
        type: int  default: 0
  --always-compact (Perform compaction on every full GC)
        type: bool  default: false
  --never-compact (Never perform compaction on full GC - testing only)
        type: bool  default: false
  --compact-code-space (Compact code space on full collections)
        type: bool  default: true
  --flush-bytecode (flush of bytecode when it has not been executed recently)
        type: bool  default: true
  --stress-flush-bytecode (stress bytecode flushing)
        type: bool  default: false
  --use-marking-progress-bar (Use a progress bar to scan large objects in increments when incremental marking is active.)
        type: bool  default: true
  --force-marking-deque-overflows (force overflows of marking deque by reducing it's size to 64 words)
        type: bool  default: false
  --stress-compaction (stress the GC compactor to flush out bugs (implies --force_marking_deque_overflows))
        type: bool  default: false
  --stress-compaction-random (Stress GC compaction by selecting random percent of pages as evacuation candidates. It overrides stress_compaction.)
        type: bool  default: false
  --stress-incremental-marking (force incremental marking for small heaps and run it more often)
        type: bool  default: false
  --fuzzer-gc-analysis (prints number of allocations and enables analysis mode for gc fuzz testing, e.g. --stress-marking, --stress-scavenge)
        type: bool  default: false
  --stress-marking (force marking at random points between 0 and X (inclusive) percent of the regular marking start limit)
        type: int  default: 0
  --stress-scavenge (force scavenge at random points between 0 and X (inclusive) percent of the new space capacity)
        type: int  default: 0
  --gc-experiment-background-schedule (new background GC schedule heuristics)
        type: bool  default: false
  --gc-experiment-less-compaction (less compaction in non-memory reducing mode)
        type: bool  default: false
  --disable-abortjs (disables AbortJS runtime function)
        type: bool  default: false
  --manual-evacuation-candidates-selection (Test mode only flag. It allows an unit test to select evacuation candidates pages (requires --stress_compaction).)
        type: bool  default: false
  --fast-promotion-new-space (fast promote new space on high survival rates)
        type: bool  default: false
  --clear-free-memory (initialize free memory with 0)
        type: bool  default: false
  --young-generation-large-objects (allocates large objects by default in the young generation large object space)
        type: bool  default: true
  --idle-time-scavenge (Perform scavenges in idle time.)
        type: bool  default: true
  --debug-code (generate extra code (assertions) for debugging)
        type: bool  default: true
  --code-comments (emit comments in code disassembly; for more readable source positions you should add --no-concurrent_recompilation)
        type: bool  default: false
  --enable-sse3 (enable use of SSE3 instructions if available)
        type: bool  default: true
  --enable-ssse3 (enable use of SSSE3 instructions if available)
        type: bool  default: true
  --enable-sse4-1 (enable use of SSE4.1 instructions if available)
        type: bool  default: true
  --enable-sahf (enable use of SAHF instruction if available (X64 only))
        type: bool  default: true
  --enable-avx (enable use of AVX instructions if available)
        type: bool  default: true
  --enable-fma3 (enable use of FMA3 instructions if available)
        type: bool  default: true
  --enable-bmi1 (enable use of BMI1 instructions if available)
        type: bool  default: true
  --enable-bmi2 (enable use of BMI2 instructions if available)
        type: bool  default: true
  --enable-lzcnt (enable use of LZCNT instruction if available)
        type: bool  default: true
  --enable-popcnt (enable use of POPCNT instruction if available)
        type: bool  default: true
  --arm-arch (generate instructions for the selected ARM architecture if available: armv6, armv7, armv7+sudiv or armv8)
        type: string  default: armv8
  --force-long-branches (force all emitted branches to be in long mode (MIPS/PPC only))
        type: bool  default: false
  --mcpu (enable optimization for specific cpu)
        type: string  default: auto
  --partial-constant-pool (enable use of partial constant pools (X64 only))
        type: bool  default: true
  --enable-source-at-csa-bind (Include source information in the binary at CSA bind locations.)
        type: bool  default: false
  --enable-armv7 (deprecated (use --arm_arch instead))
        type: maybe_bool  default: unset
  --enable-vfp3 (deprecated (use --arm_arch instead))
        type: maybe_bool  default: unset
  --enable-32dregs (deprecated (use --arm_arch instead))
        type: maybe_bool  default: unset
  --enable-neon (deprecated (use --arm_arch instead))
        type: maybe_bool  default: unset
  --enable-sudiv (deprecated (use --arm_arch instead))
        type: maybe_bool  default: unset
  --enable-armv8 (deprecated (use --arm_arch instead))
        type: maybe_bool  default: unset
  --enable-regexp-unaligned-accesses (enable unaligned accesses for the regexp engine)
        type: bool  default: true
  --script-streaming (enable parsing on background)
        type: bool  default: true
  --disable-old-api-accessors (Disable old-style API accessors whose setters trigger through the prototype chain)
        type: bool  default: false
  --expose-free-buffer (expose freeBuffer extension)
        type: bool  default: false
  --expose-gc (expose gc extension)
        type: bool  default: false
  --expose-gc-as (expose gc extension under the specified name)
        type: string  default: nullptr
  --expose-externalize-string (expose externalize string extension)
        type: bool  default: false
  --expose-trigger-failure (expose trigger-failure extension)
        type: bool  default: false
  --stack-trace-limit (number of stack frames to capture)
        type: int  default: 10
  --builtins-in-stack-traces (show built-in functions in stack traces)
        type: bool  default: false
  --experimental-stack-trace-frames (enable experimental frames (API/Builtins) and stack trace layout)
        type: bool  default: false
  --disallow-code-generation-from-strings (disallow eval and friends)
        type: bool  default: false
  --expose-async-hooks (expose async_hooks object)
        type: bool  default: false
  --allow-unsafe-function-constructor (allow invoking the function constructor without security checks)
        type: bool  default: false
  --force-slow-path (always take the slow path for builtins)
        type: bool  default: false
  --test-small-max-function-context-stub-size (enable testing the function context size overflow path by making the maximum size smaller)
        type: bool  default: false
  --inline-new (use fast inline allocation)
        type: bool  default: true
  --trace (trace function calls)
        type: bool  default: false
  --lazy (use lazy compilation)
        type: bool  default: true
  --max-lazy (ignore eager compilation hints)
        type: bool  default: false

  --always-opt (always try to optimize functions)
        type: bool  default: false
  --always-osr (always try to OSR functions)
        type: bool  default: false
  --prepare-always-opt (prepare for turning on always opt)
        type: bool  default: false

  --external-reference-stats (print statistics on external references used during serialization)
        type: bool  default: false
  --compilation-cache (enable compilation cache)
        type: bool  default: true
  --cache-prototype-transitions (cache prototype transitions)
        type: bool  default: true
  --parallel-compile-tasks (enable parallel compile tasks)
        type: bool  default: false
  --compiler-dispatcher (enable compiler dispatcher)
        type: bool  default: false

  --cpu-profiler-sampling-interval (CPU profiler sampling interval in microseconds)
        type: int  default: 1000

  --hard-abort (abort by crashing)
        type: bool  default: true
  --expose-inspector-scripts (expose injected-script-source.js for debugging)
        type: bool  default: false
  --stack-size (default size of stack region v8 is allowed to use (in kBytes))
        type: int  default: 984
  --max-stack-trace-source-length (maximum length of function source code printed in a stack trace.)
        type: int  default: 300
  --clear-exceptions-on-js-entry (clear pending exceptions when entering JavaScript)
        type: bool  default: false
  --histogram-interval (time interval in ms for aggregating memory histograms)
        type: int  default: 600000

  --heap-profiler-use-embedder-graph (Use the new EmbedderGraph API to get embedder nodes)
        type: bool  default: true
  --heap-snapshot-string-limit (truncate strings to this length in the heap snapshot)
        type: int  default: 1024
  --sampling-heap-profiler-suppress-randomness (Use constant sample intervals to eliminate test flakiness)
        type: bool  default: false
  --use-idle-notification (Use idle notification to reduce memory footprint.)
        type: bool  default: true

  --modify-field-representation-inplace (enable in-place field representation updates)
        type: bool  default: true
  --max-polymorphic-map-count (maximum number of maps to track in POLYMORPHIC state)
        type: int  default: 4
  --native-code-counters (generate extra code for manipulating stats counters)
        type: bool  default: true
  --thin-strings (Enable ThinString support)
        type: bool  default: true
  --use-verbose-printer (allows verbose printing)
        type: bool  default: true
  --allow-natives-syntax (allow natives syntax)
        type: bool  default: false
  --parse-only (only parse the sources)
        type: bool  default: false
  --debug-sim (Enable debugging the simulator)
        type: bool  default: false
  --check-icache (Check icache flushes in ARM and MIPS simulator)
        type: bool  default: false
  --stop-sim-at (Simulator stop after x number of instructions)
        type: int  default: 0
  --sim-stack-alignment (Stack alingment in bytes in simulator (4 or 8, 8 is default))
        type: int  default: 8
  --sim-stack-size (Stack size of the ARM64, MIPS64 and PPC64 simulator in kBytes (default is 2 MB))
        type: int  default: 2048
  --log-colour (When logging, try to use coloured output.)
        type: bool  default: true
  --ignore-asm-unimplemented-break (Don't break for ASM_UNIMPLEMENTED_BREAK macros.)
        type: bool  default: false
  --async-stack-traces (include async stack traces in Error.stack)
        type: bool  default: true
  --stack-trace-on-illegal (print stack trace when an illegal exception is thrown)
        type: bool  default: false
  --abort-on-uncaught-exception (abort program (dump core) when an uncaught exception is thrown)
        type: bool  default: false
  --correctness-fuzzer-suppressions (Suppress certain unspecified behaviors to ease correctness fuzzing: Abort program when the stack overflows or a string exceeds maximum length (as opposed to throwing RangeError). Use a fixed suppression string for error messages.)
        type: bool  default: false
  --randomize-hashes (randomize hashes to avoid predictable hash collisions (with snapshots this option cannot override the baked-in seed))
        type: bool  default: true
  --rehash-snapshot (rehash strings from the snapshot to override the baked-in seed)
        type: bool  default: true
  --hash-seed (Fixed seed to use to hash property keys (0 means random)(with snapshots this option cannot override the baked-in seed))
        type: uint64  default: 0
  --random-seed (Default seed for initializing random generator (0, the default, means to use system random).)
        type: int  default: 0
  --fuzzer-random-seed (Default seed for initializing fuzzer random generator (0, the default, means to use v8's random number generator seed).)
        type: int  default: 0


  --detailed-error-stack-trace (includes arguments for each function call in the error stack frames array)
        type: bool  default: false
  --runtime-call-stats (report runtime call counts and times)
        type: bool  default: false
  --profile-deserialization (Print the time it takes to deserialize the snapshot.)
        type: bool  default: false
  --serialization-statistics (Collect statistics on serialized objects.)
        type: bool  default: false
  --serialization-chunk-size (Custom size for serialization chunks)
        type: uint  default: 4096
  --regexp-optimization (generate optimized regexp code)
        type: bool  default: true
  --regexp-mode-modifiers (enable inline flags in regexp.)
        type: bool  default: false
  --regexp-interpret-all (interpret all regexp code)
        type: bool  default: false
  --testing-bool-flag (testing_bool_flag)
        type: bool  default: true
  --testing-maybe-bool-flag (testing_maybe_bool_flag)
        type: maybe_bool  default: unset
  --testing-int-flag (testing_int_flag)
        type: int  default: 13
  --testing-float-flag (float-flag)
        type: float  default: 2.5
  --testing-string-flag (string-flag)
        type: string  default: Hello, world!
  --testing-prng-seed (Seed used for threading test randomness)
        type: int  default: 42
  --embedded-src (Path for the generated embedded data file. (mksnapshot only))
        type: string  default: nullptr
  --embedded-variant (Label to disambiguate symbols in embedded data file. (mksnapshot only))
        type: string  default: nullptr
  --startup-src (Write V8 startup as C++ src. (mksnapshot only))
        type: string  default: nullptr
  --startup-blob (Write V8 startup blob file. (mksnapshot only))
        type: string  default: nullptr
  --target-arch (The mksnapshot target arch. (mksnapshot only))
        type: string  default: nullptr
  --target-os (The mksnapshot target os. (mksnapshot only))
        type: string  default: nullptr
  --minor-mc-parallel-marking (use parallel marking for the young generation)
        type: bool  default: true

  --minor-mc (perform young generation mark compact GCs)
        type: bool  default: false
  --help (Print usage message, including flags, on console)
        type: bool  default: true

  --use-external-strings (Use external strings for source code)
        type: bool  default: false
  --map-counters (Map counters to a file)
        type: string  default: 
  --mock-arraybuffer-allocator (Use a mock ArrayBuffer allocator for testing.)
        type: bool  default: false
  --mock-arraybuffer-allocator-limit (Memory limit for mock ArrayBuffer allocator used to simulate OOM for testing.)
        type: size_t  default: 0
  --gdbjit (enable GDBJIT interface)
        type: bool  default: false
  --gdbjit-full (enable GDBJIT interface for all code objects)
        type: bool  default: false
  --gdbjit-dump (dump elf objects with debug info to disk)
        type: bool  default: false
  --gdbjit-dump-filter (dump only objects containing this substring)
        type: string  default: 
  --enable-slow-asserts (enable asserts that are slow to execute)
        type: bool  default: true
e
  --trap-on-abort (replace aborts by breakpoints)
        type: bool  default: false


  --gc-verbose (print stuff during garbage collection)
        type: bool  default: false
  --code-stats (report code statistics after GC)
        type: bool  default: false

  --check-handle-count (Check that there are not too many handles at GC)
        type: bool  default: false


  --collect-heap-spill-statistics (report heap spill statistics along with heap_stats (requires heap_stats))
        type: bool  default: false

  --regexp-possessive-quantifier (enable possessive quantifier syntax for testing)
        type: bool  default: false
  --prof (Log statistical profiling information (implies --log-code).)
        type: bool  default: false
  --detailed-line-info (Always generate detailed line information for CPU profiling.)
        type: bool  default: false
  --prof-sampling-interval (Interval for --prof samples (in microseconds).)
        type: int  default: 1000
  --prof-cpp (Like --prof, but ignore generated code.)
        type: bool  default: false
  --prof-browser-mode (Used with --prof, turns on browser-compatible mode for profiling.)
        type: bool  default: true
  --logfile (Specify the name of the log file.)
        type: string  default: v8.log
  --logfile-per-isolate (Separate log files for each isolate.)
        type: bool  default: true
  --ll-prof (Enable low-level linux profiler.)
        type: bool  default: false
  --perf-basic-prof (Enable perf linux profiler (basic support).)
        type: bool  default: false
  --perf-basic-prof-only-functions (Only report function code ranges to perf (i.e. no stubs).)
        type: bool  default: false
  --perf-prof (Enable perf linux profiler (experimental annotate support).)
        type: bool  default: false
  --perf-prof-unwinding-info (Enable unwinding info for perf linux profiler (experimental).)
        type: bool  default: false
  --gc-fake-mmap (Specify the name of the file for fake gc mmap used in ll_prof)
        type: string  default: /tmp/__v8_gc__
  --log-internal-timer-events (Time internal events.)
        type: bool  default: false
  --log-instruction-stats (Log AArch64 instruction statistics.)
        type: bool  default: false
  --log-instruction-file (AArch64 instruction statistics log file.)
        type: string  default: arm64_inst.csv
  --log-instruction-period (AArch64 instruction statistics logging period.)
        type: int  default: 4194304
  --redirect-code-traces (output deopt information and disassembly into file code-<pid>-<isolate id>.asm)
        type: bool  default: false
  --redirect-code-traces-to (output deopt information and disassembly into the given file)
        type: string  default: nullptr
  --win64-unwinding-info (Enable unwinding info for Windows/x64)
        type: bool  default: true
  --interpreted-frames-native-stack (Show interpreted frames on the native stack (useful for external profilers).)
        type: bool  default: false
  --sodium (print generated code output suitable for use with the Sodium code viewer)
        type: bool  default: false
  --predictable (enable predictable mode)
        type: bool  default: false
  --predictable-gc-schedule (Predictable garbage collection schedule. Fixes heap growing, idle, and memory reducing behavior.)
        type: bool  default: false
  --single-threaded (disable the use of background tasks)
        type: bool  default: false
  --single-threaded-gc (disable the use of background gc tasks)
        type: bool  default: false


}

Other options: 
--no-arguments
--stress-opt
--stress-deopt
--stress-background-compile
--noalways-opt
--logfile-per-isolate
--shell
--test
--send-idle-notification
--invoke-weak-callbacks
--omit-quit
--no-wait-for-wasm
--isolate
--throws
--icu-data-file
--natives_blob
--snapshot_blob
--cache=code|none|after-execute|full-code-cache
--enable-tracing
--trace-path
--trace-config
--enable-inspector
--lcov
--disable-in-process-stack-traces
--read-from-tcp-port
--enable-os-system
--quiet-load
--thread-pool-size
--stress-delay-tasks
--module
