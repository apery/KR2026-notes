# Kernel Recipes 2026 - Notes

16 October 2026 · Philippe

## Overview

Kernel Recipes 2026, the 13th edition (Paris, 21–23 September), had one dominant theme: LLMs are reshaping kernel development. Bug fixes and CVEs are surging, and AI review tooling such as Sashiko is already part of the workflow. The rest went deep into schedulers, memory management, locking and Rust.

### Talks I preferred

| Talk | Speaker | Why |
| --- | --- | --- |
| The Kernel Report | Jonathan Corbet (LWN) | What LLMs change: faster fixes, review load, rug-pull risk, knowledge loss |
| LLMs and us | Greg Kroah-Hartman | Of 79 Mythos "vulnerabilities", about 10 were real fixes |
| The Maintainer Container | Konstantin Ryabitsev | kernel.org tooling (b4, korgalore) for the patch firehose |
| What's cooking in Git | Patrick Steinhardt (GitLab) | Little-known commands, and Git 3.0 (SHA-256, reftables, `main`) |
| Multipath TCP | Matthieu Baerts | Several network paths at once (Wi-Fi + 4G) |
| Large scale kernel build testing | Arnd Bergmann | About 1,000 kernels a day on one workstation |
| Sashiko | Roman Gushchin | Open-source, multi-stage AI review sending LKML-style emails |
| Rust for Linux | Miguel Ojeda | The experiment is over: Rust is here to stay |
| DAMOS | SJ Park | Automatic in-kernel RAM optimisation driven by DAMON |
| Futex, the good the bad and the ugly | Steven Rostedt | Building userspace locks from `cmpxchg` and the futex syscall |

### What I remember

- **C vs Rust is a live debate:** C is removing undefined behaviour from the standard, while Rust is now official in the kernel and has replaced the C binder driver.
- **LLMs caused a surge in bug reports:** from about 50 CVEs a week last year to 33 a day. Greg's advice: push back on long, persuasive text and ask for a patch.
- **MPTCP** is built into Linux since v5.6; curl, nginx, haproxy and Go servers already opt in.
- **Git 3.0** brings SHA-256 by default, but forges and tools (GitHub, Gerrit, JGit) are not ready yet.
- **The community's organisation is impressive:** maintainer tooling, CI, kselftest/KUnit and stable processes scale through tools and conventions.

Break discussions: boot sequence security, offline mail with `mbsync`, and the book *Modern C* by Jens Gustedt (Inria, ISO C committee).

Links: 
- [live blog](https://kernel-recipes.org/en/2026/the-live-blog/)
- [videos](https://www.youtube.com/playlist?list=PLEVVgAZOU9P8)

## Day 1: Monday 21 September

**The Kernel Report** — Jonathan Corbet, LWN.net · [replay](https://www.youtube.com/watch?v=-KAx6m1XIlM&list=PLEVVgAZOU9P8&index=1)
The yearly state of Linux: a new version every 9–10 weeks, and this year the story was AI. Bugs get fixed faster, but AI-generated patches pile work on a small number of reviewers. Risks: depending on AI vendors who can change their terms overnight, and experienced maintainers retiring without successors.

**Undefined behavior in C: a Lost Cause?** — Martin Uecker, C standards committee · [replay](https://www.youtube.com/watch?v=dhlYcmX_oBQ&list=PLEVVgAZOU9P8&index=14)
Most of the kernel is written in C, a language where some mistakes lead to unpredictable behaviour. The answer was "no, not a lost cause": the C standard is closing these gaps and compilers now ship checkers that catch many of them.

**DAMOS: the Smart Cruise Control for RAM** — SJ Park · [replay](https://www.youtube.com/watch?v=cFGxYJ_oeVM&list=PLEVVgAZOU9P8&index=13)
The kernel can now watch which memory a workload really uses and automatically free or move the rest to cheaper memory. You set a goal ("keep memory pressure low") instead of tuning knobs. Already in production at AWS (Aurora Serverless v2): relevant for anyone sizing or right-sizing hosts.

**Linux Secure by Default** — Marta Rybczynska · [replay](https://www.youtube.com/watch?v=MJXXaUAPHy0&list=PLEVVgAZOU9P8&index=8)
She checked Ubuntu, OpenWrt, Yocto and the stock kernel against a list of 260 recommended security settings. Distributions are safer than the stock kernel defaults, but not fully hardened. SRE takeaway: don't assume defaults are secure, and audit your kernel config. Docker can also conflict with Ubuntu's `ufw` firewall.

**Userspace Assisted Scheduling with Sched QoS** — Qais Yousef · [replay](https://www.youtube.com/watch?v=UL7PfLAisbE&list=PLEVVgAZOU9P8&index=11)
A proposal to let applications tell the kernel "I care about latency" or "I care about throughput", so a single scheduler can serve both. Kernel changes take 2–3 years to reach production systems.

**Kernel testing frameworks** — Shuah Khan · [replay](https://www.youtube.com/watch?v=BbATAIfSLjs&list=PLEVVgAZOU9P8&index=5)
The kernel has thousands of built-in tests, and new features are expected to come with tests. Code-coverage numbers are useful to find gaps but are a bad target in themselves, a lesson that applies to any codebase.

**Dual-core video decoding on RK3588** — Detlev Casanova, Collabora · [replay](https://www.youtube.com/watch?v=pNVac5VcmmU&list=PLEVVgAZOU9P8&index=18)
How hardware video decoding (up to 8K) for a popular ARM board chip was added to Linux, using both of its decoder units in parallel. A story about undocumented hardware quirks.

## Day 2: Tuesday 22 September

**Futex, the good the bad and the ugly** — Steven Rostedt · [replay](https://www.youtube.com/watch?v=KPDkA8_wyJU&list=PLEVVgAZOU9P8&index=2)
How the locks that multi-threaded programs use are built. The idea: stay fast in the common case and only ask the kernel for help when threads actually wait on each other. Also covered: what happens when a process dies while holding a lock.

**LAVD: from gaming to server fleets** — Changwoo Min, Gavin Guo, Igalia · [replay](https://www.youtube.com/watch?v=wh9GJDnbaMs&list=PLEVVgAZOU9P8&index=20)
Linux now lets you plug in a custom CPU scheduler without rebuilding the kernel. LAVD started on the Steam Deck to stop games from stuttering, and now runs on servers. The SRE lesson: optimise tail latency (the slowest 1%), not the average.

**The Maintainer Container** — Konstantin Ryabitsev, kernel.org · [replay](https://www.youtube.com/watch?v=MF_4bRsZZoY&list=PLEVVgAZOU9P8&index=7)
Kernel development still runs on email and git. This new self-hosted container gives maintainers an offline copy of mailing lists and repos, a terminal UI to review patches with CI and AI results, and hooks for AI agents, with caution about prompt injection hidden in patches.

**Charity auction** supported the Software Freedom Conservancy, which hosts free-software projects and enforces the GPL licence.

**LLMs and us** — Greg Kroah-Hartman, stable kernel maintainer · [replay](https://www.youtube.com/watch?v=NnV_cWeoo5Q&list=PLEVVgAZOU9P8&index=9)
"Do not panic." Linux security advisories (CVEs) went from about 50 a week to 33 a day, driven by AI tools. A headline about "79 vulnerabilities found by AI" boiled down to about 10 real fixes. Attackers now often have an exploit before a fix ships, so patching speed matters more than ever. His advice: be wary of long, convincing AI text, ask for a fix rather than a report, and never paste private data into an AI service. "It's going to be a rough 18 months."

**What's cooking in Git** — Patrick Steinhardt, GitLab · [replay](https://www.youtube.com/watch?v=gbxCamrCt2o&list=PLEVVgAZOU9P8&index=16)
Handy recent Git commands (`git range-diff` to compare two versions of a branch, `git rebase --update-refs` for stacked branches). Git 3.0 (around April 2027) switches to a stronger hash (SHA-256) and `main` as the default branch. Expect tooling friction: GitHub and other forges don't support the new format yet.

**Handling lock-holder preemption** — Victor Laforet, Inria · [replay](https://www.youtube.com/watch?v=SFBJvfb2tHs&list=PLEVVgAZOU9P8&index=10)
When a machine runs more threads than CPUs, some locks waste CPU spinning while the thread that holds them is paused. FlexGuard detects this and switches the waiting threads to sleep, improving performance on overloaded hosts.

## Day 3: Wednesday 23 September

**Swap and memory reclaim** — Kairui Song, Tencent · [replay](https://www.youtube.com/watch?v=XEhDipqOpsI&list=PLEVVgAZOU9P8&index=12)
With RAM prices rising, swap is worth a second look. Linux swap was rewritten to be simpler and faster, and the kernel's way of picking which memory to evict got smarter. Compressed RAM (zram/zswap) is an alternative to swapping to disk.

**Enforcing Device Driver Lifetime Rules at Compile Time** — Danilo Krummrich, Red Hat · [replay](https://www.youtube.com/watch?v=A5awIY4UTG0&list=PLEVVgAZOU9P8&index=4)
Using Rust, a whole class of driver bugs (using a device after it's gone, leaking resources) becomes impossible: the code simply won't compile. Fewer kernel crashes from drivers in the long run.

**Multipath TCP** — Matthieu Baerts · [replay](https://www.youtube.com/watch?v=uU079w98ink&list=PLEVVgAZOU9P8&index=19)
One connection over several network paths at once: survive a Wi-Fi → 4G switch without dropping, or combine bandwidth. Built into Linux and supported by curl, nginx, haproxy and Go servers; existing apps can be enabled without code changes. Load balancers and CDNs are the main gap. See [mptcp.dev](https://www.mptcp.dev).

**Large scale kernel build testing on a desktop** — Arnd Bergmann, Linaro · [replay](https://www.youtube.com/watch?v=Gxw7lorBEKA&list=PLEVVgAZOU9P8&index=6)
About 1,000 kernel builds a day on a single workstation, no cloud, catching thousands of bugs. Randomised build configurations find the most problems: a good reminder that testing many configurations beats testing one well.

**Postgres {on,vs,with} Linux** — Andres Freund · [replay](https://www.youtube.com/watch?v=isATpooTax8&list=PLEVVgAZOU9P8&index=17)
Very relevant for anyone running PostgreSQL. It is moving to threads and faster asynchronous I/O. Pain points: memory-limit (cgroup) out-of-memory kills ignore the strict overcommit setting Postgres prefers, disk preallocation fragments files, and 1 GB huge pages can cause contention. Good news: recent kernels write data to disk 2–4× faster.

**Sashiko** — Roman Gushchin · [replay](https://www.youtube.com/watch?v=gE7dBZBLvBc&list=PLEVVgAZOU9P8&index=15)
An open-source AI code reviewer for kernel patches that replies by email like a human reviewer. It reviews in about 16 minutes, has sent 6,000+ reviews, and the issues it flags as "critical" tend to need fixes later. It still makes things up, so humans stay in the loop. [sashiko.dev](https://sashiko.dev)

**Rust for Linux** — Miguel Ojeda · [replay](https://www.youtube.com/watch?v=7kPn2Kf7AJM&list=PLEVVgAZOU9P8&index=3)
Rust is officially a permanent part of the kernel. It already ships on Android, and Debian and other distributions enable it. Expect more drivers written in Rust, with fewer memory-safety bugs.
