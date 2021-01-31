# dist-upload

## Script for AWS S3 bucket upload from the distribution folder

### Last release version: __1.1.0__

__Syntax__:  dist-upload [params]

_Optional params:_

   -c    (configFile)          The name of the config file to save (-w) or use. [aws.distconfig]

   -w                          Config file write mode, for creating configuration(s).

   -p    (profileName)         Sets the AWS profile name. [default]

   -r    (regionName)          Sets the AWS region name for the profile. [us-east-1]

   -a    (accessKey)           Sets the AWS IAM user's access_key for the profile.

   -s    (secretKey)           Sets the AWS IAM user's secret_access_key for the profile.

   -g    (true|[false])        Should the name of the config file be added to .gitignore file.

   -d    (distDirectory)       Sets the distribution directory. [dist]

   -b    (bucketName)          Sets the AWS S3 bucket name in config.

   -i    (bucketName|off)      Sets the AWS S3 bucket name for incremental release backup in config.

   -R                          Rollback (undo) release: Rolls back the code to previsous state, deleting the last release.

   -m    (versionLimit)        The maximum number of versions kept in the bucket. Older will be deleted.

   -f    (branchFolder)        The folder for automated version storage. You can store different branches this way.

   -l    [tailNumber]          Lists [the last n number of] the release versions in the incremental backup bucket.

   -y                          Answers default option to the config questions. Hint: use for changing only the given params.

   -S                          Silent mode. Hides all the information about the process.

## Examples
_To configure the system, as the first step:_
```script
dist-upload -w
```
_Creating a special config file:_
```script
dist-upload -c myConfig -w
```
_Updating the config file, changing one or multiple params_
_(For example switching off the backup):_
```script
dist-upload -c myConfig -w -y -i off
```
_Uploading the 'build' folder (forcing the folder) in silent mode, while using the branch name 'stage':_
```bash
dist-upload -d build -S -f stage
```
_Listing the backup folder content:_
```bash
dist-upload -l
```
  >Written by: __Attila Kiss__, [e-LET Kft](https://e-let.hu), Hungary  ( GitHub: [kissato70](https://github.com/kissato70) )

  Licence:  MIT
