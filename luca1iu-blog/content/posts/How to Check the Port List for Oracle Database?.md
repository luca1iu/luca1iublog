+++
title = 'How to Check the Port List for Oracle Database?'
date = 2023-09-11T21:34:44+08:00
+++


# Introduction
When you want to access a database using Jupyter Notebook or other web-based Python compilers like Datalore, DeepNote, or Google Colab, you may face issues even if you can access the same database using an IDE locally. One possible reason for this issue is that the database you are using does not allow web access.

So, how can you check whether your database allows web access?

# Checking the Port List for Oracle Database
To check the port list for Oracle Database, follow these steps:

1. Log in to Oracle Database using the system administrator account in SQL/PLUS.
2. Run the following command:


```oracle
SELECT DISTINCT PROTOCOL, PORT FROM SYS.V_$LISTENER_NETWORK;
```

This command will show the protocols and ports used by all the listeners in the database. If the command returns a port number, it means that the database is configured to allow web access. If the command returns an empty value or an error, it means that the database is not configured to allow web access.

You can also check the configuration of the current listener by running the following command:

```oracle
LSNRCTL STATUS
```
This command will show the status of the current listener and the protocol and port it uses.

Note: If you do not have system administrator permissions, you may not be able to view the configuration information for all listeners.

# Checking the Port List for MySQL Database
To check the port list for MySQL Database, use the following command:

```mysql
sudo lsof -i -P -n | grep LISTEN | grep mysql
```

This command will show the list of all the ports being listened to by MySQL Database.

# Checking the Port List for Postgres Database
To check the port list for Postgres Database, open a command-line tool and enter the following command:

```mysql
sudo lsof -i -P -n | grep LISTEN | grep postgres
```
This command will show the list of all the ports being listened to by Postgres Database.

# Conclusion
Checking the port list for a database is an important step in troubleshooting web access issues. Hopefully, this article has helped you understand how to check the port list for Oracle, MySQL, and Postgres databases.



