jBASE-SQL-Server-ETL
====================

Blazing Fast Data Extraction from jBASE to SQL Server

The jBASE-SQL Server ETL is a suite of utilities that work together to extract and load data from jBASE to SQL Server securely. 

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

##Installation  

The following utilities and configuration files will be created once the installation has completed:

![Image Alt](http://eztier.com/documentation/t24/jbase-sql-etl/images/ownerobjects/installed-utilities.png)
