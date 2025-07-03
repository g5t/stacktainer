# stacktainer 
ECDC stack + McCode-Plumber apptainer images

# Images
Images are defined and built in their associated repositories

| image | repository |
|-------|------------|
| ECDC binaries | [stacktainer-ecdc](https://github.com/g5t/stacktainer-ecdc) |
| ECDC binaries + McCode-Plumber | [stacktainer-splitrun](https://github.com/g5t/stacktainer-splitrun) |
| temporary Kafka server | [stacktainer-kafka](https://github.com/g5t/stacktainer-kafka) |

Built images are hosted by Github, and can be retrieved via, e.g.,

```cmd
apptainer pull oras://ghcr.io/g5t/stacktainer/splitrun:5.1
apptainer pull oras://ghcr.io/g5t/stacktainer/kafka:3.0
```

# Use
The modulefile defined in this repository is intended to be the gateway to _using_ the full stack `splitrun`.

```cmd
module load stacktainer/1.1
```

The `kafka` module file provides two commands (under `sh`-like shells only, at the moment) to `start-kafka` and `stop-kafka`.
The `splitrun` module file provides aliases to the useful binaries and programs in the image
