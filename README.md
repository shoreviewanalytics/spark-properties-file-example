
Having clean understandable code is important. Doing things like adding comments, so someone looking at your code can follow it, can go a long way.  This example uses a java .properties file to provide a flexible way to pass values such as the job name, the location for logback.xml file to the compiled code of the spark job. It's important to note that the .properties file used in this example doesn't need to be placed or referenced within the actual source code of the project.  However, it does need to be able to be found at runtime by the spark submit process.  As you review this example you will notice that there is line where the path is being read. You can use the default path or amend it, so your job can find the .properties file.  The path is relative to the directory where you deploy your .jar file on a server.  For example, if your jar is in a folder called jobs, you can configure your code to look for the .properties file in a subdirectory of the jobs folder or a nested folder called 'config' as is the case for this example.  This example can be run on a single node DataStax Enterprise (DSE) cluster with Analytics enabled or a multi-node (DSE) cluster with Analytics enabled.   

Similar to spark-logback-example-two job, this example job doesn't require the use of --driver-java-options "=Dlogback.configurationFile=" option with spark-submit as found in spark-logback-example-one.  The reference to a specific logback.xml file can be shared between jobs or you could create custom logback.xml file for each job using a name like application_name.logback.xml.  The logback.xml file is configured with a parameter ${jobname}, which takes a value set within the job using System.setProperty to provide the job name.  The job name is set in the .properties file.   

To run:

dse -u cassandra -p yourpassword spark-submit --class com.java.spark.SparkPropertiesFileExample /pathtojobsfolderonyourserver/spark-properties-file-example-0.1.jar

Configuration and Data Files:

Configuration and data files are located in the src/main/resources folder.  You will need to place these files in the appropriate location based upon your development and server environment.  