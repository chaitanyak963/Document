## Android External Storage
* External storage such as SD card can also store application data, there’s no security enforced upon files you save to the external storage.
* In android, External Storage is useful to store the data files publically on the shared external storage using the FileOutputStream object. After storing the data files on external storage, we can read the data file from external storage media using a FileInputStream object.
* The data files saved in external storage are word-readable and can be modified by the user when they enable USB mass storage to transfer files on a computer.
**Example:** SD Card

#### Grant Access to External Storage
To read or write files on the external storage, our app must acquire the WRITE_EXTERNAL_STORAGE and READ_EXTERNAL_STORAGE system permissions. For that, we need to add the following permissions in the android manifest file like as shown below.

```xml
<manifest>
    ....
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
    ....
</manifest>
```

#### Checking External Storage Availability
Before we do any work with external storage, first we need to check whether the media is available or not by calling getExternalStorageState(). The media might be mounted to a computer, missing, read-only or in some other state. To get the media status, we need to write the code like as shown below.

```java
boolean Available= false;
boolean Readable= false;
String state = Environment.getExternalStorageState();
if(Environment.MEDIA_MOUNTED.equals(state)){
    // Both Read and write operations available
    Available= true;
} else if (Environment.MEDIA_MOUNTED_READ_ONLY.equals(state)){
    // Only Read operation available
    Available= true;
    Readable= true;
} else {
    // SD card not mounted
    Available = false;
}
```

If you observe the above code snippet, we used **getExternalStorageState()** method to know the status of media mounted to a computer, such as missing, read-only or in some other state.

In android, by using **getExternalStoragePublishDirectory()** method we can access the files from appropriate public directory by passing the type of directory we want, such as DIRECTORY_MUSIC, DIRECTORY_PICTURES, DIRECTORY_RINGTONES, etc. based on our requirements.

If we save our files to corresponding media-type public directory, the system's media scanner can properly categorize our files in the system.

Following is the example to create a directory for a new photo album in the public pictures directory.

```java
// Get the directory for the user's public pictures directory.
File file = new File(Environment.getExternalStoragePublicDirectory(
        Environment.DIRECTORY_PICTURES), albumName);
if (!file.mkdirs()) {
    Log.e(LOG_TAG, "Directory not created");
}
```

In case, if we are handling the files that are not intended for other apps to use, then we should use a private storage directory on the external storage by calling **getExternalFilesDir()**.
 
 #### Write a File to External Storage
 
By using android **FileOutputStream** object and **getExternalStoragePublicDirectory** method, we can easily create and write data to the file in external storage public folders.
 
Following is the code snippet to create and write a public file in the device Downloads folder.

```java
String FILENAME = "storage_details";
String name = "Android";

File folder = Environment.getExternalStoragePublicDirectory(Environment.DIRECTORY_DOWNLOADS);
File myFile = new File(folder, FILENAME);
FileOutputStream fstream = new FileOutputStream(myFile);
fstream.write(name.getBytes());
fstream.close();
```

If you observe above code, we are creating and writing a file in device public Downloads folder by using **getExternalStoragePublicDirectory** method. We used **write()** method to write the data in file and used **close()** method to close the stream.

#### Read a File from External Storage

By using the android **FileInputStream** object and **getExternalStoragePublicDirectory** method, we can easily read the file from external storage.

Following is the code snippet to read data from a file that is in the downloads folder.

```java
String FILENAME = "user_details";
File folder = Environment.getExternalStoragePublicDirectory(Environment.DIRECTORY_DOWNLOADS);
File myFile = new File(folder, FILENAME);
FileInputStream fstream = new FileInputStream(myFile);
StringBuffer sbuffer = new StringBuffer();
int i;
while ((i = fstream.read())!= -1){
    sbuffer.append((char)i);
}
fstream.close();
```

If you observe above code, we are reading a file from device **Downloads** folder storage by using **FileInputStream** object **getExternalStoragePublicDirectory** method with file name. We used **read()** method to read one character at a time from the file and used **close()** method to close the stream.

Now we will see how to save or write file to external memory and read the file data from external storage using android **FileInputStream** and **FileOutputStream** objects in android applications with examples.
 
