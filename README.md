# local-s3-minio-sample
This is a thing for to create S3 enviriment in local enviroment.
It can be reproduce public access of S3 bucket.

## Installation
### 0. Setting
You can modify username, password, and bucket name.  
Please modify [.env](./.env) file.

### 1. Launch
```
docker compose up -d
```

### 2. Create bucket(public access)
```
docker compose run --rm create-bucket
```

### Console URL
[http://0.0.0.0:9001](http://0.0.0.0:9001)


## How to use with aws-cli

### 1. Set AWS Access Key and Secret Access Key
```sh
$ aws configure --profile minio
AWS Access Key ID [None]: username
AWS Secret Access Key [None]: password
Default region name [None]:
Default output format [None]:
```


### 2. Use aws-cli with `--endpoint-url` option
```sh
$ aws --profile minio --endpoint-url http://0.0.0.0:9000 s3 ls
```


## How to create public web page

### 1. Create file
```sh
cat - << EOS > index.html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Thanks MINIO</title>
</head>
<body>
    This is static web sites.
</body>
</html>
EOS
```

### 2. Copy to S3
```sh
$ aws --profile minio --endpoint-url http://0.0.0.0:9000 s3 cp ./index.html s3://test-bucket/
```

### 3. Open in Web browser.
[http://0.0.0.0:9000/test-bucket/index.html](http://0.0.0.0:9000/test-bucket/index.html)

