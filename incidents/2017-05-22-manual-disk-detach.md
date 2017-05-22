# Summary

On May 22, 2017, a user's pod was stuck in ContainerCreating because their disk was already in use. The disk was manually detached from the node after which their server started up correctly.

## Timeline

### 2017-05-22 10:04

A report in the uc-jupyter #datahub-support slack said that a user was having a server issue. After starting the user's server as admin, their pod was stuck in ContainerCreating. `describe pod` cited ```Failed to attach volume '<volume>' on node '<instance>' with googleapi: Error 400: The disk resource '<pvc>' is already being used by '<node>'```. This persisted for several minutes.

### 10:10

After running `gcloud compute instances detach-disk <instance> --disk <pvc>` and deleting the pod, the user's server was successfully started.

## Conclusion

A disk did not get detached from an instance.

## Action items

### Monitoring

1. Identify attached user volumes for which there is no pod.
