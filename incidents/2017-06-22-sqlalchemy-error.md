## Summary ##

Late night 21 June 2017, the data8 hub went down. Students noticed, and alarm was raised in the #datahub-support channel. A restart fixed temporarily, but it kept recurring pretty regularly the next day. The underlying issue turned out to be storage related, and was finally fixed 22 June 2017 10:16.

## Timeline ##

All times in PST

### June 21 2017 23:48 ###

The hub starts failing.

### 23:59 ###

It's mentioned in the #datahub-support channel

### June 22 00:15 ###

It is determined that the proxy pod is fine, but the hub pod is returning empty responses when hit with requests.

### 00:20 ###

The hub pod's logs are saved, and the hub is restarted. Service is restored, everything seems fine.

[Issue](https://github.com/jupyterhub/jupyterhub/issues/1179) is filed in JupyterHub about the exception being thrown in the logs.

### 09:01 ###

Classes start, and alarm is raised again in #datahub-support about the hub being down.

### 09:09 ###

Another hub restart fixes it.

### 09:28 ###

Recurs! A manual restart is performed, and progress made towards merging the PR that'll have kubernetes do a health check and autorestart.

We play whack-a-mole with hub restarts.

### 09:48 ###

A student reports getting `write error: no space left on device` as an error. This is illuminating - the NFS mount on which the students homedirectories and the hub db are mounted is almost full! However, it is only 50G, while it should have been 4T.


## Conclusion ##

Storage should be as big as you think it is.

## Action items ##

### Monitoring ###

1. This has been so many action items! Add monitoring so we get notified by robots, not humans.

### Helm chart ###

1. Add a simple health check to the hub pod process so it'll restart if situations like this happen again. [PR](https://github.com/jupyterhub/helm-chart/pull/36)
