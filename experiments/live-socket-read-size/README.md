# Round 5 Track D — live socket regression collaboration

Prior work: Hugohong258/pydantic-settings collaboration PR #1 remains open, head unchanged, no comments/reviews; upstream #1109 head unchanged and exact diff does not include the proposed native test. No follow-up comment was posted.

Discovery: 105 issue rows across boltons, humanize, more-itertools, path, attrs, cachetools, sortedcontainers, alive-progress and cached-property. Several recent defects already had prepared fixes; no duplicate production PR was created.

New contribution: https://github.com/Gambit-Checkmate/boltons/pull/1 targets the existing author's `fix/buffered-socket-read-size` branch for upstream mahmoud/boltons#676. Adds 12 native socketpair checks supplementing the existing fake-socket tests. They assert queued kernel bytes, wrapper buffer, original timeout and subsequent recovery, for negative/float lengths across recv/recv_size/peek with/without a prefilled buffer.

Candidate production head `2378372d88de01b123ce2a024f60b992dc284da5`: 12 new cases pass; two complete socket modules 43 passed. Revert only socketutils.py to base `d31d821d56c8f7756af9c30a864077f2e5855321`: 10 failed, 2 passed. The failures include missing expected ValueError and mutation of the underlying timeout before TypeError. Raw output retained.

An initial module run in the restricted environment passed 41 and failed 2 due to loopback PermissionError; this is retained in socket-modules.txt. Running the identical modules with loopback networking enabled passed all 43 (socket-modules-network.txt). Only generated socketutils bytecode was cleared between baseline and restored candidate to prevent stale source-cache results.

The external collaboration PR contains actual native test code. Author reply/run/acceptance, inclusion in upstream #676 and merge remain not observed. Code and raw outputs are published on owned branches; no additional upstream issue comment or duplicate implementation PR was created.
