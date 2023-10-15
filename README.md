# BIG_DATA_HDFS
## HDFS
HDFS, or Hadoop Distributed File System, is a distributed file system designed to store and manage very large datasets in a distributed computing environment. It is a key component of the Apache Hadoop ecosystem, which is used for processing and analyzing big data.

## BIG DATA

Big data refers to extremely large and complex data sets that are difficult to manage, process, and analyze using traditional data processing tools and methods. The term "big data" encompasses not only the sheer volume of data but also its variety, value, velocity, and veracity.

## Start Hadoop processes
## Start HDFS service and YARN service
Start the HDFS services and YARN services with the following commands:

`start-dfs.sh`

`start-yarn.sh`

![Alt Text](TP1-TP2/start-dfs-yarn.PNG)

## Check if the services have been started

`jps`

![Alt Text](TP1-TP2/jps.PNG)

## Open the web interface for the NameNode

`http://localhost:50070`

![Alt Text](TP1-TP2/web.PNG)

## Formulate the tree structure below in HDFS

![Alt Text](TP1-TP2/arbo.PNG)

`hdfs dfs -mkdir -p SDIA/{JAVA/{TPs,Cours},PYTHON/{TPs,Cours}}`

![Alt Text](TP1-TP2/directories.PNG)

## Generate files within a directory 

`hdfs dfs -touchz SDIA/PYTHON/Cours/{CoursPY1,CoursPY2,CoursPY3}`

![Alt Text](TP1-TP2/files.PNG)

![Alt Text](TP1-TP2/cours.PNG)


## Add content to files and then view the file contents

`echo "Master SDIA!" | hadoop fs -appendToFile - SDIA/PYTHON/Cours/CoursPY1`

`hdfs dfs -cat SDIA/PYTHON/Cours/CoursPY1`

![Alt Text](TP1-TP2/addContent.PNG)

## Transfer files to a different repository

`hdfs dfs -cp -f SDIA/PYTHON/Cours/{CoursPY1,CoursPY2,CoursPY3} SDIA/JAVA/Cours`

![Alt Text](TP1-TP2/copy.PNG)

## Delete a file

`hdfs dfs -rm SDIA/JAVA/Cours/CoursPY2`

![Alt Text](TP1-TP2/delete.PNG)

## Rename files

`hdfs dfs -mv SDIA/JAVA/Cours/CoursPY1 SDIA/JAVA/Cours/CoursJAVA1`

`hdfs dfs -mv SDIA/JAVA/Cours/CoursPY3 SDIA/JAVA/Cours/CoursJAVA2`

![Alt Text](TP1-TP2/rename.PNG)

## Create file in local 

`touch {TP1CPP,TP2CPP,TP1JAVA,TP2JAVA,TP3JAVA}`

![Alt Text](TP1-TP2/create1.PNG)

## Transfer files from a local source to HDFS

`hdfs dfs -copyFromLocal {TP1CPP,TP2CPP} SDIA/PYTHON/TPs`

![Alt Text](TP1-TP2/fromLocal.PNG)

## Show the contents of the repository

`hdfs dfs -ls -R SDIA`

![Alt Text](TP1-TP2/display.PNG)


## Delete file and directory

`hdfs dfs -rm SDIA/PYTHON/TPs/TP3CPP`

`hdfs dfs -rmr SDIA/JAVA`

![Alt Text](TP1-TP2/remove.PNG)

## Hadoop FileSystem API
The following example demonstrates how to write to a text file in HDFS:
```java
package org.example;


import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.FSDataOutputStream;
import org.apache.hadoop.fs.FileSystem;
import java.io.*;
import org.apache.hadoop.fs.Path;
import java.nio.charset.StandardCharsets;


public class Write {
    public static void main(String[] args) throws IOException {
        Configuration configuration = new Configuration();
        configuration.set("fs.defaultFS","hdfs://localhost:9000");
        FileSystem fileSystem = FileSystem.get(configuration);
        Path path = new Path("/home/bouzyan/TP1CPP/text");
        FSDataOutputStream fsDataOutputStream = fileSystem.create(path);
        BufferedWriter bufferedWriter = new BufferedWriter(new OutputStreamWriter(fsDataOutputStream, StandardCharsets.UTF_8));
        bufferedWriter.write("JAVA1");
        bufferedWriter.newLine();
        bufferedWriter.write("PYTHON");
        bufferedWriter.newLine();
        bufferedWriter.close();
        fsDataOutputStream.close();
    }
}
```




The following example demonstrates how to read from a text file in HDFS:
```java
package org.example;

import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.FSDataInputStream;
import org.apache.hadoop.fs.FileSystem;
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.nio.charset.StandardCharsets;
import org.apache.hadoop.fs.Path;

public class Read {
    public static void main(String[] args) throws IOException {
        Configuration configuration = new Configuration();
        configuration.set("fs.defaultFS","hdfs://localhost:9000");
        FileSystem fileSystem = FileSystem.get(configuration);
        Path path = new Path("/home/bouzyan/TP1CPP/text");
        FSDataInputStream fsDataInputStream = fileSystem.open(path);
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(fsDataInputStream, StandardCharsets.UTF_8));
        String line = null;
        while((line = bufferedReader.readLine()) != null){
            System.out.println(line);
        }
        fsDataInputStream.close();
        bufferedReader.close();
    }
}

```
![Alt Text](TP1-TP2/java.PNG)







