---
layout: post
title: ContentProvider
category: 'jekyll'
---

Content providers are one of the primary building blocks of Android applications, providing content to applications. They encapsulate data and provide it to applications through the single ContentResolver interface. A content provider is only required if you need to share data between multiple applications. For example, the contacts data is used by multiple applications and must be stored in a content provider. If you don't need to share data amongst multiple applications you can use a database directly via SQLiteDatabase.

```
public abstract class ContentProvider
extends Object implements ComponentCallbacks2

java.lang.Object
   ↳	android.content.ContentProvider
```

-   Known Direct Subclasses
    -   DocumentsProvider, FileProvider, MockContentProvider, SearchRecentSuggestionsProvider

Content providers are one of the primary building blocks of Android applications, providing content to applications. They encapsulate data and provide it to applications through the single ContentResolver interface. A content provider is only required if you need to share data between multiple applications. For example, the contacts data is used by multiple applications and must be stored in a content provider. If you don't need to share data amongst multiple applications you can use a database directly via SQLiteDatabase.

When a request is made via a ContentResolver the system inspects the authority of the given URI and passes the request to the content provider registered with the authority. The content provider can interpret the rest of the URI however it wants. The UriMatcher class is helpful for parsing URIs.

The primary methods that need to be implemented are:

-   onCreate() which is called to initialize the provider
-   query(Uri, String[], String, String[], String) which returns data to the caller
-   insert(Uri, ContentValues) which inserts new data into the content provider
-   update(Uri, ContentValues, String, String[]) which updates existing data in the content provider
-   delete(Uri, String, String[]) which deletes data from the content provider
-   getType(Uri) which returns the MIME type of data in the content provider

>Data access methods (such as insert(Uri, ContentValues) and update(Uri, ContentValues, String, String[])) may be called from many threads at once, and must be thread-safe. Other methods (such as onCreate()) are only called from the application main thread, and must avoid performing lengthy operations. See the method descriptions for their expected thread behavior.

Requests to ContentResolver are automatically forwarded to the appropriate ContentProvider instance, so subclasses don't have to worry about the details of cross-process calls.

##  Nested classes

|--------|--------|
| name   | desc   |
|--------|--------|
|interface	ContentProvider.PipeDataWriter<T>|Interface to write a stream of data to a pipe.

##  Public methods

|--------|--------|
| name   | desc   |
|--------|--------|
|ContentProviderResult[]	applyBatch(ArrayList<ContentProviderOperation> operations)|Override this to handle requests to perform a batch of operations, or the default implementation will iterate over the operations and call apply(ContentProvider, ContentProviderResult[], int) on each of them.
|void	attachInfo(Context context, ProviderInfo info)|After being instantiated, this is called to tell the content provider about itself.
|int	bulkInsert(Uri uri, ContentValues[] values)|Override this to handle requests to insert a set of new rows, or the default implementation will iterate over the values and call insert(Uri, ContentValues) on each of them.
|Bundle	call(String method, String arg, Bundle extras)|Call a provider-defined method.
|Uri	canonicalize(Uri url)|Implement this to support canonicalization of URIs that refer to your content provider.
|abstract int	delete(Uri uri, String selection, String[] selectionArgs)|Implement this to handle requests to delete one or more rows.
|void	dump(FileDescriptor fd, PrintWriter writer, String[] args)|Print the Provider's state into the given stream.
|final String	getCallingPackage()|Return the package name of the caller that initiated the request being processed on the current thread.
|final Context	getContext()|Retrieves the Context this provider is running in.
|final PathPermission[]	getPathPermissions()|Return the path-based permissions required for read and/or write access to this content provider.
|final String	getReadPermission()|Return the name of the permission required for read-only access to this content provider.
|String[]	getStreamTypes(Uri uri, String mimeTypeFilter)|Called by a client to determine the types of data streams that this content provider supports for the given URI.
|abstract String	getType(Uri uri)|Implement this to handle requests for the MIME type of the data at the given URI.
|final String	getWritePermission()|Return the name of the permission required for read/write access to this content provider.
|abstract Uri	insert(Uri uri, ContentValues values)|Implement this to handle requests to insert a new row.
|void	onConfigurationChanged(Configuration newConfig)|alled by the system when the device configuration changes while your component is running. This method is always called on the application main thread, and must not perform lengthy operations.
|abstract boolean	onCreate()|Implement this to initialize your content provider on startup.
|void	onLowMemory()|This is called when the overall system is running low on memory, and actively running processes should trim their memory usage. This method is always called on the application main thread, and must not perform lengthy operations.
|void	onTrimMemory(int level)|Called when the operating system has determined that it is a good time for a process to trim unneeded memory from its process.
|AssetFileDescriptor	openAssetFile(Uri uri, String mode, CancellationSignal signal)|This is like openFile(Uri, String), but can be implemented by providers that need to be able to return sub-sections of files, often assets inside of their .apk.
|AssetFileDescriptor	openAssetFile(Uri uri, String mode)|This is like openFile(Uri, String), but can be implemented by providers that need to be able to return sub-sections of files, often assets inside of their .apk.
|ParcelFileDescriptor	openFile(Uri uri, String mode, CancellationSignal signal)|Override this to handle requests to open a file blob.
|ParcelFileDescriptor	openFile(Uri uri, String mode)|Override this to handle requests to open a file blob.
|<T> ParcelFileDescriptor	openPipeHelper(Uri uri, String mimeType, Bundle opts, T args, PipeDataWriter<T> func)|A helper function for implementing openTypedAssetFile(Uri, String, Bundle), for creating a data pipe and background thread allowing you to stream generated data back to the client.
|AssetFileDescriptor	openTypedAssetFile(Uri uri, String mimeTypeFilter, Bundle opts)|Called by a client to open a read-only stream containing data of a particular MIME type.
|AssetFileDescriptor	openTypedAssetFile(Uri uri, String mimeTypeFilter, Bundle opts, CancellationSignal signal)|Called by a client to open a read-only stream containing data of a particular MIME type.
|Cursor	query(Uri uri, String[] projection, String selection, String[] selectionArgs, String sortOrder, CancellationSignal cancellationSignal)|Implement this to handle query requests from clients with support for cancellation.
|abstract Cursor	query(Uri uri, String[] projection, String selection, String[] selectionArgs, String sortOrder)|Implement this to handle query requests from clients.
|void	shutdown()|Implement this to shut down the ContentProvider instance.
|Uri	uncanonicalize(Uri url)|Remove canonicalization from canonical URIs previously returned by canonicalize(Uri).
|abstract int	update(Uri uri, ContentValues values, String selection, String[] selectionArgs)|Implement this to handle requests to update one or more rows.

##  Protected methods

|--------|--------|
| name   | desc   |
|--------|--------|
|boolean	isTemporary()|Returns true if this instance is a temporary content provider.
|final ParcelFileDescriptor	openFileHelper(Uri uri, String mode)|Convenience for subclasses that wish to implement openFile(Uri, String) by looking up a column named "_data" at the given URI.
|final void	setPathPermissions(PathPermission[] permissions)|Change the path-based permission required to read and/or write data in the content provider.
|final void	setReadPermission(String permission)|Change the permission required to read data from the content provider.
|final void	setWritePermission(String permission)|Change the permission required to read and write data in the content provider.

##  Inherited methods

|--------|
|name    |
|--------|
|java.lang.Object
|android.content.ComponentCallbacks2
|android.content.ComponentCallbacks

