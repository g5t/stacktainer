# stack-tainer 
ECDC stack + McCode-Plumber apptainer images

# Images
Images are defined and built in their associated repositories

| image | repository |
|-------|------------|
| ECDC binaries | [stack-tainer-ecdc](https://github.com/g5t/stack-tainer-ecdc) |
| ECDC binaries + McCode-Plumber | [stack-tainer-splitrun](https://github.com/g5t/stack-tainer-splitrun) |
| temporary Kafka server | [stack-tainer-kafka](https://github.com/g5t/stack-tainer-kafka) |

Built images are hosted by Github, and can be retrieved via, e.g.,

```cmd
apptainer pull oras://ghcr.io/g5t/stack-tainer-splitrun/stack-tainer-splitrun:2.0
apptainer pull oras://ghcr.io/g5t/stack-tainer-kafka/stack-tainer-kafka:1.0
```

# Use
The modulefile defined in this repository is intended to be the gateway to _using_ the full stack `splitrun`.

```cmd
module load ./kafka/1.0
module load ./splitrun/2.0
```

The `kafka` module file provides two commands (under `sh`-like shells only, at the moment) to `start-kafka` and `stop-kafka`.
The `splitrun` module file provides aliases to the useful binaries and programs in the image
