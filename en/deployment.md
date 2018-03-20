# How to Deploy

## Summary

Laravel Rockect is designed working with AWS and support Elastic Beanstalk. So best way to manage production/staging/development server is using Elastic Beanstalk. But application itself is quite normal laravel application and can use the following environment.

## Deploy in elastic beanstalk

### 1. Create New App and Environment in Elastic beanstalk

Create app on your preference region ( now we use Singapore region for testing environment ) and create new instance.

For instance type, t2.micro is okay for testing environment. and for production environment, we recommend c4.large and autoscaling from 1 to 4 servers. Normally it is quite okay with 1 instance. But can set autoscaling just in case.

Select PHP 7.1 server.

### 2. Create new RDS instance

It is possible to create RDS instance on Elastic Beanstalk but we won't do that. Because if we create RDS instance on Elastic Beanstalk, that instance will be terminated when we delete environment on Elastic Beanstalk. So it is strongly recommended to create new environment.

Instance type can be okay with micro on testing, and for production, small or medium is okay.

And after create RDS instance, need to add Elastic Beanstalk EC2 instance's security group to incoming TCP MySQL connection permission.


### 3. Create new Redis Instance

The app support both Redis and Memcached, so you can choose with your preference on Elastec Cache. And for testing environment, you don't have to use Elastic Cache for cashing and session store. On that case, app server's local file system will be used.
Using server's local file system is okay only on "Single Instance Environment" and will be removed totally when you deploy new version of server. So if you still want to keep session info after you did deploy on testing environment, you should use ElasticCashe on testing environment also.

### 4. Set Environment Variables

On local development, we can use `.env` file to set specific params like mysql server/user/password, AWS key/secret and so on. But on Elastic Beanstalk, you need to set environment variables on Elastic Beanstalk console or command line `eb` command like follows.

```
eb setenv APP_ENV=development APP_KEY=XXXXXXX APP_DEBUG=true APP_LOG_LEVEL=debug APP_URL=http://localhost DB_CONNECTION=mysql DB_HOST=XXXXXXXX DB_PORT=3306 DB_DATABASE=XXXXXX DB_USERNAME=XXXXX BROADCAST_DRIVER=log CACHE_DRIVER=file SESSION_DRIVER=file QUEUE_DRIVER=sync  REDIS_HOST=127.0.0.1 REDIS_PASSWORD=null REDIS_PORT=6379  STORAGE_TYPE=s3  AWS_IMAGE_REGION=ap-southeast-1 AWS_IMAGE_BUCKET=XXXXXXXX AWS_KEY=XXXXX AWS_SECRET=XXXXXXX AWS_SES_REGION=us-east-1
```

### 5. Setup elasticbeanstalk on your local repository.

To deploy code, it also uses eb command which AWS officially distrubutes.
These tools are written by Python and Python's package manager pip can help to install.

```
% pip install awscli
% pip install awsebcli
```

Then you can configure the account with `aws` command.

```
% aws --profile [ProfileName] configure   
```

This command ask you about AWS key & secrets for deploy. So you can set your own key for deployment ( it will only be stored in your local machine).
Then setup Elastic Beanstalk on your git repository base directory.

```
% eb init --profile [ProfileName]
```

This command ask you several questions. You should choose region and app name which you created and answer "no"(default) to the question about "use code deploy".

### 6. Deploy

Now you are ready for deployment. To deploy current branch with `eb deploy` command.

```
% eb deploy
```

Then, deploy will start and you need to wait for a while.
`eb init` create `.elasticbeanstalk` directory on your repository and `config.yml` file is the config file like following.

```
branch-defaults:
  master:
    environment: [Environment Name]
environment-defaults:
  [Environment Name]:
    branch: null
    repository: null
global:
  application_name: [App Name]
  default_ec2_keyname: [Key File Name]
  default_platform: arn:aws:elasticbeanstalk:ap-southeast-1::platform/PHP 7.1 running
    on 64bit Amazon Linux/2.6.5
  default_region: ap-southeast-1
  include_git_submodules: true
  instance_profile: null
  platform_name: null
  platform_version: null
  profile: [Profile Name]
  sc: git
  workspace_type: Application
```

And as you can see the `branch-defaults`, branch & elastic beanstalk environment has a relation. So you need to configure this file to associate branch and environment before you try to push new build.
