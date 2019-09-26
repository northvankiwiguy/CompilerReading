# V8 Debug/Trace/Log Options

The following options can be passed to the `d8` executable, with the goal of generating debug/trace output. This list of options was extracted from d8 version 7.7.0, and can be find via `d8 --help` or in `src/flags/flag-definitions.h`.

Note that at start-up time, a lot of additional debug output is displayed, as various default functions are initialized.

## Parser Debugging

### `--print-ast`

type: `bool`,  default: `false`

Displays a pretty-printed version of the parsed AST.

Code in:
* `src/interpreter/interpreter.cc:MaybePrintAst()`
* `src/ast/prettyprinter.cc:AstPrinter::PrintProgram()`

## Ignition Debugging

  --trace-ignition-codegen (trace the codegen of ignition interpreter bytecode handlers)
        type: bool  default: false
  --trace-ignition-dispatches (traces the dispatches to bytecode handlers by the ignition interpreter)
        type: bool  default: false
  --trace-ignition-dispatches-output-file (the file to which the bytecode handler dispatch table is written (by default, the table is not written to a file))
        type: string  default: nullptr      

## Turbofan Debugging

  --trace-turbo (trace generated TurboFan IR)
        type: bool  default: false
  --trace-turbo-path (directory to dump generated TurboFan IR to)
        type: string  default: nullptr
  --trace-turbo-filter (filter for tracing turbofan compilation)
        type: string  default: *
  --trace-turbo-graph (trace generated TurboFan graphs)
        type: bool  default: false
  --trace-turbo-scheduled (trace TurboFan IR with schedule)
        type: bool  default: false
  --trace-turbo-cfg-file (trace turbo cfg graph (for C1 visualizer) to a given file name)
        type: string  default: nullptr
  --trace-turbo-types (trace TurboFan's types)
        type: bool  default: true
  --trace-turbo-scheduler (trace TurboFan's scheduler)
        type: bool  default: false
  --trace-turbo-reduction (trace TurboFan's various reducers)
        type: bool  default: false
  --trace-turbo-trimming (trace TurboFan's graph trimmer)
        type: bool  default: false
  --trace-turbo-jt (trace TurboFan's jump threading)
        type: bool  default: false
  --trace-turbo-ceq (trace TurboFan's control equivalence)
        type: bool  default: false
  --trace-turbo-loop (trace TurboFan's loop optimizations)
        type: bool  default: false
  --trace-turbo-inlining (trace TurboFan inlining)
        type: bool  default: false
  --trace-turbo-load-elimination (trace TurboFan load elimination)
        type: bool  default: false

## Garbage Collection Debugging

  --trace-gc (print one trace line following each garbage collection)
        type: bool  default: false
  --trace-gc-nvp (print one detailed trace line in name=value format after each garbage collection)
        type: bool  default: false
  --trace-gc-ignore-scavenger (do not print trace line after scavenger collection)
        type: bool  default: false
  --trace-gc-verbose (print more details following each garbage collection)
        type: bool  default: false
  --trace-allocation-stack-interval (print stack trace after <n> free-list allocations)
        type: int  default: -1
  --trace-duplicate-threshold-kb (print duplicate objects in the heap if their size is more than given threshold)
        type: int  default: 0
  --trace-fragmentation (report fragmentation for old space)
        type: bool  default: false
  --trace-fragmentation-verbose (report fragmentation for old space (detailed))
        type: bool  default: false
  --trace-evacuation (report evacuation statistics)
        type: bool  default: false
  --trace-mutator-utilization (print mutator utilization, allocation speed, gc speed)
        type: bool  default: false
  --trace-unmapper (Trace the unmapping)
        type: bool  default: false
  --trace-parallel-scavenge (trace parallel scavenge)
        type: bool  default: false
  --trace-concurrent-marking (trace concurrent marking)
        type: bool  default: false
  --trace-incremental-marking (trace progress of the incremental marking)
        type: bool  default: false
  --trace-stress-marking (trace stress marking progress)
        type: bool  default: false
  --trace-stress-scavenge (trace stress scavenge progress)
        type: bool  default: false
  --trace-gc-object-stats (trace object counts and memory usage)
        type: bool  default: false
  --trace-zone-stats (trace zone memory usage)
        type: bool  default: false
  --trace-detached-contexts (trace native contexts that are expected to be garbage collected)
        type: bool  default: false
  --trace-minor-mc-parallel-marking (trace parallel marking for the young generation)
        type: bool  default: false

## asm.js Debugging

  --trace-asm-time (log asm.js timing info to the console)
        type: bool  default: false
  --trace-asm-scanner (log tokens encountered by asm.js scanner)
        type: bool  default: false
  --trace-asm-parser (verbose logging of asm.js parse failures)
        type: bool  default: false

## Wasm Debugging

  --trace-wasm-native-heap (trace wasm native heap events)
        type: bool  default: false
  --trace-wasm-serialization (trace serialization/deserialization)
        type: bool  default: false
  --trace-wasm-decoder (trace decoding of wasm code)
        type: bool  default: false
  --trace-wasm-compiler (trace compiling of wasm code)
        type: bool  default: false
  --trace-wasm-interpreter (trace interpretation of wasm code)
        type: bool  default: false
  --trace-wasm-streaming (trace streaming compilation of wasm code)
        type: bool  default: false
  --trace-wasm-ast-start (start function for wasm AST trace (inclusive))
        type: int  default: 0
  --trace-wasm-ast-end (end function for wasm AST trace (exclusive))
        type: int  default: 0
  --trace-liftoff (trace Liftoff, the baseline compiler for WebAssembly)
        type: bool  default: false
  --trace-wasm-memory (print all memory updates performed in wasm code)
        type: bool  default: false
  --trace-wasm-lazy-compilation (trace lazy compilation of wasm functions)
        type: bool  default: false
  --trace-wasm-code-gc (trace garbage collection of wasm code)
        type: bool  default: false
  --print-wasm-code (Print WebAssembly code)
        type: bool  default: false
  --print-wasm-stub-code (Print WebAssembly stub code)
        type: bool  default: false

### To Be Classified

  `--trace-pretenuring` (trace pretenuring decisions of HAllocate instructions)
        type: bool  default: false
  --trace-pretenuring-statistics (trace allocation site pretenuring statistics)
        type: bool  default: false
  --trace-block-coverage (trace collected block coverage information)
        type: bool  default: false
  --trace-track-allocation-sites (trace the tracking of allocation sites)
        type: bool  default: false
  --trace-migration (trace object migration)
        type: bool  default: false
  --trace-generalization (trace map generalization)
        type: bool  default: false
  --trace-concurrent-recompilation (track concurrent recompilation)
        type: bool  default: false
  --trace-heap-broker-verbose (trace the heap broker verbosely (all reports))
        type: bool  default: false
  --trace-heap-broker (trace the heap broker (reports on missing data only))
        type: bool  default: false
  --trace-alloc (trace register allocator)
        type: bool  default: false
  --trace-all-uses (trace all use positions)
        type: bool  default: false
  --trace-representation (trace representation types)
        type: bool  default: false
  --trace-verify-csa (trace code stubs verification)
        type: bool  default: false
  --trace-osr (trace on-stack replacement)
        type: bool  default: false
  --trace-environment-liveness (trace liveness of local variable slots)
        type: bool  default: false
  --trace-store-elimination (trace store elimination)
        type: bool  default: false
  --trace-idle-notification (print one trace line following each idle notification)
        type: bool  default: false
  --trace-idle-notification-verbose (prints the heap state used by the idle notification)
        type: bool  default: false
  --trace-opt (trace lazy optimization)
        type: bool  default: false
  --trace-opt-verbose (extra verbose compilation tracing)
        type: bool  default: false
  --trace-opt-stats (trace lazy optimization statistics)
        type: bool  default: false
  --trace-deopt (trace optimize function deoptimization)
        type: bool  default: false
  --trace-file-names (include file names in trace-opt/trace-deopt output)
        type: bool  default: false
  --trace-serializer (print code serializer trace)
        type: bool  default: false
  --trace-compiler-dispatcher (trace compiler dispatcher activity)
        type: bool  default: false
  --trace-side-effect-free-debug-evaluate (print debug messages for side-effect-free debug-evaluate for testing)
        type: bool  default: false
  --heap-profiler-trace-objects (Dump heap object allocations/movements/size_updates)
        type: bool  default: false
  --trace-ic (trace inline cache state transitions for tools/ic-processor)
        type: bool  default: false
  --trace-prototype-users (Trace updates to prototype user tracking)
        type: bool  default: false
  --trace-for-in-enumerate (Trace for-in enumerate slow-paths)
        type: bool  default: false
  --trace-maps (trace map creation)
        type: bool  default: false
  --trace-maps-details (also log map details)
        type: bool  default: true
  --trace-sim (Trace simulator execution)
        type: bool  default: false
  --trace-sim-messages (Trace simulator debug messages. Implied by --trace-sim.)
        type: bool  default: false
  --trace-rail (trace RAIL mode)
        type: bool  default: false

  --trace-contexts (trace contexts operations)
        type: bool  default: false
  --trace-turbo-escape (enable tracing in escape analysis)
        type: bool  default: false
  --trace-module-status (Trace status transitions of ECMAScript modules)
        type: bool  default: false
  --trace-normalization (prints when objects are turned into dictionaries.)
        type: bool  default: false
  --trace-lazy (trace lazy compilation)
        type: bool  default: false
  --trace-isolates (trace isolate state changes)
        type: bool  default: false
  --trace-regexp-bytecodes (trace regexp bytecode execution)
        type: bool  default: false
  --trace-regexp-assembler (trace regexp macro assembler calls.)
        type: bool  default: false
  --trace-regexp-parser (trace regexp parsing)
        type: bool  default: false
  --trace-wasm-instances (trace creation and collection of wasm instances)
        type: bool  default: false
  --trace-elements-transitions (trace elements transitions)
        type: bool  default: false
  --trace-creation-allocation-sites (trace the creation of allocation sites)
        type: bool  default: false
  --print-bytecode (print bytecode generated by ignition interpreter)
        type: bool  default: false
  --print-bytecode-filter (filter for selecting which functions to print bytecode)
        type: string  default: *
  --print-deopt-stress (print number of possible deopt points)
        type: bool  default: false

  --print-all-exceptions (print exception object and stack trace on each thrown exception)
        type: bool  default: false

  --print-scopes (print scopes)
        type: bool  default: false
  --print-handles (report handles after GC)
        type: bool  default: false
  --print-global-handles (report global handles after GC)
        type: bool  default: false
  --print-break-location (print source location on debug break)
        type: bool  default: false
  --print-opt-source (print source code of optimized and inlined functions)
        type: bool  default: false
  --print-code (print generated code)
        type: bool  default: false
  --print-opt-code (print optimized code)
        type: bool  default: false
  --print-opt-code-filter (filter for printing optimized code)
        type: string  default: *
  --print-code-verbose (print more information for code)
        type: bool  default: false
  --print-builtin-code (print generated code for builtins)
        type: bool  default: false
  --print-builtin-code-filter (filter for printing builtin code)
        type: string  default: *
  --print-builtin-size (print code size for builtins)
        type: bool  default: false
  --print-all-code (enable all flags related to printing code)
        type: bool  default: false
  --dump-wasm-module (dump wasm module bytes)
        type: bool  default: false
  --dump-wasm-module-path (directory to dump wasm modules to)
        type: string  default: nullptr
  --dump-counters (Dump counters on exit)
        type: bool  default: false
  --dump-counters-nvp (Dump counters as name-value pairs on exit)
        type: bool  default: false
  --log (Minimal logging (no API, code, GC, suspect, or handles samples).)
        type: bool  default: false
  --log-all (Log all events to the log file.)
        type: bool  default: false
  --log-api (Log API events to the log file.)
        type: bool  default: false
  --log-code (Log code events to the log file without profiling.)
        type: bool  default: false
  --log-handles (Log global handle events.)
        type: bool  default: false
  --log-suspect (Log suspect operations.)
        type: bool  default: false
  --log-source-code (Log source code.)
        type: bool  default: false
  --log-function-events (Log function events (parse, compile, execute) separately.)
        type: bool  default: false
