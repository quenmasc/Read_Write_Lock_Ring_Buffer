# Read Write Lock Ring Buffer

This git contain a file which able to create a ring buffer with write priority. You can use many read threads to read ring buffer.

# How does it works ?

First of all, you need to use alsa-audio library on python (2.7) -> Linux / Raspbian / Debian
The ring buffer breaks down into two methods sharing a shared memory. Each task protects its critical tasks with semaphores. Both methods are writing and reading the circular buffer. Writing takes precedence over playback to avoid buffer loss from the sound card.
Writing is controlled by a method that verifies that the buffer is not full. Indeed, we seek to avoid over-writing and losing data. A buffer distance of two read buffers avoids this. The buffers are synchronized to the interruptions of the sound card.
The reading is somewhat different from conventional ring buffers. Indeed, the reading returns windows of "n" samples with an offset of "k" samples with each call. It therefore makes it possible to carry out frequency operations in real time.

# Real time ?
The buffet is designed to have the lowest latency output. Nevertheless, your treatments can lead to latency. ALL is in real time.

