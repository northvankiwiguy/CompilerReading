# Documentation on V8's Heap Mechanism

## TBDs
* Where in the code is an isolate's Heap object created?
* What are the main algorithms?

## Flags

* FLAG_stress_flush_bytecode - Used in GetBytecodeFlushMode()
* FLAG_flush_bytecode - Used in GetBytecodeFlushMode()
* FLAG_clear_free_memory - Used in ZapValue()
* FLAG_minor_mc - Used in YoungGenerationCollector()
* FLAG_trace_gc_freelists - Used in PrintFreeListsStats()
* FLAG_trace_gc_freelists_verbose - Used in PrintFreeListsStats()

## class Heap

* Top-level source code in `src/heap/heap.h` and `src/heap/heap.cc`

```
  EphemeronRememberedSet ephemeron_remembered_set_;
```

```
  enum FindMementoMode { kForRuntime, kForGC };
```

```
  enum class HeapGrowingMode { kSlow, kConservative, kMinimal, kDefault };
```

```
  enum HeapState {
    NOT_IN_GC,
    SCAVENGE,
    MARK_COMPACT,
    MINOR_MARK_COMPACT,
    TEAR_DOWN
  };
```
```
  using PretenuringFeedbackMap =
      std::unordered_map<AllocationSite, size_t, Object::Hasher>;
```

```
  // Taking this mutex prevents the GC from entering a phase that relocates
  // object references.
  base::Mutex* relocation_mutex() { return &relocation_mutex_; }
```

```
  // Support for partial snapshots.  After calling this we have a linear
  // space to write objects in each space.
  struct Chunk {
    uint32_t size;
    Address start;
    Address end;
  };
```

```
  using Reservation = std::vector<Chunk>;
```

```
  static const int kPointerMultiplier = i::kTaggedSize / 4;
```

```
  static const size_t kMaxInitialOldGenerationSize =
      256 * MB * kPointerMultiplier;
```

```
  // These constants control heap configuration based on the physical memory.
  static constexpr size_t kPhysicalMemoryToOldGenerationRatio = 4;
  static constexpr size_t kOldGenerationToSemiSpaceRatio = 128;
  static constexpr size_t kOldGenerationToSemiSpaceRatioLowMemory = 256;
  static constexpr size_t kOldGenerationLowMemory =
      128 * MB * kPointerMultiplier;
  static constexpr size_t kNewLargeObjectSpaceToSemiSpaceRatio = 1;
  static constexpr size_t kMinSemiSpaceSize = 512 * KB * kPointerMultiplier;
  static constexpr size_t kMaxSemiSpaceSize = 8192 * KB * kPointerMultiplier;
```

```
  static const int kTraceRingBufferSize = 512;
  static const int kStacktraceBufferSize = 512;
```

```
  static const int kNoGCFlags = 0;
```

```
  static const int kReduceMemoryFootprintMask = 1;
```

```
  // The minimum size of a HeapObject on the heap.
  static const int kMinObjectSizeInTaggedWords = 2;
```

```
  static const int kMinPromotedPercentForFastPromotionMode = 90;
```

```
  // Calculates the maximum amount of filler that could be required by the
  // given alignment.
  static int GetMaximumFillToAlign(AllocationAlignment alignment);
```

```
  // Calculates the actual amount of filler required for a given address at the
  // given alignment.
  static int GetFillToAlign(Address address, AllocationAlignment alignment);
```

```
  // Returns the size of the initial area of a code-range, which is marked
  // writable and reserved to contain unwind information.
  static size_t GetCodeRangeReservedAreaSize();
```

```
  void FatalProcessOutOfMemory(const char* location);
```

```
  // Checks whether the space is valid.
  static bool IsValidAllocationSpace(AllocationSpace space);
```
```
  // Zapping is needed for verify heap, and always done in debug builds.
  static inline bool ShouldZapGarbage() { ... }
```
```
  // Helper function to get the bytecode flushing mode based on the flags. This
  // is required because it is not safe to acess flags in concurrent marker.
  static inline BytecodeFlushMode GetBytecodeFlushMode() { ... }
```
```
  static uintptr_t ZapValue() { ... }
```

```
  static inline bool IsYoungGenerationCollector(GarbageCollector collector) { ... }
```

```
  static inline GarbageCollector YoungGenerationCollector() { ... }
```

```
  static inline const char* CollectorName(GarbageCollector collector) { ... }
```

```
  // Copy block of memory from src to dst. Size of block should be aligned
  // by pointer size.
  static inline void CopyBlock(Address dst, Address src, int byte_size);
```

```
  // Executes generational and/or marking write barrier for a [start, end) range
  // of non-weak slots inside |object|.
  template <typename TSlot>
  void WriteBarrierForRange(HeapObject object, TSlot start, TSlot end);
```

```
  static void WriteBarrierForCodeSlow(Code host);
```

```
  static void GenerationalBarrierSlow(
    HeapObject object, Address slot, HeapObject value);
```

```
  inline void RecordEphemeronKeyWrite(EphemeronHashTable table, Address key_slot);
```

```
  static void EphemeronKeyWriteBarrierFromCode(
      Address raw_object, Address address, Isolate* isolate);
```

```
  static void GenerationalBarrierForCodeSlow(
      Code host, RelocInfo* rinfo, HeapObject value);
```

```
  static void MarkingBarrierSlow(
    HeapObject object, Address slot, HeapObject value);
```
```
  static void MarkingBarrierForCodeSlow(
    Code host, RelocInfo* rinfo, HeapObject value);
```
```
  static void MarkingBarrierForDescriptorArraySlow(
      Heap* heap, HeapObject host, HeapObject descriptor_array,
      int number_of_own_descriptors);
```
```
  static bool PageFlagsAreConsistent(HeapObject object);
```

```
  // Notifies the heap that is ok to start marking or other activities that
  // should not happen during deserialization.
  void NotifyDeserializationComplete();
```
```
  void NotifyBootstrapComplete();
```

```
  void NotifyOldGenerationExpansion();
```

```
  inline Address* NewSpaceAllocationTopAddress();
  inline Address* NewSpaceAllocationLimitAddress();
  inline Address* OldSpaceAllocationTopAddress();
  inline Address* OldSpaceAllocationLimitAddress();
```
```
  // Move len non-weak tagged elements from src_slot to dst_slot of dst_object.
  // The source and destination memory ranges can overlap.
  void MoveRange(HeapObject dst_object, ObjectSlot dst_slot,
                 ObjectSlot src_slot, int len, WriteBarrierMode mode);
```

```
  // Copy len non-weak tagged elements from src_slot to dst_slot of dst_object.
  // The source and destination memory ranges must not overlap.
  template <typename TSlot>
  void CopyRange(HeapObject dst_object, TSlot dst_slot, TSlot src_slot, int len,
                 WriteBarrierMode mode);
```

```
  // Initialize a filler object to keep the ability to iterate over the heap
  // when introducing gaps within pages. If slots could have been recorded in
  // the freed area, then pass ClearRecordedSlots::kYes as the mode. Otherwise,
  // pass ClearRecordedSlots::kNo. If the memory after the object header of
  // the filler should be cleared, pass in kClearFreedMemory. The default is
  // kDontClearFreedMemory.
  HeapObject CreateFillerObjectAt(
      Address addr, int size, ClearRecordedSlots clear_slots_mode,
      ClearFreedMemoryMode clear_memory_mode =
          ClearFreedMemoryMode::kDontClearFreedMemory);
```

```
  template <typename T>
  void CreateFillerForArray(T object, int elements_to_trim, int bytes_to_trim);
```

```
  bool CanMoveObjectStart(HeapObject object);
```

```
  bool IsImmovable(HeapObject object);
```

```
  static bool IsLargeObject(HeapObject object);
```

```
  // Trim the given array from the left. Note that this relocates the object
  // start and hence is only valid if there is only a single reference to it.
  FixedArrayBase LeftTrimFixedArray(FixedArrayBase obj,
                                                      int elements_to_trim);
```

```
  // Trim the given array from the right.
  void RightTrimFixedArray(FixedArrayBase obj,
                                             int elements_to_trim);
```
```
  void RightTrimWeakFixedArray(WeakFixedArray obj, int elements_to_trim);
```
```
  // Converts the given boolean condition to JavaScript boolean value.
  inline Oddball ToBoolean(bool condition);
```

```
  // Notify the heap that a context has been disposed.
  int NotifyContextDisposed(bool dependant_context);
```

```
  void set_native_contexts_list(Object object) { ... }
```

```
  Object native_contexts_list() const { ... }
```

```
  void set_allocation_sites_list(Object object) { ... }
```

```
  Object allocation_sites_list() { ... }
```

```
  // Used in CreateAllocationSiteStub and the (de)serializer.
  Address allocation_sites_list_address() { ... }
```

```
  // Traverse all the allocaions_sites [nested_site and weak_next] in the list
  // and foreach call the visitor
  void ForeachAllocationSite(
      Object list, const std::function<void(AllocationSite)>& visitor);
```

```
  // Number of mark-sweeps.
  int ms_count() const { ... }
```

```
  // Checks whether the given object is allowed to be migrated from it's
  // current space into the given destination space. Used for debugging.
  bool AllowedToBeMigrated(Map map, HeapObject object, AllocationSpace dest);
```

```
  void CheckHandleCount();
```

```
  // Number of "runtime allocations" done so far.
  uint32_t allocations_count() { return allocations_count_; }
```

```
  // Print short heap statistics.
  void PrintShortHeapStatistics();
```

```
  // Print statistics of freelists of old_space:
  //  with FLAG_trace_gc_freelists: summary of each FreeListCategory.
  //  with FLAG_trace_gc_freelists_verbose: also prints the statistics of each
  //  FreeListCategory of each page.
  void PrintFreeListsStats();
```

```
  // Dump heap statistics in JSON format.
  void DumpJSONHeapStatistics(std::stringstream& stream);
```

```
  bool write_protect_code_memory() const { return write_protect_code_memory_; }
```

```
  uintptr_t code_space_memory_modification_scope_depth() { ... }
```

```
  void increment_code_space_memory_modification_scope_depth() { ... }
```

```
  void decrement_code_space_memory_modification_scope_depth() { ... }
```

```
  void UnprotectAndRegisterMemoryChunk(MemoryChunk* chunk);
  void UnprotectAndRegisterMemoryChunk(HeapObject object);
  void UnregisterUnprotectedMemoryChunk(MemoryChunk* chunk);
  void ProtectUnprotectedMemoryChunks();
```

```
  void EnableUnprotectedMemoryChunksRegistry() { ... }
```

```
  void DisableUnprotectedMemoryChunksRegistry() { ... }
```

```
  bool unprotected_memory_chunks_registry_enabled() { ... }
```

```
  inline HeapState gc_state() { return gc_state_; }
  void SetGCState(HeapState state);
```

```
  bool IsTearingDown() const { ... }
```

```
  inline bool IsInGCPostProcessing() { ... }
```

```
  // If an object has an AllocationMemento trailing it, return it, otherwise
  // return a null AllocationMemento.
  template <FindMementoMode mode>
  inline AllocationMemento FindAllocationMemento(Map map, HeapObject object);
```

```
  // Returns false if not able to reserve.
  bool ReserveSpace(Reservation* reservations, std::vector<Address>* maps);
```

  ### Support for the V8 API

```
  void CreateApiObjects();
```

```
  // Implements the corresponding V8 API function.
  bool IdleNotification(double deadline_in_seconds);
  bool IdleNotification(int idle_time_in_ms);
```

```
  void MemoryPressureNotification(MemoryPressureLevel level,
                                                    bool is_isolate_locked);
```

```
  void CheckMemoryPressure();
```

```
  void AddNearHeapLimitCallback(v8::NearHeapLimitCallback,
                                                  void* data);
```
```
  void RemoveNearHeapLimitCallback(
      v8::NearHeapLimitCallback callback, size_t heap_limit);
```
```
  void AutomaticallyRestoreInitialHeapLimit(
      double threshold_percent);
```
```
  double MonotonicallyIncreasingTimeInMs();
```
```
  void RecordStats(HeapStats* stats, bool take_snapshot = false);
```
```
  Handle<JSPromise> MeasureMemory(Handle<NativeContext> context,
                                  v8::MeasureMemoryMode mode);
```

```
  // Check new space expansion criteria and expand semispaces if it was hit.
  void CheckNewSpaceExpansionCriteria();
```

```
  void VisitExternalResources(v8::ExternalResourceVisitor* visitor);
```

```
  // An object should be promoted if the object has survived a
  // scavenge operation.
  inline bool ShouldBePromoted(Address old_address);
```
```
  void IncrementDeferredCount(v8::Isolate::UseCounterFeature feature);
```

```
  inline int NextScriptId();
  inline int NextDebuggingId();
  inline int GetNextTemplateSerialNumber();
```
```
  void SetSerializedObjects(FixedArray objects);
  void SetSerializedGlobalProxySizes(FixedArray sizes);
```

```
  // For post mortem debugging.
  void RememberUnmappedPage(Address page, bool compacted);
```

```
  int64_t external_memory_hard_limit() { ... }

  int64_t external_memory();
  void update_external_memory(int64_t delta);
  void update_external_memory_concurrently_freed(uintptr_t freed);
  void account_external_memory_concurrently_freed();
```

```
  size_t backing_store_bytes() const { return backing_store_bytes_; }
```

```
  void CompactWeakArrayLists(AllocationType allocation);
```

```
  void AddRetainedMap(Handle<Map> map);
```

```
  // This event is triggered after successful allocation of a new object made
  // by runtime. Allocations of target space for object evacuation do not
  // trigger the event. In order to track ALL allocations one must turn off
  // FLAG_inline_new.
  inline void OnAllocationEvent(HeapObject object, int size_in_bytes);
```

```
  // This event is triggered after object is moved to a new place.
  void OnMoveEvent(HeapObject target, HeapObject source, int size_in_bytes);
```

```
  inline bool CanAllocateInReadOnlySpace();
```
```
  bool deserialization_complete() const { ... }
```
```
  bool HasLowAllocationRate();
```

```
  bool HasHighFragmentation();
  bool HasHighFragmentation(size_t used, size_t committed);
```

```
  void ActivateMemoryReducerIfNeeded();
```

```
  bool ShouldOptimizeForMemoryUsage();
```

```
  bool HighMemoryPressure() { ... }
```

```
  void RestoreHeapLimit(size_t heap_limit) { ... }
```

### Initialization Methods

```
  void ConfigureHeap(const v8::ResourceConstraints& constraints);
  void ConfigureHeapDefault();
```

```
  // Prepares the heap, setting up for deserialization.
  void SetUp();
```

```
  // Sets read-only heap and space.
  void SetUpFromReadOnlyHeap(ReadOnlyHeap* ro_heap);
```

```
  // Sets up the heap memory without creating any objects.
  void SetUpSpaces();
```

```
  // (Re-)Initialize hash seed from flag or RNG.
  void InitializeHashSeed();
```

```
  // Bootstraps the object heap with the core set of objects required to run.
  // Returns whether it succeeded.
  bool CreateHeapObjects();
```

```
  // Create ObjectStats if live_object_stats_ or dead_object_stats_ are nullptr.
  void CreateObjectStats();
```

```
  // Sets the TearDown state, so no new GC tasks get posted.
  void StartTearDown();
```

```
  // Destroys all memory allocated by the heap.
  void TearDown();
```

```
  // Returns whether SetUp has been called.
  bool HasBeenSetUp();
```

### Getters for Spaces

```
  inline Address NewSpaceTop();
```

```
  NewSpace* new_space() { return new_space_; }
  OldSpace* old_space() { return old_space_; }
  CodeSpace* code_space() { return code_space_; }
  MapSpace* map_space() { return map_space_; }
  OldLargeObjectSpace* lo_space() { return lo_space_; }
  CodeLargeObjectSpace* code_lo_space() { return code_lo_space_; }
  NewLargeObjectSpace* new_lo_space() { return new_lo_space_; }
  ReadOnlySpace* read_only_space() { return read_only_space_; }
```

```
  inline PagedSpace* paged_space(int idx);
  inline Space* space(int idx);
```

```
  // Returns name of the space.
  static const char* GetSpaceName(AllocationSpace space);
```

### Getters to Other Components

```
  GCTracer* tracer() { return tracer_.get(); }
```

```
  MemoryAllocator* memory_allocator() { return memory_allocator_.get(); }
```

```
  inline Isolate* isolate();
```

```
  MarkCompactCollector* mark_compact_collector() { ... }
```

```
  MinorMarkCompactCollector* minor_mark_compact_collector() { ... }
```
```
  ArrayBufferCollector* array_buffer_collector() { ... }
```

### Root Set Access

```
  // Shortcut to the roots table stored in the Isolate.
  RootsTable& roots_table();
```

```
// Heap root getters.
\#define ROOT_ACCESSOR(type, name, CamelName) inline type name();
  MUTABLE_ROOT_LIST(ROOT_ACCESSOR)
\#undef ROOT_ACCESSOR
```

```
  void SetRootMaterializedObjects(FixedArray objects);
  void SetRootScriptList(Object value);
  void SetRootStringTable(StringTable value);
  void SetRootNoScriptSharedFunctionInfos(Object value);
  void SetMessageListeners(TemplateList value);
  void SetPendingOptimizeForTestBytecode(Object bytecode);
```

```
  void RegisterStrongRoots(FullObjectSlot start, FullObjectSlot end);
  void UnregisterStrongRoots(FullObjectSlot start);
```

```
  void SetBuiltinsConstantsTable(FixedArray cache);
```

```
  // A full copy of the interpreter entry trampoline, used as a template to
  // create copies of the builtin at runtime. The copies are used to create
  // better profiling information for ticks in bytecode execution. Note that
  // this is always a copy of the full builtin, i.e. not the off-heap
  // trampoline.
  // See also: FLAG_interpreted_frames_native_stack.
  void SetInterpreterEntryTrampolineForProfiling(Code code);
```

```
  // Add finalization_group into the dirty_js_finalization_groups list.
  void AddDirtyJSFinalizationGroup(
      JSFinalizationGroup finalization_group,
      std::function<void(HeapObject object, ObjectSlot slot, Object target)>
          gc_notify_updated_slot);
```

```
  void KeepDuringJob(Handle<JSReceiver> target);
```

```
  void ClearKeptObjects();
```

### Inline Allocation

```
  // Indicates whether inline bump-pointer allocation has been disabled.
  bool inline_allocation_disabled() { return inline_allocation_disabled_; }
```

```
  // Switch whether inline bump-pointer allocation should be used.
  void EnableInlineAllocation();
  void DisableInlineAllocation();
```

### Methods that Trigger GCs

```
  // Performs garbage collection operation.
  // Returns whether there is a chance that another major GC could
  // collect more garbage.
  bool CollectGarbage(
      AllocationSpace space, GarbageCollectionReason gc_reason,
      const GCCallbackFlags gc_callback_flags = kNoGCCallbackFlags);
```

```
  // Performs a full garbage collection.
  void CollectAllGarbage(
      int flags, GarbageCollectionReason gc_reason,
      const GCCallbackFlags gc_callback_flags = kNoGCCallbackFlags);
```

```
  // Last hope GC, should try to squeeze as much as possible.
  void CollectAllAvailableGarbage(
      GarbageCollectionReason gc_reason);
```

```
  // Precise garbage collection that potentially finalizes already running
  // incremental marking before performing an atomic garbage collection.
  // Only use if absolutely necessary or in tests to avoid floating garbage!
  void PreciseCollectAllGarbage(
      int flags, GarbageCollectionReason gc_reason,
      const GCCallbackFlags gc_callback_flags = kNoGCCallbackFlags);
```
```
  // Reports and external memory pressure event, either performs a major GC or
  // completes incremental marking in order to free external resources.
  void ReportExternalMemoryPressure();
```

```
  using GetExternallyAllocatedMemoryInBytesCallback =
      v8::Isolate::GetExternallyAllocatedMemoryInBytesCallback;
```

```
  void SetGetExternallyAllocatedMemoryInBytesCallback(
      GetExternallyAllocatedMemoryInBytesCallback callback) { ... }
```

```
  // Invoked when GC was requested via the stack guard.
  void HandleGCRequest();
```

### Builtins

```
  Code builtin(int index);
  Address builtin_address(int index);
  void set_builtin(int index, Code builtin);
```

### Iterators

```
  // None of these methods iterate over the read-only roots. To do this use
  // ReadOnlyRoots::Iterate. Read-only root iteration is not necessary for
  // garbage collection and is usually only performed as part of
  // (de)serialization or heap verification.
```

```
  // Iterates over the strong roots and the weak roots.
  void IterateRoots(RootVisitor* v, VisitMode mode);
```

```
  // Iterates over the strong roots.
  void IterateStrongRoots(RootVisitor* v, VisitMode mode);
```

```
  // Iterates over entries in the smi roots list.  Only interesting to the
  // serializer/deserializer, since GC does not care about smis.
  void IterateSmiRoots(RootVisitor* v);
```

```
  // Iterates over weak string tables.
  void IterateWeakRoots(RootVisitor* v, VisitMode mode);
```

```
  // Iterates over weak global handles.
  void IterateWeakGlobalHandles(RootVisitor* v);
```

```
  // Iterates over builtins.
  void IterateBuiltins(RootVisitor* v);
```

### Store Buffer API

```
  // Used for query incremental marking status in generated code.
  Address* IsMarkingFlagAddress() { ... }
```

```
  void SetIsMarkingFlag(uint8_t flag) { ... }
```

```
  Address* store_buffer_top_address();
  static intptr_t store_buffer_mask_constant();
  static Address store_buffer_overflow_function_address();
```

```
  void ClearRecordedSlot(HeapObject object, ObjectSlot slot);
  void ClearRecordedSlotRange(Address start, Address end);
  static int InsertIntoRememberedSetFromCode(MemoryChunk* chunk, Address slot);
```

```
  void VerifyClearedSlot(HeapObject object, ObjectSlot slot);
```

### Incremental Marking API

```
  int GCFlagsForIncrementalMarking() { ... }
```

```
  // Start incremental marking and ensure that idle time handler can perform
  // incremental steps.
  void StartIdleIncrementalMarking(
      GarbageCollectionReason gc_reason,
      GCCallbackFlags gc_callback_flags = GCCallbackFlags::kNoGCCallbackFlags);
```

```
  // Starts incremental marking assuming incremental marking is currently
  // stopped.
  void StartIncrementalMarking(
      int gc_flags, GarbageCollectionReason gc_reason,
      GCCallbackFlags gc_callback_flags = GCCallbackFlags::kNoGCCallbackFlags);
```

```
  void StartIncrementalMarkingIfAllocationLimitIsReached(
      int gc_flags,
      GCCallbackFlags gc_callback_flags = GCCallbackFlags::kNoGCCallbackFlags);
```

```
  void FinalizeIncrementalMarkingIfComplete(GarbageCollectionReason gc_reason);
```

```
  // Synchronously finalizes incremental marking.
  void FinalizeIncrementalMarkingAtomically(GarbageCollectionReason gc_reason);
```

```
  void RegisterDeserializedObjectsForBlackAllocation(
      Reservation* reservations, const std::vector<HeapObject>& large_objects,
      const std::vector<Address>& maps);
```

```
  IncrementalMarking* incremental_marking() { ... }
```

### Concurrent Marking API

```
  ConcurrentMarking* concurrent_marking() { ... }
```

```
  // The runtime uses this function to notify potentially unsafe object layout
  // changes that require special synchronization with the concurrent marker.
  // The old size is the size of the object before layout change.
  // By default recorded slots in the object are invalidated. Pass
  // InvalidateRecordedSlots::kNo if this is not necessary or to perform this
  // manually.
  void NotifyObjectLayoutChange(
      HeapObject object, const DisallowHeapAllocation&,
      InvalidateRecordedSlots invalidate_recorded_slots =
          InvalidateRecordedSlots::kYes);
```

```
  // This function checks that either
  // - the map transition is safe,
  // - or it was communicated to GC using NotifyObjectLayoutChange.
  void VerifyObjectLayoutChange(HeapObject object,
                                                  Map new_map);
```

### Deoptimization Support API

```
  // Setters for code offsets of well-known deoptimization targets.
  void SetArgumentsAdaptorDeoptPCOffset(int pc_offset);
  void SetConstructStubCreateDeoptPCOffset(int pc_offset);
  void SetConstructStubInvokeDeoptPCOffset(int pc_offset);
  void SetInterpreterEntryReturnPCOffset(int pc_offset);
```

```
  // Invalidates references in the given {code} object that are referenced
  // transitively from the deoptimization data. Mutates write-protected code.
  void InvalidateCodeDeoptimizationData(Code code);
```

```
  void DeoptMarkedAllocationSites();
```

```
  bool DeoptMaybeTenuredAllocationSites();
```

### Embedder Heap Tracer Support

```
  LocalEmbedderHeapTracer* local_embedder_heap_tracer() const { ... }
```

```
  void SetEmbedderHeapTracer(EmbedderHeapTracer* tracer);
  EmbedderHeapTracer* GetEmbedderHeapTracer() const;
```

```
  void RegisterExternallyReferencedObject(Address* location);
```
```
  void SetEmbedderStackStateForNextFinalizaton(
      EmbedderHeapTracer::EmbedderStackState stack_state);
```
```
  EmbedderHeapTracer::TraceFlags flags_for_embedder_tracer() const;
```

### External String Table API

```
  // Registers an external string.
  inline void RegisterExternalString(String string);
```

```
  // Called when a string's resource is changed. The size of the payload is sent
  // as argument of the method.
  void UpdateExternalString(String string, size_t old_payload,
                                              size_t new_payload);
```

```
  // Finalizes an external string by deleting the associated external
  // data and clearing the resource pointer.
  inline void FinalizeExternalString(String string);
```

```
  static String UpdateYoungReferenceInExternalStringTableEntry(
      Heap* heap, FullObjectSlot pointer);
```

### Methods Checking/Returning the Space of a Given Object/Address

```
  // Returns whether the object resides in new space.
  static inline bool InYoungGeneration(Object object);
  static inline bool InYoungGeneration(MaybeObject object);
  static inline bool InYoungGeneration(HeapObject heap_object);
  static inline bool InFromPage(Object object);
  static inline bool InFromPage(MaybeObject object);
  static inline bool InFromPage(HeapObject heap_object);
  static inline bool InToPage(Object object);
  static inline bool InToPage(MaybeObject object);
  static inline bool InToPage(HeapObject heap_object);
```

```
  // Returns whether the object resides in old space.
  inline bool InOldSpace(Object object);
```

```
  // Checks whether an address/object is in the non-read-only heap (including
  // auxiliary area and unused area). Use IsValidHeapObject if checking both
  // heaps is required.
  bool Contains(HeapObject value);
```

```
  // Checks whether an address/object in a space.
  // Currently used by tests, serialization and heap verification only.
  bool InSpace(HeapObject value, AllocationSpace space);
```
```
  // Slow methods that can be used for verification as they can also be used
  // with off-heap Addresses.
  bool InSpaceSlow(Address addr, AllocationSpace space);
```
```
  static inline Heap* FromWritableHeapObject(HeapObject obj);
```

### Object Statistics Tracking

```
  // Returns the number of buckets used by object statistics tracking during a
  // major GC. Note that the following methods fail gracefully when the bounds
  // are exceeded though.
  size_t NumberOfTrackedHeapObjectTypes();
```

```
  // Returns object statistics about count and size at the last major GC.
  // Objects are being grouped into buckets that roughly resemble existing
  // instance types.
  size_t ObjectCountAtLastGC(size_t index);
  size_t ObjectSizeAtLastGC(size_t index);
```

```
  // Retrieves names of buckets used by object statistics tracking.
  bool GetObjectTypeName(size_t index, const char** object_type,
                         const char** object_sub_type);
```

```
  // The total number of native contexts object on the heap.
  size_t NumberOfNativeContexts();
```

```
  // The total number of native contexts that were detached but were not
  // garbage collected yet.
  size_t NumberOfDetachedContexts();
```

### Code Statistics

```
  // Collect code (Code and BytecodeArray objects) statistics.
  void CollectCodeStatistics();
```

### GC Statistics

```
  // Returns the maximum amount of memory reserved for the heap.
  size_t MaxReserved();
  size_t MaxSemiSpaceSize() { return max_semi_space_size_; }
  size_t InitialSemiSpaceSize() { return initial_semispace_size_; }
  size_t MaxOldGenerationSize() { return max_old_generation_size_; }
```

```
  static size_t HeapSizeFromPhysicalMemory(
      uint64_t physical_memory);
```

```
  static void GenerationSizesFromHeapSize(
      size_t heap_size, size_t* young_generation_size,
      size_t* old_generation_size);
```
```
  static size_t YoungGenerationSizeFromOldGenerationSize(
      size_t old_generation_size);
```
```
  static size_t YoungGenerationSizeFromSemiSpaceSize(
      size_t semi_space_size);
```
```
  static size_t SemiSpaceSizeFromYoungGenerationSize(
      size_t young_generation_size);
```
```
  static size_t MinYoungGenerationSize();
  static size_t MinOldGenerationSize();
  static size_t MaxOldGenerationSize(
      uint64_t physical_memory);
```

```
  // Returns the capacity of the heap in bytes w/o growing. Heap grows when
  // more spaces are needed until it reaches the limit.
  size_t Capacity();
```
```
  // Returns the capacity of the old generation.
  size_t OldGenerationCapacity();
```
```
  // Returns the amount of memory currently held alive by the unmapper.
  size_t CommittedMemoryOfUnmapper();
```
```
  // Returns the amount of memory currently committed for the heap.
  size_t CommittedMemory();
```
```
  // Returns the amount of memory currently committed for the old space.
  size_t CommittedOldGenerationMemory();
```
```
  // Returns the amount of executable memory currently committed for the heap.
  size_t CommittedMemoryExecutable();
```
```
  // Returns the amount of phyical memory currently committed for the heap.
  size_t CommittedPhysicalMemory();
```
```
  // Returns the maximum amount of memory ever committed for the heap.
  size_t MaximumCommittedMemory() { return maximum_committed_; }
```
```
  // Updates the maximum committed memory for the heap. Should be called
  // whenever a space grows.
  void UpdateMaximumCommitted();
```
```
  // Returns the available bytes in space w/o growing.
  // Heap doesn't guarantee that it can allocate an object that requires
  // all available bytes. Check MaxHeapObjectSize() instead.
  size_t Available();
```
```
  // Returns of size of all objects residing in the heap.
  size_t SizeOfObjects();
```
```
  void UpdateSurvivalStatistics(int start_new_space_size);
```
```
  inline void IncrementPromotedObjectsSize(size_t object_size) { ... }
```
```
  inline size_t promoted_objects_size() { ... }
```
```
  inline void IncrementSemiSpaceCopiedObjectSize(size_t object_size) { ... }
```

```
  inline size_t semi_space_copied_object_size() { ... }
```

```
  inline size_t SurvivedYoungObjectSize() { ... }
```

```
  inline void IncrementNodesDiedInNewSpace() { ... }
  inline void IncrementNodesCopiedInNewSpace() { ... }
  inline void IncrementNodesPromoted() { ... }
```

```
  inline void IncrementYoungSurvivorsCounter(size_t survived) { ... }
```

```
  inline uint64_t OldGenerationObjectsAndPromotedExternalMemorySize() { ... }
```

```
  inline void UpdateNewSpaceAllocationCounter();
```

```
  inline size_t NewSpaceAllocationCounter();
```

```
  // This should be used only for testing.
  void set_new_space_allocation_counter(size_t new_value) { ... }
```

```
  void UpdateOldGenerationAllocationCounter() { ... }
```

```
  size_t OldGenerationAllocationCounter() { ... }
```

```
  size_t EmbedderAllocationCounter() const;
```

```
  // This should be used only for testing.
  void set_old_generation_allocation_counter_at_last_gc(size_t new_value) { ... }
```

```
  size_t PromotedSinceLastGC() { ... }
```

```
  // This is called by the sweeper when it discovers more free space
  // than expected at the end of the preceding GC.
  void NotifyRefinedOldGenerationSize(size_t decreased_bytes) { ... }
```

```
  int gc_count() const { ... }
```

```
  bool is_current_gc_forced() const { ... }
```

```
  // Returns the size of objects residing in non-new spaces.
  // Excludes external memory held by those objects.
  size_t OldGenerationSizeOfObjects();
```

```
  size_t GlobalSizeOfObjects();
```

```
  // We allow incremental marking to overshoot the V8 and global allocation
  // limit for performace reasons. If the overshoot is too large then we are
  // more eager to finalize incremental marking.
  bool AllocationLimitOvershotByLargeMargin();
```

### Prologue/Epilogue Callback Methods

```
  void AddGCPrologueCallback(v8::Isolate::GCCallbackWithData callback,
                             GCType gc_type_filter, void* data);
  void RemoveGCPrologueCallback(v8::Isolate::GCCallbackWithData callback,
                                void* data);
```

```
  void AddGCEpilogueCallback(v8::Isolate::GCCallbackWithData callback,
                             GCType gc_type_filter, void* data);
  void RemoveGCEpilogueCallback(v8::Isolate::GCCallbackWithData callback,
                                void* data);
```

```
  void CallGCPrologueCallbacks(GCType gc_type, GCCallbackFlags flags);
  void CallGCEpilogueCallbacks(GCType gc_type, GCCallbackFlags flags);
```

### Allocation Methods

```
  // Creates a filler object and returns a heap object immediately after it.
  HeapObject PrecedeWithFiller(HeapObject object, int filler_size);
```

```
  // Creates a filler object if needed for alignment and returns a heap object
  // immediately after it. If any space is left after the returned object,
  // another filler object is created so the over allocated memory is iterable.
  HeapObject AlignWithFiller(HeapObject object, int object_size, int allocation_size,
                  AllocationAlignment alignment);
```

```
  // Allocate an external backing store with the given allocation callback.
  // If the callback fails (indicated by a nullptr result) then this function
  // will re-try the allocation after performing GCs. This is useful for
  // external backing stores that may be retained by (unreachable) V8 objects
  // such as ArrayBuffers, ExternalStrings, etc.
  //
  // The function may also proactively trigger GCs even if the allocation
  // callback does not fail to keep the memory usage low.
  void* AllocateExternalBackingStore(
      const std::function<void*(size_t)>& allocate, size_t byte_length);
```

### ArrayBuffer Tracking

```
  void RegisterBackingStore(JSArrayBuffer buffer,
                            std::shared_ptr<BackingStore> backing_store);
  std::shared_ptr<BackingStore> UnregisterBackingStore(JSArrayBuffer buffer);
  std::shared_ptr<BackingStore> LookupBackingStore(JSArrayBuffer buffer);
```

### Allocation Site Tracking

```
  // Updates the AllocationSite of a given {object}. The entry (including the
  // count) is cached on the local pretenuring feedback.
  inline void UpdateAllocationSite(
      Map map, HeapObject object, PretenuringFeedbackMap* pretenuring_feedback);
```

```
  // Merges local pretenuring feedback into the global one. Note that this
  // method needs to be called after evacuation, as allocation sites may be
  // evacuated and this method resolves forward pointers accordingly.
  void MergeAllocationSitePretenuringFeedback(
      const PretenuringFeedbackMap& local_pretenuring_feedback);
```

### Allocation Tracking

```
  // Adds {new_space_observer} to new space and {observer} to any other space.
  void AddAllocationObserversToAllSpaces(
      AllocationObserver* observer, AllocationObserver* new_space_observer);
```

```
  // Removes {new_space_observer} from new space and {observer} from any other
  // space.
  void RemoveAllocationObserversFromAllSpaces(
      AllocationObserver* observer, AllocationObserver* new_space_observer);
```

```
  bool allocation_step_in_progress() { ... }
```

```
  void set_allocation_step_in_progress(bool val) { ... }
```

### Heap object allocation tracking

```
  void AddHeapObjectAllocationTracker(HeapObjectAllocationTracker* tracker);
```
```
  void RemoveHeapObjectAllocationTracker(HeapObjectAllocationTracker* tracker);
```
```
  bool has_heap_object_allocation_tracker() const { ... }
```

### Retaining-Path Tracking

```
  // Adds the given object to the weak table of retaining path targets.
  // On each GC if the marker discovers the object, it will print the retaining
  // path. This requires --track-retaining-path flag.
  void AddRetainingPathTarget(Handle<HeapObject> object,
                              RetainingPathOption option);
```

### Stack Frame Support

```
  // Returns the Code object for a given interior pointer.
  Code GcSafeFindCodeForInnerPointer(Address inner_pointer);
```

```
  // Returns true if {addr} is contained within {code} and false otherwise.
  // Mostly useful for debugging.
  bool GcSafeCodeContains(Code code, Address addr);
```

```
  // Casts a heap object to a code object and checks if the inner_pointer is
  // within the object.
  Code GcSafeCastToCode(HeapObject object, Address inner_pointer);
```

```
  // Returns the map of an object. Can be used during garbage collection, i.e.
  // it supports a forwarded map. Fails if the map is not the code map.
  Map GcSafeMapOfCodeSpaceObject(HeapObject object);
```

// =============================================================================
  
```  
  // Verify the heap is in its normal state before or after a GC.
  void Verify();
```

```
  // Verify the read-only heap after all read-only heap objects have been
  // created.
  void VerifyReadOnlyHeap();
  void VerifyRememberedSetFor(HeapObject object);
```

```
  void set_allocation_timeout(int timeout) { ... }
```

```
  void VerifyCountersAfterSweeping();
  void VerifyCountersBeforeConcurrentSweeping();
```

```
  void Print();
  void PrintHandles();
```

```
  // Report code statistics.
  void ReportCodeStatistics(const char* title);
```

```
  void* GetRandomMmapAddr() { ... }
```

```
  static const char* GarbageCollectionReasonToString(
      GarbageCollectionReason gc_reason);
```

```
  // Calculates the nof entries for the full sized number to string cache.
  inline int MaxNumberToStringCacheSize() const;
```