---
id: backend
sidebar_label: backend
---
# Backend
A backend defines where Kusion stores its state data files. Kusion configure backend in project.yaml.

By default, Kusion uses a backend called local, which stores state as a local file on disk. You can also configure backend in this documentation.

## Backend configure
### File configure 

kusion configure backend in project.yaml.

```yaml
backend:
  storageType: oss
  config:
    endpoint: oss-cn-beijing.aliyuncs.com
    bucket: kusion-oss
```
* storageType - define backend type
* config - define parameters of the backend
### Command-line configure
```sh
kusion apply -C accessKeyID=********** -C accessKeySecret=************
```
### Merge configure
If backend settings are provided in multiple locations, the top-level settings are merged such that any command-line options override the settings in the main configuration.

File Configuration:

```yaml
backend:
  storageType: oss
  config:
    endpoint: oss-cn-beijing.aliyuncs.com
    bucket: kusion-oss
```

Command-line Configuration:
```sh
kusion apply -C accessKeyID=********** -C accessKeySecret=************
```

the top-level settings are merged.
```yaml
backend:
  storageType: oss
  config:
    endpoint: oss-cn-beijing.aliyuncs.com
    bucket: kusion-oss
    accessKeyID: ********** 
    accessKeySecret: ************
```

## Available Backends
- local
- oss
- s3
- db

### default Backend

if not define backend, defalut [local](#local)

### local
The local backend stores state on the local filesystem.

Example Configuration:
```yaml
backend:
  storageType: local
  config:
    path: kusion_state.json
```
* storageType - local, define local backend
* path - (Optional) The path to the state file.

### oss

The oss backend stores state on the alibaba Cloud OSS.

Example Configuration:
```yaml
backend:
  storageType: oss
  config:
    endpoint: oss-cn-beijing.aliyuncs.com
    bucket: kusion-oss
```
Command-line Configuration:
```sh
kusion apply -C accessKeyID=********** -C accessKeySecret=************
```

* storageType - oss, define Alibaba Cloud OSS backend.
* endpoint - (Required) A custom endpoint for the OSS API.
* bucket - (Required) The name of the OSS bucket..
* accessKeyID - (Required) Alibaba Cloud access key.
* accessKeySecret - (Required) Alibaba Cloud access secret.
### s3 

The s3 backend stores state on Amazon S3.

Example Configuration:
```yaml
backend:
  storageType: s3
  config:
    endpoint: http://localhost:9000
    bucket: kusion-s3
    region: us-east-1
```

Command-line Configuration

```sh
kusion apply -C accessKeyID=********* -C accessKeySecret=*********
```

* storageType - s3, Define Amazon S3 backend.
* endpoint - (Required) Custom endpoint for the AWS S3 API.
* bucket - (Required) Name of the S3 bucket.
* accessKeyID - (Required) AWS access key,
* accessKeySecret - (Required) AWS access secret.

### db

The db backend stores state on database.

Example Configuration:

```yaml
backend:
  storageType: db
  config:
    dbHost: 127.0.0.1
    dbName: kusiondemo
    dbPort: 3306
```

Command-line Configuration
```sh
kusion apply -C dbUser=********* -C dbPassword=**********
```

* storageType - db, Define database backend.
* dbHost - (Required) The host of the database.
* dbName - (Required) The name of the database.
* dbPort - (Required) The port of the database.
* dbUser - (Required) The user of the database.
* dbPassword - (Required) The password of the database.