# zip4j-symlink
MWE of issue with zip4j where file with symlinks cannot be extracted on Windows without admin rights

I'm using `zipFile.extractAll` to extract a file containing a symbolic link. Under Windows, Administrator rights are required for this. As a result, the following exception occurs:
```
C:\tmp\zip4j-symlink>gradlew clean run

> Task :app:run FAILED
Exception in thread "main" net.lingala.zip4j.exception.ZipException: java.nio.file.FileSystemException: C:\Users\Maikel\AppData\Local\Temp\tmp10742489646321434610\symlink.txt: A required privilege is not held by the client.

        at net.lingala.zip4j.tasks.AsyncZipTask.performTaskWithErrorHandling(AsyncZipTask.java:53)
        at net.lingala.zip4j.tasks.AsyncZipTask.execute(AsyncZipTask.java:40)
        at net.lingala.zip4j.ZipFile.extractAll(ZipFile.java:436)
        at zip4j.symlink.App.main(App.java:17)
Caused by: java.nio.file.FileSystemException: C:\Users\Maikel\AppData\Local\Temp\tmp10742489646321434610\symlink.txt: A required privilege is not held by the client.

        at java.base/sun.nio.fs.WindowsException.translateToIOException(WindowsException.java:92)
        at java.base/sun.nio.fs.WindowsException.rethrowAsIOException(WindowsException.java:103)
        at java.base/sun.nio.fs.WindowsException.rethrowAsIOException(WindowsException.java:108)
        at java.base/sun.nio.fs.WindowsFileSystemProvider.createSymbolicLink(WindowsFileSystemProvider.java:585)
        at java.base/java.nio.file.Files.createSymbolicLink(Files.java:1058)
        at net.lingala.zip4j.tasks.AbstractExtractFileTask.createSymLink(AbstractExtractFileTask.java:108)
        at net.lingala.zip4j.tasks.AbstractExtractFileTask.extractFile(AbstractExtractFileTask.java:61)
        at net.lingala.zip4j.tasks.ExtractAllFilesTask.executeTask(ExtractAllFilesTask.java:38)
        at net.lingala.zip4j.tasks.ExtractAllFilesTask.executeTask(ExtractAllFilesTask.java:16)
        at net.lingala.zip4j.tasks.AsyncZipTask.performTaskWithErrorHandling(AsyncZipTask.java:46)
        ... 3 more
```
