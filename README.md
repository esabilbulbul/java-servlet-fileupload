# java-servlet-fileupload

Apache File Upload Stream Data Problem

Author: Software Engineer @ <a href="www.shipshuk.com">Shipshuk</a>

This article explains how to fix the problem of the file uploaded different from the original file. The environment is Apache Tomcat and the code for servlet is java.

The problem underlying is not to check the data received as we have no guarantee of how much data we received. Therefore, some byte received
size check should be implemented before writing in the code.


<p>
// Create a new file upload handler
ServletFileUpload upload = new ServletFileUpload();
upload.setHeaderEncoding("UTF-8");

// Parse the request
FileItemIterator iter = upload.getItemIterator(request);
while (iter.hasNext()) 
{
    FileItemStream item = iter.next();
    String name = item.getFieldName();

    //InputStream attachmentStream = item.openStream();
    //byte[] attachmentBytes = ByteStreams.toByteArray(attachmentStream);


    //InputStream stream = item.getInputStream();
    InputStream stream = item.openStream();

    if (item.isFormField()) 
    {
        //System.out.println("Form field " + name + " with value " + Streams.asString(stream) + " detected.");
    }
    else
    {
        System.out.println("File field " + name + " with file name "+ item.getName() + " detected.");

        // Process the input stream
        FileOutputStream fout= new FileOutputStream ("c:\\" + item.getName());
        BufferedOutputStream bout= new BufferedOutputStream (fout);
        BufferedInputStream bin= new BufferedInputStream(stream);
        byte buf[] = new byte[2048];
        int len=0;
        while ((len = bin.read(buf)) > 0)//((bin.read(buf)) != -1)
        {
            bout.write(buf, 0, len);
            if (len<2048)
                len = len;
        }
        bout.close();
        bin.close();
    }        
}
</p>
