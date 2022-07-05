# ecs-elasticbeanstalk

## download container image from private repository
```
{
  "AWSEBDockerrunVersion": "1",
  "Authentication": {
    "Bucket": "DOC-EXAMPLE-BUCKET",
    "Key": "mydockercfg"
  },
  "Image": {
    "Name": "quay.io/johndoe/private-image",
    "Update": "true"
  },
  "Ports": [
    {
      "ContainerPort": "1234"
    }
  ],
  "Volumes": [
    {
      "HostDirectory": "/var/app/mydb",
      "ContainerDirectory": "/etc/mysql"
    }
  ],
  "Logging": "/var/log/nginx"
}
```
## ElasticBeanstalk Configuration

### Before environment creation

* save configuration of an environment

```
eb config save --cfg my-app-v1
```
once you tape this command the new file will be create (project/.elasticbeanstalk/saved_configs/my-app-v1.cfg.yml)

* upload the saved configuration to s3

```
eb config put my-app-v1
```

* to create new environment within your eb app run the below command

```
eb create --cfg savedconfig
```

* apply saved configuration to the running environment

```
 eb config --cfg v1
```
