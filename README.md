# java-servlet-fileupload

Apache File Upload Stream Data Problem

Author: Software Engineer @ <a href="www.shipshuk.com">Shipshuk</a>

This article explains how to fix the problem of the file uploaded different from the original file. The environment is Apache Tomcat and the code for servlet is java.

The problem underlying is not to check the data received as we have no guarantee of how much data we received. Therefore, some byte received
size check should be implemented before writing in the code.


