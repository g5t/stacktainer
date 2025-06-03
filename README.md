# stack-tainer 
ECDC stack + McCode-Plumber apptainer images

# Build

Use the Confluent Kafka Debian packages to build an Apptainer image which will launch a standalone
server listening on `localhost:9092` with suitable defaults.

```cmd
apptainer build kafka.sif kafka.def
```

# Run
The Kafka server can be started through either `run`, in which case the server logging output is visible,
or in a detached thread via `instance run` in which case no output is visible and the service must
be managed through `apptainer instance`

```cmd
apptainer run --writable-tmpfs kafka.sif 
```

```cmd
apptainer instance run --writable-tmpfs kafka.sif 
```

Note that in either case a writable temporary filesystem overlay is needed to allow the server to write
to the filesystem. This means that all stream data is lost when the server is restarted, so this mode
of operation is only suitable for ephemeral (stream) data as when producing simulated results.

Also note that the Kafka KRaft server uses port `9093`, so either launch method is liable to fail with
a hard-to-spot error message if either port `9092` or `9093` is already in use.
