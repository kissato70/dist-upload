# dist-upload-s3

## Script for AWS S3 bucket upload from the distribution folder (linux version)

### Latest stable version: __1.1.x__

<br>

**`Syntax:`** &nbsp;  `dist-upload-s3` &nbsp;  [optional params]

| option | argument | description |
|------------ | ------ | ------------ |
|  -c  |  configFile  |        The name of the config file to save (-w) or use. [aws.distconfig] |
|   -w |     |                    Config file write mode, for creating configuration(s).|
|   -p |   profileName  |       Sets the AWS profile name. [default]|
|   -r |   regionName  |        Sets the AWS region name for the profile. [us-east-1]|
|   -a |   accessKey  |         Sets the AWS IAM user's access_key for the profile.|
|   -s |   secretKey   |        Sets the AWS IAM user's secret_access_key for the profile.|
|   -g |  true \| [false]  |       Should the name of the config file be added to .gitignore file.|
|   -d |   distDirectory |      Sets the distribution directory. [dist]|
|   -b |   bucketName |       Sets the AWS S3 bucket name in config.|
|   -i |   bucketName \| off |     Sets the AWS S3 bucket name for incremental release backup in config.|
|   -R   |       |                Rollback (undo) release: Rolls back the code to previsous state, deleting the last release.|
|   -m  |  versionLimit  |      The maximum number of versions kept in the bucket. Older will be deleted.|
|   -f |   branchFolder  |      The folder for automated version storage. You can store different branches this way.|
|   -l |   tailNumber  |        Lists [optionaly the last n number of] the release versions in the incremental backup bucket.|
|   -y   | |                       Answers default option to the config questions. Hint: use for changing only the given params.|
|   -S  | |                        Silent mode. Hides all the information about the process.|

&nbsp;
## `Examples`
**To configure the system, as the first step:**
```script
dist-upload-s3 -w
```
_The script will ask all the setup parameters and save it to the default config file._
<br><br>
**Creating a special config file (for example for staging):**
```script
dist-upload-s3 -c myTestConfig -w
```
_This will create a config file 'myTestconfig', which can be used for alternative uploads._
<br><br>
**Sending this complete startup setup along with the webpack config to the team:**
```bash
dist-upload-s3 -w -d dist  -b ourProdBucket -i ourProdBackup -m 5
dist-upload-s3 -w -d build -b ourTestBucket -i off -c stage
```
_The script will ask for the personal AWS access keys._<br>
_Hint: Place the above into the package.json under the 'scripts' like this:   `"init" : "dist-upload-s3 -w dist ..."`_
<br><br>
**Updating the config file, changing ONLY the given params**<br>
(In this example switching off the backup and changing the region):
```script
dist-upload-s3 -c myConfig -w -y -i off -r eu-west-1
```
&nbsp;<br>
**Uploading the folder 'test_build' (other than the folder set in config) in silent mode, while using the branch name 'stage':**
```bash
dist-upload-s3 -d test_build -S -f stage
```
&nbsp;<br>
**Listing the backup folder content, but only the last 3 versions:**
```bash
dist-upload-s3 -l 3
```
&nbsp;<br>
**Uploading the dist folder (as set in the config) by leaving only 5 older versions alive, without status messages:**
```bash
dist-upload-s3 -m 5 -S
```
_Any older versions above the number, will be deleted._
<br><br>
**Uploading to the previously configured staging area:**
```bash
dist-upload-s3 -c stage
```
&nbsp;
>Written by: __Attila Kiss__, [e-LET Kft](https://e-let.hu), Hungary  ( GitHub: [kissato70](https://github.com/kissato70) )

 > Licence:  MIT

<br>

> **Buy me a beer (Donation):** http://bit.ly/kissato70_donate
