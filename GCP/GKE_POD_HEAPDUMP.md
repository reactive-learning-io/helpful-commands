# GKE: Doing stuff in a POD

### Permanently save the namespace for all subsequent **kubectl** commands in that context.
`kubectl config set-context --current --namespace=my-namepsace`

## Executing into a Pod
### Got to Pod command line
`kubectl exec -it pod_name -n my-namespace sh`

### Install SDK 
```
- curl https://sdk.cloud.google.com | bash
- exec -l $SHELL
```

### Installing jattach utility
`apk add --no-cache jattach --repository http://dl-cdn.alpinelinux.org/alpine/edge/community/
`

### Define below params in Dockerfile
```
ENV MALLOC_ARENA_MAX=2
ENV JAVA_OPS="-XX:MaxMetaspaceSize=256m -XshowSettings:vm -XX:+UseG1GC -XX:MaxDirectMemorySize=64m -XX:NativeMemoryTracking=off"
```

### Native Memory Tracking
```
- jattach 1 jcmd "VM.native_memory baseline"
- jattach 1 jcmd "VM.native_memory summary"
- jattach 1 jcmd "VM.native_memory summary.diff"
```

### Taking heapdump
`jattach 1 dumpheap heapdump_podname_time.hprof`

### Compressing heapdump
`tar -cvzf heapdump_podname_time.tar.gz heapdump_podname_time.hprof`

### Copy heapdump from K8s pod to local machine
`kubectl cp POD_NAME:/app/heapdump_podname_time.tar.gz heapdump.tar.gz`

--- 
## Alternatively Push the heapdumps to Google Storage

### Installing gsutil
```
- wget https://storage.googleapis.com/pub/gsutil.tar.gz
- tar xfz gsutil.tar.gz -C $HOME
- export PATH=${PATH}:$HOME/gsutil
```

### Active Service Account
`gcloud auth activate-service-account --key-file /key.json`

### Copy file to Google Bucket
`gsutil cp file gs://testbucket/`

[Learn more](https://cloud.google.com/storage/docs/gsutil/commands/cp)

---
### References:
- https://www.infoq.com/articles/Troubleshooting-Java-Memory-Issues/
- https://docs.oracle.com/javase/8/docs/technotes/guides/troubleshoot/tooldescr007.html