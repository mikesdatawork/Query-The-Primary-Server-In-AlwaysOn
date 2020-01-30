![MIKES DATA WORK GIT REPO](https://raw.githubusercontent.com/mikesdatawork/images/master/git_mikes_data_work_banner_01.png "Mikes Data Work")        

# Query The Primary Server In AlwaysOn
**Post Date: August 17, 2016**        



## Contents    
- [About Process](##About-Process)  
- [SQL Logic](#SQL-Logic)  
- [Build Info](#Build-Info)  
- [Author](#Author)  
- [License](#License)       

## About-Process

<p>Here's another quick way you can query the primary server. I've posted about this before sure; but that was using a precise result. If you wanted to see all servers involved you can use this little number. It works by simply looking at the [ROLE_DESC] value from sys.dm_hadr_availability_replica_states. Simply put… If the PRIMARY is listed, then you are on the Primary server because the Primary will show the servers involved in the AlwaysOn configuration.
If this is run from the Secondary server then the PRIMARY value from the [ROLE_DESC] will not be listed. It's a simple method to determine which server is which. I use this with certain automation logic as a quick check before any processes are carried out. This particular example is of an old Sharepoint 2013 environment which is using an OS of Server 2012 environment with SQL Server 2014. Ancient at this point but doesn't hurt to mention it.</p>  



## SQL-Logic
```SQL
use master;
set nocount on
set ansi_warnings off
 
select * from sys.dm_hadr_availability_replica_states;
 
if exists(select role_desc from sys.dm_hadr_availability_replica_states where role_desc in ('primary'))
    begin
        print 'The Primary role was found.'
    end
    else
        print 'The Primary role was NOT found.'
```

![Query Primary AlwaysOn Server]( https://mikesdatawork.files.wordpress.com/2016/08/image0011.png "Query Primary AlwaysOn Server With SQL")
 


[![WorksEveryTime](https://forthebadge.com/images/badges/60-percent-of-the-time-works-every-time.svg)](https://shitday.de/)

## Build-Info

| Build Quality | Build History |
|--|--|
|<table><tr><td>[![Build-Status](https://ci.appveyor.com/api/projects/status/pjxh5g91jpbh7t84?svg?style=flat-square)](#)</td></tr><tr><td>[![Coverage](https://coveralls.io/repos/github/tygerbytes/ResourceFitness/badge.svg?style=flat-square)](#)</td></tr><tr><td>[![Nuget](https://img.shields.io/nuget/v/TW.Resfit.Core.svg?style=flat-square)](#)</td></tr></table>|<table><tr><td>[![Build history](https://buildstats.info/appveyor/chart/tygerbytes/resourcefitness)](#)</td></tr></table>|

## Author

[![Gist](https://img.shields.io/badge/Gist-MikesDataWork-<COLOR>.svg)](https://gist.github.com/mikesdatawork)
[![Twitter](https://img.shields.io/badge/Twitter-MikesDataWork-<COLOR>.svg)](https://twitter.com/mikesdatawork)
[![Wordpress](https://img.shields.io/badge/Wordpress-MikesDataWork-<COLOR>.svg)](https://mikesdatawork.wordpress.com/)

      
## License
[![LicenseCCSA](https://img.shields.io/badge/License-CreativeCommonsSA-<COLOR>.svg)](https://creativecommons.org/share-your-work/licensing-types-examples/)

![Mikes Data Work](https://raw.githubusercontent.com/mikesdatawork/images/master/git_mikes_data_work_banner_02.png "Mikes Data Work")

