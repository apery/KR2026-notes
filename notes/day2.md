# Link (official blog post)
- https://kernel-recipes.org/en/2026/2026/09/22/live-blog-day-2-morning/
- https://kernel-recipes.org/en/2026/2026/09/22/live-blog-day-2-afternoon/

# Futexes, the good the bad and the ugly
## Replay
- https://www.youtube.com/watch?v=KPDkA8_wyJU&list=PLEVVgAZOU9P8&index=2
## Presenter
- Steven Rostedt: Qube
## Notes
- deep dive into futexes:
  * lock, race condition -> xchg
  * userspace
  * waiters
  * use share memory using mmap, shmem
  * robust futexes (owner died)
  * PI-futex
- A userspace issue as kernel dont need Futex because it knows every things

# LAVD: from gaming to server fleets
## Replay
- https://www.youtube.com/watch?v=wh9GJDnbaMs&list=PLEVVgAZOU9P8&index=20
## Presenter
- Changwoo Min and Gavin Guo : Igalia
## Notes
- SCX: Replace scheduler by a Bpf scheduler (for gaming) → scx_land 
- cfs scheduler
- low fps metric (for gaming)
- waker / wakee
- wait_freq, wake_freq,runtime
- predict wait, wait budget
- l3 cache
- proton, wine, pipewire
- Steam deck

# Maintainer container
## Replay
- https://www.youtube.com/watch?v=MF_4bRsZZoY&list=PLEVVgAZOU9P8&index=7
## Presenter
- Konstantin Ryabitsev, Infra (kernel.org)
## Notes
- Tools for kernel maintainers
- b4 : Am, shazam, prep, send
- tui for review, NACK (not acknowledged)
- "s in mcp stand for security"

# Charity auction: Software Freedom conservancy
- coreboot
- openwrt one
- copyleft enforcement

# Security in LLM
## Replay
- https://www.youtube.com/watch?v=NnV_cWeoo5Q&list=PLEVVgAZOU9P8&index=9
## Presenter
- Greg Kroah-Hartman, main linux developer (after Linus Torvald)
## Notes
- NOMMU bug (79 mythos cve → ~3 real bugs)
- skip body on commit message
- skip big comments for small changes (few line)
- ask for patch
- run local model (opencode, pi, etc)
- never upload non public info
- to read : securing code in the age of AI
- "it's all about trust"

# What’s cooking in Git
## Presenter
- Patrick Steinhardt, Engineer at GitLab
## Replay
- https://www.youtube.com/watch?v=gbxCamrCt2o&list=PLEVVgAZOU9P8&index=16
## Notes
- merge-tree --write-tree
- range-diff
- rebase -i --update-refs
- git history (experimental, rewrite history)
- jujutsu (git compatible): extends features
  → git 3
- sha256, reftables
  → Migration challenges : submodule ? branches ? Gpg signature

# Kernel support for user-space locking: handling lock-holder preemption
## Replay
- https://www.youtube.com/watch?v=SFBJvfb2tHs&list=PLEVVgAZOU9P8&index=10
## Presenter
- Victor Laforet, Inria
## Notes
- spinlock
- time slice extension
- qspinlock
- flexguard
