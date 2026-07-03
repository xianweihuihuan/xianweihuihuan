# xianweihuihuan

Computer Science undergraduate at Xi'an University of Posts and Telecommunications, focused on **system software** and **LLM inference infrastructure**.

Currently looking for **AI Infrastructure / LLM Inference Systems internship** opportunities, with a focus on KV Cache management, vLLM integration, cache offloading, transfer correctness, and runtime reliability.

## Current Focus

- LLM inference infrastructure and KV Cache systems
- KV Cache offloading / reuse for long-context serving
- vLLM, FlexKV, and vLLM V1 KV Connector integration
- GPU / CPU / SSD tiered cache and transfer paths
- Task lifecycle, ownership, shutdown, and reliability in runtime systems
- Learning CUDA / GPU systems, especially GPU ↔ CPU data movement

## Featured Work

### FlexKV upstream contributions

Contributed **7 merged PRs** to [`taco-project/FlexKV`](https://github.com/taco-project/FlexKV).

- [PR #187](https://github.com/taco-project/FlexKV/pull/187): addressed vLLM 0.23+ non-MLA KV layout changes that caused incorrect `num_blocks` detection, wrong stride calculation, and KV transfer corruption. Added the `LAYERBLOCK` layout and tensor-shape based detection for old/new layouts.
- [PR #184](https://github.com/taco-project/FlexKV/pull/184): addressed sub-task ownership / lifecycle leaks after batch `KVTask` merge. Moved ownership transfer into the batch merge stage and maintained batch result demux.
- Other fixes: early-return `KVTask` leaks in match / put flows, `slot_mapping` consistency, `TransferWorker` shutdown signaling, shared pool concurrency safety, and Mempool block id validation.

### MiniFlex

A KV Cache offloading and reuse system for vLLM.

- Supports GPU / CPU / SSD tiered KV Cache.
- Integrates with the vLLM V1 KV Connector.
- Separates logical cache management from physical transfer paths.
- Implements the GPU ↔ CPU transfer path and adapts to vLLM 0.23 KV layout changes.
- On my long-context benchmark workload: RTX 5090 32GB + Qwen3-8B + vLLM 0.23.
  - Around 30k context: TTFT reduced from ~3806 ms to ~408 ms, about **9.32x** faster.
  - When the working set exceeds GPU KV capacity, native vLLM APC reaches 100% miss; MiniFlex keeps 0% miss with TTFT around ~190 ms.

### [xianwei_OS](https://github.com/xianweihuihuan/xianwei_OS)

A 32-bit x86 teaching operating system project.

- Bootloader, protected mode, paging, interrupts, and system calls.
- Process / thread scheduling and file system support.
- `fork`, `exec`, `wait`, `exit`, pipe, and user-space programs.

## Systems Background

- Distributed systems: [MapReduce, KV service, Raft](https://github.com/xianweihuihuan/6.8540)
- Database internals: [Buffer Pool, B+Tree, PageGuard, DiskScheduler](https://github.com/xianweihuihuan/CMU15445)
- LLM inference study: [vLLM / PagedAttention notes and experiments](https://github.com/xianweihuihuan/nano-vllm-learn)
- CUDA / GPU systems learning: memory hierarchy, kernel basics, GPU ↔ CPU data movement, pinned memory, Roofline model

## Technical Stack

- Languages: C/C++, Python, Go
- Systems: Linux, Git, CMake, Bash
- LLM inference: vLLM, FlexKV, KV Cache, CUDA basics
- Foundations: operating systems, distributed systems, database internals

## Contact

- GitHub: [xianweihuihuan](https://github.com/xianweihuihuan)
- Email: xianweihuihuan@163.com
