# Scoped Storage

Working with the file system is an important part of developing any Android app. Up until Android 10, when you gave an app storage permission, it could access any file on the device. However, most apps don’t need access to the whole storage system. They usually perform tasks on a single file or a small group of files. This created a threat to user privacy.

In Android 10, Google introduced the concept of scoped storage, which enhances user control and privacy while cutting back the file clutter that removed apps leave behind.

### Why Scoped Storage

There are three main reasons for using scoped storage:

* **Improving security:** Developers should have control over the files their apps create. Scoped storage provides this control, letting developers work with files without having to request storage permissions At the same time, scoped storage also provides better app data protection because other apps can’t access these files easily.
* **Reducing leftover app data:** When a user uninstalls an app from their device, some app data still remains in the shared storage. With scoped storage, this problem disappears as all the app data resides exclusively in the app directory.
* **Limiting the abuse of READ_EXTERNAL_STORAGE permission:** Developers have abused this permission heavily because it gave them access to the entire external storage. Using scoped storage, apps can access only their own files, folders and other media file types using storage APIs.


