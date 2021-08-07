# xsync benchmarks

Use the following command to run the benchmarks:
```bash
$ go test -bench .
```

To limit the number of used CPU cores append `-cpu=<number>` argument to the above command.

This document contains some benchmark results obtained on a cloud VM.

### RBMutex vs. sync.RWMutex

The following results were obtained on a GCP e2-highcpu-32 VM with 32 vCPUs (Intel Haswell), 32 GB memory, Ubuntu 20.04, Go 1.16.5.

<figure>
  <img src="./images/rb-mutex-read-only-no-work-chart.svg" alt="Reader locks only, no work in the critical section" />
  <figcaption>Reader locks only, no work in the critical section</figcaption>
</figure>

<br/><br/>

<figure>
  <img src="./images/rb-mutex-read-only-work-chart.svg" alt="Reader locks only, a loop spin in the critical section" />
  <figcaption>Reader locks only, some work in the critical section</figcaption>
</figure>

<br/><br/>

<figure>
  <img src="./images/rb-mutex-write-10000-chart.svg" alt="Writer locks on each 10,000 iteration, both no work and a loop spin in the critical section" />
  <figcaption>Writer locks on each 10,000 iteration, both no work and some work in the critical section</figcaption>
</figure>

### MPMCQueue vs. Go channels

The following results were obtained on a GCP e2-highcpu-32 VM with 32 vCPUs (Intel Haswell), 32 GB memory, Ubuntu 20.04, Go 1.16.5.

<figure>
  <img src="./images/mpmcqueue-no-work-chart.svg" alt="Concurrent producers and consumers (1:1), queue/channel size 1,000, no work" />
  <figcaption>Concurrent producers and consumers (1:1), queue/channel size 1,000, no work</figcaption>
</figure>

<br/><br/>

<figure>
  <img src="./images/mpmcqueue-work-chart.svg" alt="Concurrent producers and consumers (1:1), queue/channel size 1,000, some work" />
  <figcaption>Concurrent producers and consumers (1:1), queue/channel size 1,000, some work</figcaption>
</figure>

### Counter vs. atomic int64

The following results were obtained on a GCP e2-highcpu-32 VM with 32 vCPUs (Intel Haswell), 32 GB memory, Ubuntu 20.04, Go 1.16.5.

<figure>
  <img src="./images/counter-chart.svg" alt="Concurrent incs/decs, a value read on each 10,000 modification" />
  <figcaption>Concurrent incs/decs, a value read on each 10,000 modification</figcaption>
</figure>