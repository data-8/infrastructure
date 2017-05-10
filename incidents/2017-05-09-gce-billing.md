# Summary

On May 9, 2017, the compute resources associated with the data-8 project at GCE were suspended. All hubs including datahub, stat28, and prob140 were not reachable. This happened because the grant that backed the project's billing account ran out of funds. The project was moved to a different funding source and the resources gradually came back online.

## Timeline

### 2017-05-09 16:51

A report in the Data 8 Spring 2017 Staff slack, #jupyter channel, says that datahub is down. This is confirmed. Attempting to access the provisioner via `gcloud compute ssh provisioner-01` fails with:

```ERROR: (gcloud.compute.ssh) Instance [provisioner-01] in zone [us-central1-a] has not been allocated an external IP address yet. Try rerunning this command later.```

### 17:01

The Google Cloud console shows that the billing account has run out of the grant that supported the data-8 project. The project account is moved to another billing account which has resources left.

The billing state is confirmed by `gcloud` messages:

```
Google Compute Engine: Project data-8 cannot accept requests to setMetadata while in an inactive billing state.  Billing state may take several minutes to update.
```

### 17:09

provisioner-01 is manually started. All clusters are still present but the containers are in a ContainerCreating state.

### 17:15

datahub is back online. stat28 and prob140 are stuck in the ContainerCreating state so their hub pods are manually killed. After a few moments the hubs are back online.

## Conclusion

There was not sufficient visibility into the billing alerts.

## Action items

### Process

1. Identify channels for billing alerts.
1. Identify billing threshold functions that predict when funds will run out.

### Monitoring

1. Setup scheduled billing reports and threshold alarms.