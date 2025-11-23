Go’s goroutines are multiplexed onto a small pool of OS threads —
the runtime picks which goroutine runs on which thread at any moment.
