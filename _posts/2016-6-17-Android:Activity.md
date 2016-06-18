---
layout: post
title: Activity
category: 'technology'
---

An activity is a single, focused thing that the user can do. Almost all activities interact with the user, so the Activity class takes care of creating a window for you in which you can place your UI with setContentView(View). While activities are often presented to the user as full-screen windows, they can also be used in other ways: as floating windows (via a theme with windowIsFloating set) or embedded inside of another activity (using ActivityGroup).

```
public class Activity
extends ContextThemeWrapper implements LayoutInflater.Factory2, Window.Callback, KeyEvent.Callback, View.OnCreateContextMenuListener, ComponentCallbacks2

java.lang.Object
   ↳	android.content.Context
 	   ↳	android.content.ContextWrapper
 	 	   ↳	android.view.ContextThemeWrapper
 	 	 	   ↳	android.app.Activity
```

-   Known Direct Subclasses
    -   AccountAuthenticatorActivity, ActivityGroup, AliasActivity, ExpandableListActivity, FragmentActivity, ListActivity, NativeActivity
-   Known Indirect Subclasses
    -   ActionBarActivity, AppCompatActivity, LauncherActivity, PreferenceActivity, TabActivity


An activity is a single, focused thing that the user can do. Almost all activities interact with the user, so the Activity class takes care of creating a window for you in which you can place your UI with setContentView(View). While activities are often presented to the user as full-screen windows, they can also be used in other ways: as floating windows (via a theme with windowIsFloating set) or embedded inside of another activity (using ActivityGroup). There are two methods almost all subclasses of Activity will implement:

-   onCreate(Bundle) is where you initialize your activity. Most importantly, here you will usually call setContentView(int) with a layout resource defining your UI, and using findViewById(int) to retrieve the widgets in that UI that you need to interact with programmatically.
-   onPause() is where you deal with the user leaving your activity. Most importantly, any changes made by the user should at this point be committed (usually to the ContentProvider holding the data).

To be of use with Context.startActivity(), all activity classes must have a corresponding <activity> declaration in their package's AndroidManifest.xml.

Topics covered here:

-   Fragments
-   Activity Lifecycle
-   Configuration Changes
-   Starting Activities and Getting Results
-   Saving Persistent State
-   Permissions
-   Process Lifecycle

##  Developer Guides
The Activity class is an important part of an application's overall lifecycle, and the way activities are launched and put together is a fundamental part of the platform's application model. For a detailed perspective on the structure of an Android application and how activities behave, please read the Application Fundamentals and Tasks and Back Stack developer guides.

You can also find a detailed discussion about how to create activities in the Activities developer guide.

##  Fragments
Starting with HONEYCOMB, Activity implementations can make use of the Fragment class to better modularize their code, build more sophisticated user interfaces for larger screens, and help scale their application between small and large screens.


##  Activity Lifecycle
Activities in the system are managed as an activity stack. When a new activity is started, it is placed on the top of the stack and becomes the running activity -- the previous activity always remains below it in the stack, and will not come to the foreground again until the new activity exits.

An activity has essentially four states:

-   If an activity is in the foreground of the screen (at the top of the stack), it is active or running.
-   If an activity has lost focus but is still visible (that is, a new non-full-sized or transparent activity has focus on top of your activity), it is paused. A paused activity is completely alive (it maintains all state and member information and remains attached to the window manager), but can be killed by the system in extreme low memory situations.
-   If an activity is completely obscured by another activity, it is stopped. It still retains all state and member information, however, it is no longer visible to the user so its window is hidden and it will often be killed by the system when memory is needed elsewhere.
-   If an activity is paused or stopped, the system can drop the activity from memory by either asking it to finish, or simply killing its process. When it is displayed again to the user, it must be completely restarted and restored to its previous state.

The following diagram shows the important state paths of an Activity. The square rectangles represent callback methods you can implement to perform operations when the Activity moves between states. The colored ovals are major states the Activity can be in.

![image](/images/activity_lifecycle.png)

There are three key loops you may be interested in monitoring within your activity:

-   The entire lifetime of an activity happens between the first call to onCreate(Bundle) through to a single final call to onDestroy(). An activity will do all setup of "global" state in onCreate(), and release all remaining resources in onDestroy(). For example, if it has a thread running in the background to download data from the network, it may create that thread in onCreate() and then stop the thread in onDestroy().
-   The visible lifetime of an activity happens between a call to onStart() until a corresponding call to onStop(). During this time the user can see the activity on-screen, though it may not be in the foreground and interacting with the user. Between these two methods you can maintain resources that are needed to show the activity to the user. For example, you can register a BroadcastReceiver in onStart() to monitor for changes that impact your UI, and unregister it in onStop() when the user no longer sees what you are displaying. The onStart() and onStop() methods can be called multiple times, as the activity becomes visible and hidden to the user.
-   The foreground lifetime of an activity happens between a call to onResume() until a corresponding call to onPause(). During this time the activity is in front of all other activities and interacting with the user. An activity can frequently go between the resumed and paused states -- for example when the device goes to sleep, when an activity result is delivered, when a new intent is delivered -- so the code in these methods should be fairly lightweight.

The entire lifecycle of an activity is defined by the following Activity methods. All of these are hooks that you can override to do appropriate work when the activity changes state. All activities will implement onCreate(Bundle) to do their initial setup; many will also implement onPause() to commit changes to data and otherwise prepare to stop interacting with the user. You should always call up to your superclass when implementing these methods.

```
 public class Activity extends ApplicationContext {
     protected void onCreate(Bundle savedInstanceState);

     protected void onStart();

     protected void onRestart();

     protected void onResume();

     protected void onPause();

     protected void onStop();

     protected void onDestroy();
 }

```

In general the movement through an activity's lifecycle looks like this:


|-------+---------------+-----------+----|
|Method	|Description	|Killable?	|Next|
|-------|:--------------|-----------|----|
|onCreate()|Called when the activity is first created. This is where you should do all of your normal static set up: create views, bind data to lists, etc. This method also provides you with a Bundle containing the activity's previously frozen state, if there was one.Always followed by onStart().| No | onStart()|
|-------|:--------------|-----------|----|
|onRestart()|Called after your activity has been stopped, prior to it being started again.Always followed by onStart()|No|onStart()|
|-------|:--------------|-----------|----|
|onStart()|Called when the activity is becoming visible to the user.Followed by onResume() if the activity comes to the foreground, or onStop() if it becomes hidden.|No|onResume() onStop()|
|-------|:--------------|-----------|----|
|onResume()|Called when the activity will start interacting with the user. At this point your activity is at the top of the activity stack, with user input going to it.Always followed by onPause().|No|onPause()|
|-------|:--------------|-----------|----|
|onPause()|Called when the system is about to start resuming a previous activity. This is typically used to commit unsaved changes to persistent data, stop animations and other things that may be consuming CPU, etc. Implementations of this method must be very quick because the next activity will not be resumed until this method returns. Followed by either onResume() if the activity returns back to the front, or onStop() if it becomes invisible to the user.|No|onResume() onStop()|
|-------|:--------------|-----------|----|
|onStop()|Called when the activity is no longer visible to the user, because another activity has been resumed and is covering this one. This may happen either because a new activity is being started, an existing one is being brought in front of this one, or this one is being destroyed. Followed by either onRestart() if this activity is coming back to interact with the user, or onDestroy() if this activity is going away.|Yes|onRestart() onDestroy()|
|-------|:--------------|-----------|----|
|onDestroy()|The final call you receive before your activity is destroyed. This can happen either because the activity is finishing (someone called finish() on it, or because the system is temporarily destroying this instance of the activity to save space. You can distinguish between these two scenarios with the isFinishing() method.|Yes|nothing|
|--------+-------------+-----------+-----|

##  Configuration Changes
If the configuration of the device (as defined by the Resources.Configuration class) changes, then anything displaying a user interface will need to update to match that configuration. Because Activity is the primary mechanism for interacting with the user, it includes special support for handling configuration changes.

Unless you specify otherwise, a configuration change (such as a change in screen orientation, language, input devices, etc) will cause your current activity to be destroyed, going through the normal activity lifecycle process of onPause(), onStop(), and onDestroy() as appropriate. If the activity had been in the foreground or visible to the user, once onDestroy() is called in that instance then a new instance of the activity will be created, with whatever savedInstanceState the previous instance had generated from onSaveInstanceState(Bundle).

This is done because any application resource, including layout files, can change based on any configuration value. Thus the only safe way to handle a configuration change is to re-retrieve all resources, including layouts, drawables, and strings. Because activities must already know how to save their state and re-create themselves from that state, this is a convenient way to have an activity restart itself with a new configuration.

In some special cases, you may want to bypass restarting of your activity based on one or more types of configuration changes. This is done with the android:configChanges attribute in its manifest. For any types of configuration changes you say that you handle there, you will receive a call to your current activity's onConfigurationChanged(Configuration) method instead of being restarted. If a configuration change involves any that you do not handle, however, the activity will still be restarted and onConfigurationChanged(Configuration) will not be called.

##  Starting Activities and Getting Results
The startActivity(Intent) method is used to start a new activity, which will be placed at the top of the activity stack. It takes a single argument, an Intent, which describes the activity to be executed.

Sometimes you want to get a result back from an activity when it ends. For example, you may start an activity that lets the user pick a person in a list of contacts; when it ends, it returns the person that was selected. To do this, you call the startActivityForResult(Intent, int) version with a second integer parameter identifying the call. The result will come back through your onActivityResult(int, int, Intent) method.

When an activity exits, it can call setResult(int) to return data back to its parent. It must always supply a result code, which can be the standard results RESULT_CANCELED, RESULT_OK, or any custom values starting at RESULT_FIRST_USER. In addition, it can optionally return back an Intent containing any additional data it wants. All of this information appears back on the parent's Activity.onActivityResult(), along with the integer identifier it originally supplied.

If a child activity fails for any reason (such as crashing), the parent activity will receive a result with the code RESULT_CANCELED.

```
public class MyActivity extends Activity {
     ...

     static final int PICK_CONTACT_REQUEST = 0;

     public boolean onKeyDown(int keyCode, KeyEvent event) {
         if (keyCode == KeyEvent.KEYCODE_DPAD_CENTER) {
             // When the user center presses, let them pick a contact.
             startActivityForResult(
                 new Intent(Intent.ACTION_PICK,
                 new Uri("content://contacts")),
                 PICK_CONTACT_REQUEST);
            return true;
         }
         return false;
     }

     protected void onActivityResult(int requestCode, int resultCode,
             Intent data) {
         if (requestCode == PICK_CONTACT_REQUEST) {
             if (resultCode == RESULT_OK) {
                 // A contact was picked.  Here we will just display it
                 // to the user.
                 startActivity(new Intent(Intent.ACTION_VIEW, data));
             }
         }
     }
 }
```

##  Saving Persistent State
There are generally two kinds of persistent state than an activity will deal with: shared document-like data (typically stored in a SQLite database using a content provider) and internal state such as user preferences.

For content provider data, we suggest that activities use a "edit in place" user model. That is, any edits a user makes are effectively made immediately without requiring an additional confirmation step. Supporting this model is generally a simple matter of following two rules:

When creating a new document, the backing database entry or file for it is created immediately. For example, if the user chooses to write a new e-mail, a new entry for that e-mail is created as soon as they start entering data, so that if they go to any other activity after that point this e-mail will now appear in the list of drafts.

When an activity's onPause() method is called, it should commit to the backing content provider or file any changes the user has made. This ensures that those changes will be seen by any other activity that is about to run. You will probably want to commit your data even more aggressively at key times during your activity's lifecycle: for example before starting a new activity, before finishing your own activity, when the user switches between input fields, etc.

This model is designed to prevent data loss when a user is navigating between activities, and allows the system to safely kill an activity (because system resources are needed somewhere else) at any time after it has been paused. Note this implies that the user pressing BACK from your activity does not mean "cancel" -- it means to leave the activity with its current contents saved away. Canceling edits in an activity must be provided through some other mechanism, such as an explicit "revert" or "undo" option.

See the content package for more information about content providers. These are a key aspect of how different activities invoke and propagate data between themselves.

The Activity class also provides an API for managing internal persistent state associated with an activity. This can be used, for example, to remember the user's preferred initial display in a calendar (day view or week view) or the user's default home page in a web browser.

Activity persistent state is managed with the method getPreferences(int), allowing you to retrieve and modify a set of name/value pairs associated with the activity. To use preferences that are shared across multiple application components (activities, receivers, services, providers), you can use the underlying Context.getSharedPreferences() method to retrieve a preferences object stored under a specific name. (Note that it is not possible to share settings data across application packages -- for that you will need a content provider.)

Here is an excerpt from a calendar activity that stores the user's preferred view mode in its persistent settings:


```
 public class CalendarActivity extends Activity {
     ...

     static final int DAY_VIEW_MODE = 0;
     static final int WEEK_VIEW_MODE = 1;

     private SharedPreferences mPrefs;
     private int mCurViewMode;

     protected void onCreate(Bundle savedInstanceState) {
         super.onCreate(savedInstanceState);

         SharedPreferences mPrefs = getSharedPreferences();
         mCurViewMode = mPrefs.getInt("view_mode", DAY_VIEW_MODE);
     }

     protected void onPause() {
         super.onPause();

         SharedPreferences.Editor ed = mPrefs.edit();
         ed.putInt("view_mode", mCurViewMode);
         ed.commit();
     }
 }
```

##  Permissions
The ability to start a particular Activity can be enforced when it is declared in its manifest's <activity> tag. By doing so, other applications will need to declare a corresponding <uses-permission> element in their own manifest to be able to start that activity.

When starting an Activity you can set Intent.FLAG_GRANT_READ_URI_PERMISSION and/or Intent.FLAG_GRANT_WRITE_URI_PERMISSION on the Intent. This will grant the Activity access to the specific URIs in the Intent. Access will remain until the Activity has finished (it will remain across the hosting process being killed and other temporary destruction). As of GINGERBREAD, if the Activity was already created and a new Intent is being delivered to onNewIntent(Intent), any newly granted URI permissions will be added to the existing ones it holds.

See the Security and Permissions document for more information on permissions and security in general.

##  Process Lifecycle
The Android system attempts to keep application process around for as long as possible, but eventually will need to remove old processes when memory runs low. As described in Activity Lifecycle, the decision about which process to remove is intimately tied to the state of the user's interaction with it. In general, there are four states a process can be in based on the activities running in it, listed here in order of importance. The system will kill less important processes (the last ones) before it resorts to killing more important processes (the first ones).

The foreground activity (the activity at the top of the screen that the user is currently interacting with) is considered the most important. Its process will only be killed as a last resort, if it uses more memory than is available on the device. Generally at this point the device has reached a memory paging state, so this is required in order to keep the user interface responsive.

A visible activity (an activity that is visible to the user but not in the foreground, such as one sitting behind a foreground dialog) is considered extremely important and will not be killed unless that is required to keep the foreground activity running.

A background activity (an activity that is not visible to the user and has been paused) is no longer critical, so the system may safely kill its process to reclaim memory for other foreground or visible processes. If its process needs to be killed, when the user navigates back to the activity (making it visible on the screen again), its onCreate(Bundle) method will be called with the savedInstanceState it had previously supplied in onSaveInstanceState(Bundle) so that it can restart itself in the same state as the user last left it.

An empty process is one hosting no activities or other application components (such as Service or BroadcastReceiver classes). These are killed very quickly by the system as memory becomes low. For this reason, any background operation you do outside of an activity must be executed in the context of an activity BroadcastReceiver or Service to ensure that the system knows it needs to keep your process around.

Sometimes an Activity may need to do a long-running operation that exists independently of the activity lifecycle itself. An example may be a camera application that allows you to upload a picture to a web site. The upload may take a long time, and the application should allow the user to leave the application while it is executing. To accomplish this, your Activity should start a Service in which the upload takes place. This allows the system to properly prioritize your process (considering it to be more important than other non-visible applications) for the duration of the upload, independent of whether the original activity is paused, stopped, or finished.
