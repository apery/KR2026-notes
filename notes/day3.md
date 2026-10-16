# Link (official blog post)
- https://kernel-recipes.org/en/2026/2026/09/23/live-blog-day-3-morning/
- https://kernel-recipes.org/en/2026/2026/09/23/live-blog-day-3-afternoon/

# Swap and memory reclaim: Squeezing out more RAM
## Replay
- https://www.youtube.com/watch?v=XEhDipqOpsI&list=PLEVVgAZOU9P8&index=12
## Presenter
- Kairui Song, Tencent
## Notes
Swap and memory reclaim
- memhog
- folio / swap out
- swap cache
- swap map cgroup
- anon, file (/proc/meminfo)
- classical LRU 2 lists active / inactive
- pte access
- tier : cold, hot, etc
- mglru : aging
- refault
- compressed memory

# Enforcing Device Driver Lifetime Rules at Compile Time
## Replay
- https://www.youtube.com/watch?v=A5awIY4UTG0&list=PLEVVgAZOU9P8&index=4
## Presenter
- Danilo Krummrich, Redhat
## Notes
- Mainly about Rust avantage against C for driver developping
- pin-init
- driver mode
- IRQ registration
- qemu : emulate a driver, interrupts, etc
- DMA

# Multipath TCP: when one path is not enough
## Replay
- https://www.youtube.com/watch?v=uU079w98ink&list=PLEVVgAZOU9P8&index=19
## Presenter
- Matthieu Baerts
## Notes
- subflow / fallback
- packet scheduler
- ip mptcp endpoint add <ip> dev device
- apps : curl, haproxy, nginx
- mptcp.dev
- ptcpdump
- Tcp ulp (skb ext)
- load balancer : what's happen if server tell to use a new address
- quic
- bpf sockmap
- nvme over mptcp
- CGNat, Nat ?

# Large scale kernel build testing on a desktop
## Replay
- https://www.youtube.com/watch?v=Gxw7lorBEKA&list=PLEVVgAZOU9P8&index=6
## Presenter
- Arnd Bergmann, Kernel developer
## Notes
- Apple Mac Studio
- makefiles
- no cloud
- linux-next
- toolchain : build gcc, clang (equal to gcc these days)
- Kconfig: use dependency instead of select
- padding (arch depend)

# Postgres {on,vs,with} Linux
## Replay
- https://www.youtube.com/watch?v=isATpooTax8&list=PLEVVgAZOU9P8&index=17
## Presenter
- Andres Freund, PostgresSQL developer
## Notes
- moving to thread : tlb, context switch
- plain futex / PI futex (not useable)
- overcommit_memory=2 (does not work in cgroups)
- reserve space on disk (does not work on CoW system)
- huge pages

# Sashiko: agentic review of Linux Kernel code changes
## Replay
- https://www.youtube.com/watch?v=gE7dBZBLvBc&list=PLEVVgAZOU9P8&index=15
## Presenter
- Roman Gushchin, Kernel developper
## Notes
- Preventing new issue with agentic review

# Rust for Linux
## Replay
- https://www.youtube.com/watch?v=7kPn2Kf7AJM&list=PLEVVgAZOU9P8&index=3
## Presenter
- Miguel Ojeda, Rust maintainer
## Notes
- zerocopy
- config to enable rust support
- gccrs, rustc_codegen_gcc
- debian stable rust version
- version upgrade, backward incompability
- AI assisted formal prove
