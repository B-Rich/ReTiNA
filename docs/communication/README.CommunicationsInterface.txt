############################################################
README file for Communications Interface module of Real Time Network Analysis system
Author: Daniel Sawyer
Date: 1 May 2010
############################################################

Overview:

This module contains 3 python scripts(AttacksDB.py, StatsDB.py, and NodeDB.py), 3 cgi-scripts(StatsReport.cgi, AttackReport.cgi, and NodeReport.cgi), a Database Wrapper written in python(DatabaseWrapper.py), a MySQL database, and an Apache Web Server 

Python Scripts: Python 2.6 must be installed in order to execute these scripts. Each of the python scripts must have  a copy of the DatabaseWrapper.py in its working directory. A config file named config.py must also be present containing an associative array defining the hostname, database name, username, and password for the database being used. 

AttackDB.py: This script will parse logs generated by the attack detection module. It will insert a each attack listed as a row in the database and generate a timestamp to associate each group of attacks that is entered into the database. 

StatsDB.py: This script will parse logs generated by the Traffic Bandwidth Module. It will enter each group of statistics as a row in the database and generate a timestamp for each entry.

NodeDB.py: This script will parse logs generated by the Node Detection Module. It will enter a row in the database for each node detected in the network containing all relevant information about that node. This module will also ensure that only a current list of nodes is maintained in the database, each time is parses a log file it will clear the database table of all old node entries and update it to contain only those nodes that are currently in the network. 

Cgi-Scripts: The cgi-scripts are written in Python, and must also have Python 2.6 installed. Also, in order to host these scripts, an Apache Web server must be installed, and these scripts must be placed in a folder that is accessible by the server. A copy of the DatabaseWrapper.py must be in the same directory from where these scripts are hosted. Also, a config file named config.py must also be present containing an associative array defining the hostname, database name, username, and password for the database being used. 

AttackReport.cgi: This script required a GET variable to be passed to it that is named timestamp and contains the unix timestamp of the time at which the page was last visited or 0 if never previously visited. It will then query the database for all attacks which occured at an earlier time than the timestamp given. From the queried data, the script will then construct an XML document that is echoed to the page.

StatsReport.cgi: This script required a GET variable to be passed to it that is named timestamp and contains the unix timestamp of the time at which the page was last visited or 0 if never previously visited. It will then query the database for all statistical entries which occured at an earlier time than the timestamp given. From the queried data, the script will then construct an XML document that is echoed to the page.

NodeReport.cgi: When visited this page will query the database for a list of all node's that are currently in the network. From the queried data, the script will then construct an XML document that is echoed to the page.

MySQL Database: The database that is used must contain a schema with three tables that are named: `stats`, `attacks`, and `nodestats`. The schema name is currently `mydb`, however this name may be changed so long as it is specified in the configuration file. Also, the database username and password are currently root:rootPW, however these may also change so long as they are specificed in the configuration file. The database wrapper config file also currenly is using 'localhost' as the hostname, but this may also be changed to reflect the ip address of the database. The structure of each table must be according to the models specified in the ReTiNA Requirement Document.

Installation:

As each of the scripts for this module, are interpreted the only installation required is the installing of Python 2.6, MySQL, and an Apache Webserver. The MySQL database must be configured as outlined in the ReTiNA requirement document, the Apache Server must be able to host a directory which contains the 3 cgi-scripts, and each of the python scripts must be placed in the same directory from where the logfiles that they parse are being generated. Also, the DatabaseWrapper and its configuration file must be present in each of the working directories of the cgi and python scripts. 

Running:

This module runs as a webserver in the background.  All function calls required once the service has been started are handled by the other ReTiNA modules

