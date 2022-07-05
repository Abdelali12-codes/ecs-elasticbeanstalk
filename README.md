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
* to set env use the below command

```
eb setenv ENVVAR=TEST
```

* to print env use the below command

```
eb printenv
```

* to check the available options, check the below link
https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/command-options-general.html#command-options-general-autoscalingasg


* import value in option_settings:
```
option_settings:
  aws:elasticbeanstalk:application:environment:
    TOPIC_ARN: '`{ "Fn::ImportValue" : "NotificationTopicArn" }`'
```
