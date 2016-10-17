# MYSQL-Cloud Backup Script!!

This script will help you to manage your backups;

# Setup

Register for Google Cloud Services
Install gsutil https://developers.google.com/storage/docs/gsutil_install

Create a bucket in the Cloud Console

Configure gsutil to work with your account

gsutil config
Put the mysqltogooglecloud.sh file somewhere in your server, like /opt/local

Give the file 755 permissions chmod 755 /opt/local/mysqltogooglecloud.sh or via FTP
Edit the variables near the top of the mysqltogooglecloud.sh file to match your bucket and MySQL authentication
Now we're set. You can use it manually:

#set a new daily backup, and store the previous day as "previous_day"
sh /opt/local/mysqltogooglecloud.sh

#set a new weekly backup, and store previous week as "previous_week"
/opt/local/mysqltogooglecloud.sh week

#set a new weekly backup, and store previous month as "previous_month"
/opt/local/mysqltogooglecloud.sh month
But, we don't want to think about it until something breaks! So enter crontab -e and insert the following after editing the folders

# daily MySQL backup to Google Cloud (not on first day of month or sundays)
0 3 2-31 * 1-6 sh /opt/local/mysqltogooglecloud.sh day
# weekly MySQL backup to Google Cloud (on sundays, but not the first day of the month)
0 3 2-31 * 0 sh /opt/local/mysqltogooglecloud.sh week
# monthly MySQL backup to Google Cloud
0 3 1 * * sh /opt/local/mysqltogooglecloud.sh month
Or, if you'd prefer to have the script determine the current date and day of the week, insert the following after editing the folders

# automatic daily / weekly / monthly backup to Google Cloud.
0 3 * * * sh /opt/local/mysqltogooglecloud.sh auto
And you're set.

For Troubleshooting please contact me.
