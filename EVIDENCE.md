# Selected evidence and provenance

This is a short, redacted evidence set for the accompanying investigation note. Source archives and the full phone log remain private because they include device, process, and account details. The hashes below identify the retained originals; they are not a claim that every private record can be independently checked from this public file.

## Older Grok 1.13.0 PairIP path

Library SHA-256: `d83f5775ba1b0f7e45de9527ab8281623e609b70d44d4f0e31c6914fa1b2506a`.

Selected instructions from the retained ARM64 ELF:

```text
0x373d4  ldr  x27, [x28, w5, uxtw]
0x3742c  sxtw x26, w27
0x37444  ldr  x24, [x28, w11, uxtw]
```

Selected tombstone values, omitting device and process identifiers:

```text
signal: SIGSEGV
process uptime: 326 seconds
x27: 0x75f7830003865f6f
x26: 0x0000000003865f6f
```

The signed lower 32 bits of `x27` are `0x03865f6f` = 59,137,903, matching `x26`. The source pointer is loaded later from a separate selected slot. The excerpt hashes are `5f92e692357aa05512147574f9befb6c0eaed4998b21ac9e9814d11b80df9e17` (disassembly) and `b632683f2f0b82f8646ff0495660962e7be3704773ef78269e6258cde1d0df65` (tombstone-register excerpt).

## Capture record tally

Ten retained Grok JSONL sessions contain 10 `session_start`, 10 `breakpoints_created`, 5 `native_signal_stop`, and 9 `target_exited` records. They contain **no intended operand-capture hit**. The record name `target_exited` can also arise from debugger detach and should not be equated with process death. The remote-stub acceptance transcript for the hardware breakpoints was not retained.

The historical source archives passed ZIP integrity checks on 8 October 2026. SHA-256: `bundle.zip` = `4d4ff55eae626d0e2ce63dcd8426bf2f229dc1d43a05939a8fb529bcbdfbc1b6`; `bundle2.zip` = `74dde94d30c5e770cd95fd11a1d5c074ebf69194f42a97335f658b525c3e6598`.

## Updated-device observation

Grok 1.14.0 PairIP library SHA-256: `5af6e1929517356cd6ad77235b79378cdd1d05618e004503c711fb56e214281b`.

Normalized log observations from a 29.7-second capture on 8 October 2026, Europe/Rome (installation path and process ID removed):

```text
01:08:50  nativeloader: libpairipcore.so loaded: ok
01:08:52  ActivityTaskManager: Grok MainActivity displayed
```

After the capture, the Grok process was still running. A case-insensitive search of the captured window for `fatal signal`, `F DEBUG`, `FATAL EXCEPTION`, `crash_dump`, `am_crash`, `tombstone written`, and `Process: ai.x.grok.bot` returned zero matches. This is a bounded observation, not evidence that the older defect is fixed. The private raw-log SHA-256 is `9e8f2a05bf6b559e0888ae2b1c5ca2d2e3461059d68f4ce191a60488b78e6977`.
