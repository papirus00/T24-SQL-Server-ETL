T24-SQL-Server-ETL
====================

Blazing Fast Data Extraction from T24 to SQL Server

The T24-SQL Server ETL is a suite of utilities that work together to extract and load data from jBASE to SQL Server securely. 

It operates with as little abstraction as possible. No jBASIC, no Java, just raw unadulterated speed.

Network communications are done through secured channels such as SSH2 and SSPI. File encryption and decryption are done in the application runtime and data is never written to disk in plain text. 

The ETL not only gets the data securely from jBASE to SQL Server but it's also fast, really fast. 

![Image Alt](http://eztier.com/documentation/t24/jbase-sql-etl/images/ownerobjects/architecture-0.png)

##Threadpool

All ETL processes are multi-threaded. A typical routine is as follows:

- The main thread parses the 'jobs' XML file for information such as work path and file names.  
- The main thread stores the above information in a runtime queue.  
- The main thread creates a threadpool which contains a collection of semaphore threads.  
- The threadpool threads do not actually do the work like the classic pattern.  
- Instead, the threadpool threads are responsible for initiating and waiting for a process to end.  
- When the semaphore-invoked process completes, the semaphore will look for another job  

![Image Alt](http://eztier.com/documentation/t24/jbase-sql-etl/images/ownerobjects/threadpool-0.png)

####What's the deal with the "++" naming convention?
- Libraries and executables compiled as C/C++ are named with "++" at the end.  Else, they are .NET.

####Why are you putting this in GitHub?
- When I authored this, the suite of tools were compiled with Visual Studio 2008 and works in 64-bit Windows OS.  
  I am hoping to migrate everything to work in Linux.  Contributors welcome!

##Installation  

The following utilities and configuration files will be created once the installation has completed:

![Image Alt](http://eztier.com/documentation/t24/jbase-sql-etl/images/ownerobjects/installed-utilities.png)

##Logging

All ETL executables generate logs during processing for each session in the work folder (for more details, click on the "Logging" tab):

![Image Alt](http://eztier.com/documentation/t24/jbase-sql-etl/images/ownerobjects/logging-summary-0.png)

All executables that invoke ETL processes generate logs in the "#log" folder under the "[installation directory]\bin" folder (for more details, click on the "Logging" tab):

![Image Alt](http://eztier.com/documentation/t24/jbase-sql-etl/images/ownerobjects/logging-summary-1.png)

##Utilities

Brief Descriptions of Installed Components:


####etlcommon.dll 

- Library containing reusable objects shared by managed executables.
  
####etlctrl.exe 

- Creates dynamic jQL based on user-defined configuration files.•Exports job files for all processes based on user-defined configuration files.•Creates the key file for encryption and decryption used by all processes.
  
####etlexec++.exe 

- Starts processes sequentially based on user-defined configuration file.
  
####etlmodel.exe 

- Extracts schemas for all tables defined in FileDefineExplode.xml from ODSDB.•Exports the above as FileDefineExplodeModel.xml.•The exported file is used by tinyupload2.exe.
  
####etllog.exe 

- Constructs flat file and SQL reports from logs created by ETL processes.
  
####etlsecure.exe 

- User application to encrypt SSH2 credentials.
  
####filesystem++.dll 

- Library used for file searching shared by unmanaged executables.
  
####libssh2.dll 

- Open source client-side unmanaged library implementing SSH2 protocol.
  
####libeay32.dll 

- Open source unmanaged library containing encryption functions.
  
####threadpool++.dll 

- Library for threadpool creation shared by unmanaged executables.
  
####tinybuild2++.exe 

- Imports job file created by etlctrl.exe and creates a task queue from it.•Manages the build process in a threadpool.•Only process where threadpool threads are both semaphores and workers.
  
####tinydecrypt++.exe 

- User application to decrypt selected encrypted files.
  
####tinydownload2.exe 

- SSH2 client that downloads data from jBASE.•Encrypts the data and exports them to disk.
  
####tinydownload++.exe 

- Imports job file created by etlctrl.exe and creates a task queue from it.•Manages the download process in a threadpool.•The threadpool initiates multiple tinydownload2.exe instances.
  
####tinyencrypt++.dll 

- Library used for file encryption and decyption shared by all processes.•Used by etlctrl.exe for generating the session key.
  
####tinyexplode2.exe 

- Explodes jBASE multi/sub values.•Explode definitions is read from FileDefineExplode.xml.•The data source are raw jBASE data that has been built and uploaded to SQL.•Encrypts the exploded data and exports them to disk.
  
####tinyexplode.exe 

- Imports job file created by etlctrl.exe and creates a task queue from it.•Manages the explode process in a threadpool.•The threadpool initiates multiple tinyexplode2.exe instances.
  
####tinyupload2.exe 

- Uploads raw jBASE and exploded data to SQL.•Converts data to SQL type if table schema is defined in FileDefineExplodeModel.xml.
  
####tinyupload.exe 

- Imports job file created by etlctrl.exe and creates a task queue from it.•Manages the upload process in a threadpool.•The threadpool initiates multiple tinyupload2.exe instances.•Creates the SQL tables for raw jBASE data exploded data.
  
####xmlread++.dll

- Library used for reading XML files shared by unmanaged executables.

