---
title: "Personal Website Technical Update 2"
date: 2018-03-20T17:02:09+05:30
draft: false
tags: [ "Personal", "Hugo", "AWS", "S3", "CodeBuild", "CloudFront" ]
---

This is an update on the technical stack of my website. I was able to get [Hugo site](https://hugogo.io) 
hosted on [S3](https://aws.amazon.com/s3/) based website hosting. I then setup [CloudFront](https://aws.amazon.com/cloudfront/) based distribution with 
S3 bucket as Origin. I used CloudFront, not for performance reasons, but to enable 
HTTPS support.  I created custom SSL certification using [ACM](https://aws.amazon.com/certificate-manager/) and set up my custom 
domain to point to CloudFront distribution using [Route53](https://aws.amazon.com/route53/). I set up the whole process 
as [CodeBuild](https://aws.amazon.com/codebuild/) script. 

Below are some of the notes for each software stack to get this whole setup working.

## Hugo
1. Ensure that your baseUrl in your config.toml ends with /, if not URLs will not be correct.
2. If you are using git for your code repository, ensure you have some files in empty directories 
as git does not store empty directories.

## S3
1. Ensure you have enabled website hosting for your S3 bucket.

## CodeBuild
1. Attached is the buildSpec.yml file for CodeBuild.

```
version: 0.2

phases:
  install:
    commands:
      - echo Build started on `date`
      - echo Installing Hugo
      - cd ~
      - wget https://github.com/gohugoio/hugo/releases/download/v0.37.1/hugo_0.37.1_Linux-64bit.deb
      - dpkg -i hugo*.deb
      - hugo version
  build:
    commands:
      - echo BUILD phase commands
      - cd $CODEBUILD_SRC_DIR
      - pwd
      - hugo -v
      - aws s3 ls
      - aws s3 sync --delete public s3://{bucketname}
  post_build:
    commands:
      - echo Build completed on `date`
artifacts:
  files:
```

## CloudFront
1. Ensure that you are pointing to S3 website hosting endpoint.
2. Make sure Origin setttings are point to the exact location in S3 bucket.
3. Ensure that you update Hugo site's baseUrl CloudFront distribution url.
