# dist-upload

## Configurator script for AWS S3 bucket upload from the distribution folder

### Last release version: 1.1.0

Command:  dist-upload [params]

  Optional params:

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


  Written by: Attila Kiss, e-LET Kft, Hungary  ( GitHub: kissato70 )

  Licence:  MIT
