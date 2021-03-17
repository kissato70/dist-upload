# dist-upload-s3

## Script for AWS S3 bucket upload from the distribution folder (linux version)

___
**`Installation:`**   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  npm &nbsp;install -g dist-upload-s3  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;or  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  yarn &nbsp;add global dist-upload-s3
___
Using this script you can upload a folder of your project to an Amazaon S3 bucket, store a copy of this release into an other (backup) bucket with rollback ability, where you can set the maximum number of previous releases stored. The releases can be kept in subfolders (branches), which makes it possible to use only one central backup S3 bucket for all your different projects, you can setup your projects to use different branches. Using a backup bucket is optional. 

The parameters can be stored in configuration files, different config files can be used for different purposes. It is not obligatory to use a config file, you can run the command directly with inline parameters too. If a config file is present and you define inline parameters, the params will be merged so, that the inline parameters have the priority. In 'config file write mode' (-w) the inline params will overwrite the params stored in the config file.  

Rollback is replacing (restoring) the main bucket's content with the last previous version. During the rollback, the release is taken off the backup bucket stack (LIFO rules). If you limit the number of release versions, the oldest version is removed above the limit (FIFO). 
___
__`WARNING`:__ Be aware of keeping your config file away of your public Git repository and never publish it with your files! It doesn't contain your Amazon password, but the names of your buckets, which are public readable (and if you not set up it's access policy correctly, even publicly writeable)!!! So, make sure, your .gitignore file contains the name of the config file, even so the backup bucket is hidden from the public by having no public access, and the main bucket (used for static website hosting) is not writeable, by limiting the write access for your AWS role only.  

__The script is not sending out any of your passwords or sensitive data, storing everything locally.__

___

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
_The script will ask for all the setup parameters and save it to the default config file._  
<br><br>
**Creating a special config file (for example for staging):**
```script
dist-upload-s3 -c myTestConfig -w
```
_This will create a config file 'myTestconfig', which can be used for alternative uploads._
<br><br>
**Uploading using a previously configured other config:**
```bash
dist-upload-s3 -c otherConfig
```
_The config file 'otherConfig' is used, which can have different settings, like other bucket, other dist folder, any other setup params, you just like._  
<br/><br/>
**Sending this complete startup setup along with the project to the team:**
```bash
dist-upload-s3 -w -d dist  -b ourProdBucket -i ourProdBackup -m 5
dist-upload-s3 -w -d build -b ourTestBucket -i off -c stage
```
_The script will ask for the personal AWS access keys._<br>
_Hint: Place the above into the package.json under the 'scripts' like this:  
   `"start:init" : "dist-upload-s3 -w -d dist ..."`_
<br><br>
**Updating the config file, by changing ONLY the given params**<br>
```script
dist-upload-s3 -c myConfig -w -y -i off -r eu-west-1
```  
_In the above example we switch off the backup and changing the region in the config setup 'myConfig'._  
Without the -y flag, the script would ask for all the params, by offering the previously set values.

&nbsp;<br>

**Uploading the folder 'test_build' to the 'stageBucket' in silent mode, while using the branch folder name 'stage':**
```bash
dist-upload-s3 -d test_build -S -b stageBucket -f stage
```    
_Please note: All other config parameters are taken from the default config file. There is no need to use an other backup bucket by using a different branch (folder)._  
_Hint: You can place all these parameters into a separate config file too._  
<br/><br/>
**Listing the backup folder content, but only the last 3 versions:**
```bash
dist-upload-s3 -l 3
```  
_You could use the -f flag for listing an other branch (folder)._
&nbsp;<br/><br/>  

**Uploading the dist folder (as set in the default config) by leaving only 5 older versions alive, showing no status messages(silent mode):**
```bash
dist-upload-s3 -m 5 -S
```
_Any older versions above the number (in this example: 5), will be deleted._
<br/><br/>
___
<br/>  

>Written by: __Attila Kiss__, [e-LET Kft](https://e-let.hu), Hungary  ( GitHub: [kissato70](https://github.com/kissato70) )

 > Licence:  MIT

> Report issues [here](https://github.com/kissato70/dist-upload-s3/issues).

<br>  

## Buy me a beer >>> [Donation](https://bit.ly/kissato70_paypal_donate)  
_Please support the further releases (I have no proper job right now), if you like this script! **Thank you!**_
## Future enhancement plans:
- Do not store but ask for password
- Same functionality for linux servers, using rsync
- Merging config files
- Notification sending to team members, if an upload is done
- Maybe a Node version for the poor Win users...
<br/><br/>  

_(And ... sorry for my 'Hunglish'...)_
