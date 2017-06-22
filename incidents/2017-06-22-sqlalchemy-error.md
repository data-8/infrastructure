## Summary ##

Late night 21 June 2017, the data8 hub went down. Students noticed, and alarm was raised in the #datahub-support channel. It was a sqlalchemy issue - restarting the hub fixed it for now.

## Timeline ##

All times in PST

### June 21 2017 23:48 ###

The hub starts failing.

### 23:59 ###

It's mentioned in the #datahub-support channel

### June 22 00:15 ###

It is determined that the proxy pod is fine, but the hub pod is returning empty responses when hit with requests.

### 00:20 ###

The hub pod's logs are saved, and the hub is restarted. Services is restored.

[Issue](https://github.com/jupyterhub/jupyterhub/issues/1179) is filed in JupyterHub about the exception being thrown in the logs.

## Conclusion ##

SQLAlchemy sessions are mysterious still.

## Action items ##

### Monitoring ###

1. This has been so many action items! Add monitoring so we get notified by robots, not humans.

### Helm chart ###

1. Add a simple health check to the hub pod process so it'll restart if situations like this happen again. [PR](https://github.com/jupyterhub/helm-chart/pull/36)
