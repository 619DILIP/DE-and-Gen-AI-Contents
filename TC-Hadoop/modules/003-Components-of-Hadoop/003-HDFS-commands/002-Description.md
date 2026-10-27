## Starting Hadoop Services

Before executing any HDFS commands, ensure that the Hadoop Distributed
File System (HDFS) services are running.

    start-dfs.sh

This starts:

-   NameNode
-   Secondary NameNode
-   DataNodes

To verify services:

    jps


## Accessing HDFS

You can interact with HDFS using:

    hdfs dfs

or

    hadoop fs

------------------------------------------------------------------------
## Common HDFS Commands

| Command            | Description                                   |
|--------------------|-----------------------------------------------|
| `-ls`              | List files and directories                   |
| `-mkdir`           | Create a directory                           |
| `-rm -r`           | Remove file or directory recursively         |
| `-rmdir`           | Delete an empty directory                    |
| `-put`             | Upload file from local system to HDFS       |
| `-get`             | Download file from HDFS to local system     |
| `-cat`             | Display file content                         |
| `-du`              | Show file or directory size                  |
| `-count`           | Count directories, files, and total size     |
| `-mv`              | Move file or directory                       |
| `-cp`              | Copy file or directory                       |
| `-setrep`          | Change replication factor                    |
| `-tail`            | Display last part of file                    |
| `-df`              | Show HDFS filesystem space usage             |
| `-touchz`          | Create an empty file                         |
| `-appendToFile`    | Append content to an existing file           |
| `-checksum`        | Display file checksum                        |
| `-find`            | Search for files in HDFS                     |
