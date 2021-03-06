# Beanstalk upload persistance using EFS
.ebextensions based config files for EFS mounting and cron job based sync of local vol to efs.

Uses cron and rsync to sync assets dir from EFS on to local storage at startup and local storage to efs periodically - every hour at 15, 30, 45 mins. 
Configure parameters like EFS volume, ASSET_SRC_DIR at .ebextensions/00env_param_init.config

For EFS mount to work seamlessly, ensure NFS traffic (port 2049) is enabled within default VPC. 

## EFS Creation Steps 
1. Create/Edit security group that allows NFS traffic within VPC 
   - This could be easily done by adding an inbound rule for default security group that allows NFS traffic from 172.16.0.0/12 subnet. If default security group is edited, step 3 below could be avoided. 
2. Create EFS volume via AWS console.
3. Use the above security group to the created volume's network configuration.
4. Set the EFS volume's FS id  as FILE_SYSTEM_ID param in 00env_param_init.config available under the folder .ebextensions.

[Detailed Steps with Screenshots](docs/EFSCreate.md)

