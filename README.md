# ThreadGroup

[![crates.io](https://img.shields.io/crates/v/threadgroup.svg)](https://crates.io/crates/threadgroup)
[![docs.rs](https://docs.rs/threadgroup/badge.svg)](https://docs.rs/threadgroup)
[![license](http://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/vincentdephily/threadgroup/blob/master/LICENSE.txt)

This crate handles a group of threads (whose closures have the same return type) as one unit,
letting you `join()` or `join_timeout()` on the first thread of the group that is ready. Internally,
it uses a channel to notify about finished threads.

This is useful when you want to check whether any one of your threads has panicked or returned
early, for error-handling or for progress report. This isn't possible with
`std::thread::JoinHanlde.join()` because it is a blocking call, so thread 2 might panic or finish
while you're waiting indefinitely on thread 1.


# See also

If `ThreadGroup` isn't what you needed after all and can't be improved to suit your needs, have a
look at these other crates :

* [Thread_tryjoin](https://crates.io/crates/thread_tryjoin) gives the same benefit as
  `ThreadGroup.join_timeout()` with an API that is closer to `std`'s. But it depends on a Linux-only
  API, and only handles one thread at a time (so that `try_join()`ing a lot of thread will end up
  wasting either time or CPU).
* [Thread-control](https://crates.io/crates/thread-control) and
  [Runloop](https://crates.io/crates/runloop) let you stop threads, and test without blocking if
  they panicked or finished. Again, this only handles one thread at a time.
* [Rayon](https://crates.io/crates/rayon) is a higher-level abstraction to spread a computation over
  multiple threads.
* [Thread pools](https://crates.io/search?q=thread+pool) are a common idiom to handle short
  computations without repeatedly paying the high setup cost.
* [Future](https://crates.io/crates/futures) isn't related to threads but is often a better way to
  handle "start task B whenever task A finishes" algorythms.


# Contributing

Please create issues and send pull request via
[Github](https://github.com/vincentdephily/threadgroup).

Threadgroup is licensed as MIT. Unless you explicitly state otherwise, any contribution
intentionally submitted for inclusion in the work by you, as defined in the MIT license, shall be
licensed as above, without any additional terms or conditions.
