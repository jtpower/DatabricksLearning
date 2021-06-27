# Visual Studio Code as develop client tool connect to Azure Databricks by remotely
## Softwares Download
| ID | Production Name | Download |
| --- | --- | --- |
| 1 | Anaconda Python | [URL](https://www.anaconda.com/products/individual) |
| 2 | Java SE Development Kit 8u291 | [URL](https://www.oracle.com/es/java/technologies/javase/javase-jdk8-downloads.html) |
| 3 | WinUtils | [URL](https://github.com/steveloughran/winutils) |

## Configure Windows OS environment
Extract the appropriate version of the Hadoop folder
[<img src="./000-pictures/WinUtils.png" width="75%"/>]()
### Add environment variable - HADOOP_HOME
[<img src="./000-pictures/000-SystemEnvironmentVariables.png" width="400"/>]()<br/>
[<img src="./000-pictures/001-SystemEnvironmentVariables.png" width="400"/>]()<br/>
[<img src="./000-pictures/002-SystemEnvironmentVariables.png" width="400"/>]()
### Apply to PATH
[<img src="./000-pictures/004-SystemEnvironmentVariables.png" width="400"/>]()<br/>
[<img src="./000-pictures/003-SystemEnvironmentVariables.png" width="400"/>]()
## Create ***python environment*** and ***specific version***
```cmd
PATH>conda create --name dbconnect python=3.7
PATH>conda activate dbconnect
```
> P.S. Execution result as below:
```cmd
Microsoft Windows [Version 10.0.19043.1052]
(c) Microsoft Corporation. All rights reserved.

PATH>conda create --name dbconnect python=3.7
Collecting package metadata (current_repodata.json): done
Solving environment: done

## Package Plan ##

environment location: C:\ProgramData\Anaconda3\envs\dbconnect 

added / updated specs:
    - python=3.7


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    ca-certificates-2021.5.25  |       haa95532_1         112 KB
    certifi-2021.5.30          |   py37haa95532_0         139 KB
    pip-21.1.2                 |   py37haa95532_0         1.8 MB
    python-3.7.10              |       h6244533_0        14.5 MB
    setuptools-52.0.0          |   py37haa95532_0         711 KB
    sqlite-3.36.0              |       h2bbff1b_0         780 KB
    wincertstore-0.2           |           py37_0          14 KB
    ------------------------------------------------------------
                                        Total:        17.9 MB

The following NEW packages will be INSTALLED:

ca-certificates    pkgs/main/win-64::ca-certificates-2021.5.25-haa95532_1
certifi            pkgs/main/win-64::certifi-2021.5.30-py37haa95532_0
openssl            pkgs/main/win-64::openssl-1.1.1k-h2bbff1b_0
pip                pkgs/main/win-64::pip-21.1.2-py37haa95532_0
python             pkgs/main/win-64::python-3.7.10-h6244533_0
setuptools         pkgs/main/win-64::setuptools-52.0.0-py37haa95532_0
sqlite             pkgs/main/win-64::sqlite-3.36.0-h2bbff1b_0
vc                 pkgs/main/win-64::vc-14.2-h21ff451_1
vs2015_runtime     pkgs/main/win-64::vs2015_runtime-14.27.29016-h5e58377_2
wheel              pkgs/main/noarch::wheel-0.36.2-pyhd3eb1b0_0
wincertstore       pkgs/main/win-64::wincertstore-0.2-py37_0


Proceed ([y]/n)? Y


Downloading and Extracting Packages
python-3.7.10        | 14.5 MB   | ################################################################################################################ | 100% 
certifi-2021.5.30    | 139 KB    | ################################################################################################################ | 100%  
pip-21.1.2           | 1.8 MB    | ################################################################################################################ | 100%  
wincertstore-0.2     | 14 KB     | ################################################################################################################ | 100%  
sqlite-3.36.0        | 780 KB    | ################################################################################################################ | 100%  
ca-certificates-2021 | 112 KB    | ################################################################################################################ | 100%  
setuptools-52.0.0    | 711 KB    | ################################################################################################################ | 100%  
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate dbconnect
#
# To deactivate an active environment, use
#
#     $ conda deactivate
```

## Install ***the databricks-connect*** tools
```cmd
(dbconnect) PATH>pip uninstall pyspark
(dbconnect) PATH>pip install -U "databricks-connect==6.4.*"
```

> P.S. Execution result as below:
```cmd
(base) PATH>conda activate dbconnect

(dbconnect) PATH>pip uninstall pyspark
WARNING: Skipping pyspark as it is not installed.

(dbconnect) PATH>pip install -U "databricks-connect==6.4.*"
Collecting databricks-connect==6.4.*
  Downloading databricks-connect-6.4.28.tar.gz (246.1 MB)
     |████████████████████████████████| 246.1 MB 7.2 kB/s
Collecting py4j==0.10.7
  Downloading py4j-0.10.7-py2.py3-none-any.whl (197 kB)
     |████████████████████████████████| 197 kB ...
Collecting six
  Downloading six-1.16.0-py2.py3-none-any.whl (11 kB)
Building wheels for collected packages: databricks-connect
  Building wheel for databricks-connect (setup.py) ... done
  Created wheel for databricks-connect: filename=databricks_connect-6.4.28-py2.py3-none-any.whl size=246650709 sha256=9bc7f00efb14f63a43e5d026a4f9b1e672d5b1ee0f13916690067c595052bf44
  Stored in directory: c:\users\{USERNAME}\appdata\local\pip\cache\wheels\71\1f\a9\f0aef5ec3edc62974448dae33a8ac996f7c2142ce1f813eb1c
Successfully built databricks-connect
Installing collected packages: six, py4j, databricks-connect
Successfully installed databricks-connect-6.4.28 py4j-0.10.7 six-1.16.0
```
## Configure databricks-connect to ***connect existing*** azure databricks workspace
```cmd
(dbconnect) PATH>databricks-connect configure
```
> P.S. Execution result as below:
```cmd
(dbconnect) PATH>databricks-connect configure
Copyright (2018) Databricks, Inc.

This library (the "Software") may not be used except in connection with the
Licensee's use of the Databricks Platform Services pursuant to an Agreement
(defined below) between Licensee (defined below) and Databricks, Inc.      
("Databricks"). This Software shall be deemed part of the "Subscription    
Services" under the Agreement, or if the Agreement does not define
Subscription Services, then the term in such Agreement that refers to the  
applicable Databricks Platform Services (as defined below) shall be        
substituted herein for "Subscription Services."  Licensee's use of the     
Software must comply at all times with any restrictions applicable to the  
Subscription Services, generally, and must be used in accordance with any
applicable documentation. If you have not agreed to an Agreement or otherwise
do not agree to these terms, you may not use the Software.  This license
terminates automatically upon the termination of the Agreement or Licensee's
breach of these terms.

Agreement: the agreement between Databricks and Licensee governing the use of
the Databricks Platform Services, which shall be, with respect to Databricks,
the Databricks Terms of Service located at www.databricks.com/termsofservice,
and with respect to Databricks Community Edition, the Community Edition Terms
of Service located at www.databricks.com/ce-termsofuse, in each case unless
Licensee has entered into a separate written agreement with Databricks
governing the use of the applicable Databricks Platform Services.

Databricks Platform Services: the Databricks services or the Databricks
Community Edition services, according to where the Software is used.

Licensee: the user of the Software, or, if the Software is being used on
behalf of a company, the company.

Do you accept the above agreement? [y/N] Y
Set new config values (leave input empty to accept default):
Databricks Host [no current value, must start with https://]: https://adb-8092895524158237.1.databricks.azure.cn/
Databricks Token [no current value]: dapi101ce8980018ab4309449697440f316c

IMPORTANT: please ensure that your cluster has:
- Databricks Runtime version of DBR 5.1+
- Python version same as your local Python (i.e., 2.7 or 3.5)
- the Spark conf `spark.databricks.service.server.enabled true` set

Cluster ID (e.g., 0921-001415-jelly628) [no current value]: 0622-080046-bogs604
Org ID (Azure-only, see ?o=orgId in URL) [0]: 8092895524158237
Port [15001]: 

Updated configuration in C:\Users\{USERNAME}/.databricks-connect
* Spark jar dir: c:\programdata\anaconda3\envs\dbconnect\lib\site-packages\pyspark\jars
* Spark home: c:\programdata\anaconda3\envs\dbconnect\lib\site-packages\pyspark
* Run `pip install -U databricks-connect` to install updates
* Run `pyspark` to launch a Python shell
* Run `spark-shell` to launch a Scala shell
* Run `databricks-connect test` to test connectivity

Databricks Connect User Survey: https://forms.gle/V2indnHHfrjGWyQ4A
```

## Test databricks-connect tools
```cmd
(dbconnect) PATH>databricks-connect test
```
> P.S. Execution result as below:
[<img src="./000-pictures/005-Result.png" width="75%"/>]()<br/>
[<img src="./000-pictures/006-Result.png" width="75%"/>]()<br/>
[<img src="./000-pictures/007-Result.png" width="75%"/>]()

Done!

## Reference
* https://docs.microsoft.com/en-us/dotnet/spark/how-to-guides/windows-instructions
* https://docs.microsoft.com/zh-cn/azure/databricks/dev-tools/databricks-connect