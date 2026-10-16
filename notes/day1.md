# Link (official blog post) 
- https://kernel-recipes.org/en/2026/2026/09/21/live-blog-day-1-morning/
- https://kernel-recipes.org/en/2026/2026/09/21/live-blog-day-1-afternoon/

# Ouverture / Kernel Report
## Replay
- https://www.youtube.com/watch?v=-KAx6m1XIlM&list=PLEVVgAZOU9P8&index=1
## Presenter
- Jonathan Corbet : co-founder of LWN (linux week news)
## Notes
- Mainly about IA
- Interesting point of view on its limitation and questions
  * acceleration on bug fix
  * rugpulls → how do we do if we no more access to IA
  * ecology concerns (huge electricity consumption)
  * copyright
  * human knowledge lost (who understand the code)

# Undefined behavior in C: a Lost Cause
## Replay
- https://www.youtube.com/watch?v=dhlYcmX_oBQ&list=PLEVVgAZOU9P8&index=14
## Presenter
- Martin Uecker: professor, gcc contributor
## Notes
- C answer his problem

# DAMOS: the Smart Cruise Control for RA
## Replay
- https://www.youtube.com/watch?v=cFGxYJ_oeVM&list=PLEVVgAZOU9P8&index=13
## Presenter
- SJ Park: kernel developper
## Notes
- RAM optimisation : free when not used 
- I learn about following concepts :
  * working set
  * memory tiering: cold/warm mem

# Linux Secure by default ?
## Replay
- https://www.youtube.com/watch?v=MJXXaUAPHy0&list=PLEVVgAZOU9P8&index=8
## Presenter
- Marta Rybcynska : Linux engineer (embeded system / security)
## Notes
- I lean about Yocto: linux distribution for embeded system
- Security using net namespace with unshare command
- seccomp option to secure syscalls
- syn cookie option to resist SYN flook attacks

# Userspace Assisted Scheduling with Sched QoS
## Replay
- https://www.youtube.com/watch?v=UL7PfLAisbE&list=PLEVVgAZOU9P8&index=11
## Notes
- Qais Yousef : Google
- Example of areas where we might want to adjust in userspace : TICK 4ms / DVFS
- Mention of : ABI  protection / TCMalloc incident

# Kernel testing frameworks
## Replay
- https://www.youtube.com/watch?v=BbATAIfSLjs&list=PLEVVgAZOU9P8&index=5
## Presenter
- Shuah Khan : Kernel Developper
## Notes
- Main components: kselftest, kunit
- Cyclomatic complexity : test single function directly

# Dual-core video decoding on RK3588: upstreaming VDPU381
## Replay
- https://www.youtube.com/watch?v=pNVac5VcmmU&list=PLEVVgAZOU9P8&index=18
## Presenter
- Detlev Casanova : Linux kernel engineer at Collabora
## Notes
- Video codecs h264 / hevc, vp9 / avs2
- v4l2 vs vulkan
- 8k / 60fps 
- Tricky to do dual-core because of depend frames
