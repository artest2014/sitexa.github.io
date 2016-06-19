---
layout: post
title: Activity Summary
category: 'android'
---

##  Constants

|--------|--------|--------|
|type    |Name    | Desc   |
|--------|--------|--------|
|int     |DEFAULT_KEYS_DIALER|Use with setDefaultKeyMode(int) to launch the dialer during default key handling.|
|int	|DEFAULT_KEYS_DISABLE|Use with setDefaultKeyMode(int) to turn off default handling of keys.|
|--------|--------|--------|
|int	|DEFAULT_KEYS_SEARCH_GLOBAL|Use with setDefaultKeyMode(int) to specify that unhandled keystrokes will start a global search (typically web search, but some platforms may define alternate methods for global search)|
|--------|--------|--------|
|int	|DEFAULT_KEYS_SEARCH_LOCAL|Use with setDefaultKeyMode(int) to specify that unhandled keystrokes will start an application-defined search.|
|--------|--------|--------|
|int	|DEFAULT_KEYS_SHORTCUT|Use with setDefaultKeyMode(int) to execute a menu shortcut in default key handling.|
|--------|--------|--------|
|int	|RESULT_CANCELED|Standard activity result: operation canceled.|
|--------|--------|--------|
|int	|RESULT_FIRST_USER|Start of user-defined activity results.|
|--------|--------|--------|
|int	|RESULT_OK|Standard activity result: operation succeeded.|
|--------|--------|--------|


##  Inherited constants


|--------|--------|--------|
|type    |name    |desc    |
|--------|--------|--------|
|String	|ACCESSIBILITY_SERVICE|Use with getSystemService(Class) to retrieve a AccessibilityManager for giving the user feedback for UI events through the registered event listeners.|
|--------|--------|--------|
|String	|ACCOUNT_SERVICE|Use with getSystemService(Class) to retrieve a AccountManager for receiving intents at a time of your choosing.|
|--------|--------|--------|
|String	|ACTIVITY_SERVICE|Use with getSystemService(Class) to retrieve a ActivityManager for interacting with the global system state.|
|--------|--------|--------|
|String	|ALARM_SERVICE|Use with getSystemService(Class) to retrieve a AlarmManager for receiving intents at a time of your choosing.|
|--------|--------|--------|
|String	|APPWIDGET_SERVICE|Use with getSystemService(Class) to retrieve a AppWidgetManager for accessing AppWidgets.|
|--------|--------|--------|
|String	|APP_OPS_SERVICE|Use with getSystemService(Class) to retrieve a AppOpsManager for tracking application operations on the device.|
|--------|--------|--------|
|String	|AUDIO_SERVICE|Use with getSystemService(Class) to retrieve a AudioManager for handling management of volume, ringer modes and audio routing.|
|--------|--------|--------|
|String	|BATTERY_SERVICE|Use with getSystemService(Class) to retrieve a BatteryManager for managing battery state.|
|--------|--------|--------|
|int	|BIND_ABOVE_CLIENT|Flag for bindService(Intent, ServiceConnection, int): indicates that the client application binding to this service considers the service to be more important than the app itself.|
|--------|--------|--------|
|int	|BIND_ADJUST_WITH_ACTIVITY|Flag for bindService(Intent, ServiceConnection, int): If binding from an activity, allow the target service's process importance to be raised based on whether the activity is visible to the user, regardless whether another flag is used to reduce the amount that the client process's overall importance is used to impact it.|
|--------|--------|--------|
|int	|BIND_ALLOW_OOM_MANAGEMENT|Flag for bindService(Intent, ServiceConnection, int): allow the process hosting the bound service to go through its normal memory management.|
|--------|--------|--------|
|int	|BIND_AUTO_CREATE|Flag for bindService(Intent, ServiceConnection, int): automatically create the service as long as the binding exists.|
|--------|--------|--------|
|int	|BIND_DEBUG_UNBIND|Flag for bindService(Intent, ServiceConnection, int): include debugging help for mismatched calls to unbind.|
|--------|--------|--------|
|int	|BIND_EXTERNAL_SERVICE|Flag for bindService(Intent, ServiceConnection, int): The service being bound is an isolated, external service.|
|--------|--------|--------|
|int	|BIND_IMPORTANT|Flag for bindService(Intent, ServiceConnection, int): this service is very important to the client, so should be brought to the foreground process level when the client is.|
|--------|--------|--------|
|int	|BIND_NOT_FOREGROUND| Flag for bindService(Intent, ServiceConnection, int): don't allow this binding to raise the target service's process to the foreground scheduling priority.|
|--------|--------|--------|
|int	|BIND_WAIVE_PRIORITY|Flag for bindService(Intent, ServiceConnection, int): don't impact the scheduling or memory management priority of the target service's hosting process.|
|--------|--------|--------|
|String	|BLUETOOTH_SERVICE|Use with getSystemService(Class) to retrieve a BluetoothManager for using Bluetooth.|
|--------|--------|--------|
|String	|CAMERA_SERVICE|Use with getSystemService(Class) to retrieve a CameraManager for interacting with camera devices.|
|--------|--------|--------|
|String	|CAPTIONING_SERVICE|Use with getSystemService(Class) to retrieve a CaptioningManager for obtaining captioning properties and listening for changes in captioning preferences.|
|--------|--------|--------|
|String	|CARRIER_CONFIG_SERVICE|Use with getSystemService(Class) to retrieve a CarrierConfigManager for reading carrier configuration values.|
|--------|--------|--------|
|String	|CLIPBOARD_SERVICE|Use with getSystemService(Class) to retrieve a ClipboardManager for accessing and modifying ClipboardManager for accessing and modifying the contents of the global clipboard.|
|--------|--------|--------|
|String	|CONNECTIVITY_SERVICE|Use with getSystemService(Class) to retrieve a ConnectivityManager for handling management of network connections.|
|--------|--------|--------|
|String	|CONSUMER_IR_SERVICE|Use with getSystemService(Class) to retrieve a ConsumerIrManager for transmitting infrared signals from the device.|
|--------|--------|--------|
|int	|CONTEXT_IGNORE_SECURITY|Flag for use with createPackageContext(String, int): ignore any security restrictions on the Context being requested, allowing it to always be loaded.|
|--------|--------|--------|
|int	|CONTEXT_INCLUDE_CODE|Flag for use with createPackageContext(String, int): include the application code with the context.|
|--------|--------|--------|
|int	|CONTEXT_RESTRICTED|Flag for use with createPackageContext(String, int): a restricted context may disable specific features.|
|--------|--------|--------|
|String	|DEVICE_POLICY_SERVICE|Use with getSystemService(Class) to retrieve a DevicePolicyManager for working with global device policy management.|
|--------|--------|--------|
|String	|DISPLAY_SERVICE|Use with getSystemService(Class) to retrieve a DisplayManager for interacting with display devices.|
|--------|--------|--------|
|String	|DOWNLOAD_SERVICE|Use with getSystemService(Class) to retrieve a DownloadManager for requesting HTTP downloads.|
|--------|--------|--------|
|String	|DROPBOX_SERVICE|Use with getSystemService(Class) to retrieve a DropBoxManager instance for recording diagnostic logs.|
|--------|--------|--------|
|String	|FINGERPRINT_SERVICE|Use with getSystemService(Class) to retrieve a FingerprintManager for handling management of fingerprints.|
|--------|--------|--------|
|String	|HARDWARE_PROPERTIES_SERVICE|Use with getSystemService(Class) to retrieve a HardwarePropertiesManager for accessing the hardware properties service.|
|--------|--------|--------|
|String	|INPUT_METHOD_SERVICE|Use with getSystemService(Class) to retrieve a InputMethodManager for accessing input methods.|
|--------|--------|--------|
|String	|INPUT_SERVICE|Use with getSystemService(Class) to retrieve a InputManager for interacting with input devices.|
|--------|--------|--------|
|String	|JOB_SCHEDULER_SERVICE|Use with getSystemService(Class) to retrieve a JobScheduler instance for managing occasional background tasks.|
|--------|--------|--------|
|String	|KEYGUARD_SERVICE|Use with getSystemService(Class) to retrieve a NotificationManager for controlling keyguard.|
|--------|--------|--------|
|String	|LAUNCHER_APPS_SERVICE|Use with getSystemService(Class) to retrieve a LauncherApps for querying and monitoring launchable apps across profiles of a user.|
|--------|--------|--------|
|String	|LAYOUT_INFLATER_SERVICE|Use with getSystemService(Class) to retrieve a LayoutInflater for inflating layout resources in this context.|
|--------|--------|--------|
|String	|LOCATION_SERVICE|Use with getSystemService(Class) to retrieve a LocationManager for controlling location updates.|
|--------|--------|--------|
|String	|MEDIA_PROJECTION_SERVICE|Use with getSystemService(Class) to retrieve a MediaProjectionManager instance for managing media projection sessions.|
|--------|--------|--------|
|String	|MEDIA_ROUTER_SERVICE|Use with getSystemService(Class) to retrieve a MediaRouter for controlling and managing routing of media.|
|--------|--------|--------|
|String	|MEDIA_SESSION_SERVICE|Use with getSystemService(Class) to retrieve a MediaSessionManager for managing media Sessions.|
|--------|--------|--------|
|String	|MIDI_SERVICE|Use with getSystemService(Class) to retrieve a MidiManager for accessing the MIDI service.|
|--------|--------|--------|
|int	|MODE_APPEND|File creation mode: for use with openFileOutput(String, int), if the file already exists then write data to the end of the existing file instead of erasing it.|
|--------|--------|--------|
|int	|MODE_ENABLE_WRITE_AHEAD_LOGGING|Database open flag: when set, the database is opened with write-ahead logging enabled by default.|
|--------|--------|--------|
|int	|MODE_PRIVATE|File creation mode: the default mode, where the created file can only be accessed by the calling application (or all applications sharing the same user ID).|
|--------|--------|--------|
|String	|NETWORK_STATS_SERVICE|Use with getSystemService(Class) to retrieve a NetworkStatsManager for querying network usage stats.|
|--------|--------|--------|
|String	|NFC_SERVICE|Use with getSystemService(Class) to retrieve a NfcManager for using NFC.|
|--------|--------|--------|
|String	|NOTIFICATION_SERVICE|Use with getSystemService(Class) to retrieve a NotificationManager for informing the user of background events.|
|--------|--------|--------|
|String	|NSD_SERVICE|Use with getSystemService(Class) to retrieve a NsdManager for handling management of network service discovery|
|--------|--------|--------|
|String	|POWER_SERVICE|Use with getSystemService(Class) to retrieve a PowerManager for controlling power management, including "wake locks," which let you keep the device on while you're running long tasks.|
|--------|--------|--------|
|String	|PRINT_SERVICE|PrintManager for printing and managing printers and print tasks.|
|--------|--------|--------|
|String	|RESTRICTIONS_SERVICE|Use with getSystemService(Class) to retrieve a RestrictionsManager for retrieving application restrictions and requesting permissions for restricted operations.|
|--------|--------|--------|
|String	|SEARCH_SERVICE|Use with getSystemService(Class) to retrieve a SearchManager for handling searches.|
|--------|--------|--------|
|String	|SENSOR_SERVICE|Use with getSystemService(Class) to retrieve a SensorManager for accessing sensors.|
|--------|--------|--------|
|String	|STORAGE_SERVICE| Use with getSystemService(Class) to retrieve a StorageManager for accessing system storage functions.|
|--------|--------|--------|
|String	|TELECOM_SERVICE| Use with getSystemService(Class) to retrieve a TelecomManager to manage telecom-related features of the device.|
|--------|--------|--------|
|String	|TELEPHONY_SERVICE| Use with getSystemService(Class) to retrieve a TelephonyManager for handling management the telephony features of the device.|
|--------|--------|--------|
|String	|TELEPHONY_SUBSCRIPTION_SERVICE|Use with getSystemService(Class) to retrieve a SubscriptionManager for handling management the telephony subscriptions of the device.|
|--------|--------|--------|
|String	|TEXT_SERVICES_MANAGER_SERVICE|Use with getSystemService(Class) to retrieve a TextServicesManager for accessing text services.|
|--------|--------|--------|
|String	|TV_INPUT_SERVICE| Use with getSystemService(Class) to retrieve a TvInputManager for interacting with TV inputs on the device.|
|--------|--------|--------|
|String	|UI_MODE_SERVICE| Use with getSystemService(Class) to retrieve a UiModeManager for controlling UI modes.|
|--------|--------|--------|
|String	|USAGE_STATS_SERVICE|Use with getSystemService(Class) to retrieve a UsageStatsManager for querying device usage stats.|
|--------|--------|--------|
|String	|USB_SERVICE|Use with getSystemService(Class) to retrieve a UsbManager for access to USB devices (as a USB host) and for controlling this device's behavior as a USB device.|
|--------|--------|--------|
|String	|USER_SERVICE|Use with getSystemService(Class) to retrieve a UserManager for managing users on devices that support multiple users.|
|--------|--------|--------|
|String	|VIBRATOR_SERVICE|Use with getSystemService(Class) to retrieve a Vibrator for interacting with the vibration hardware.|
|--------|--------|--------|
|String	|WALLPAPER_SERVICE| Use with getSystemService(Class) to retrieve a com.android.server.WallpaperService for accessing wallpapers.|
|--------|--------|--------|
|String	|WIFI_P2P_SERVICE| Use with getSystemService(Class) to retrieve a WifiP2pManager for handling management of Wi-Fi peer-to-peer connections.|
|--------|--------|--------|
|String	|WIFI_SERVICE|Use with getSystemService(Class) to retrieve a WifiManager for handling management of Wi-Fi access.|
|--------|--------|--------|
|String	|WINDOW_SERVICE|Use with getSystemService(Class) to retrieve a WindowManager for accessing the system's window manager.|
|--------|--------|--------|
|int	|TRIM_MEMORY_BACKGROUND|Level for onTrimMemory(int): the process has gone on to the LRU list.|
|--------|--------|--------|
|int	|TRIM_MEMORY_COMPLETE| Level for onTrimMemory(int): the process is nearing the end of the background LRU list, and if more memory isn't found soon it will be killed.|
|--------|--------|--------|
|int	|TRIM_MEMORY_MODERATE|Level for onTrimMemory(int): the process is around the middle of the background LRU list; freeing memory can help the system keep other processes running later in the list for better overall performance.|
|--------|--------|--------|
|int	|TRIM_MEMORY_RUNNING_CRITICAL|Level for onTrimMemory(int): the process is not an expendable background process, but the device is running extremely low on memory and is about to not be able to keep any background processes running.|
|--------|--------|--------|
|int	|TRIM_MEMORY_RUNNING_LOW|Level for onTrimMemory(int): the process is not an expendable background process, but the device is running low on memory.|
|--------|--------|--------|
|int	|TRIM_MEMORY_RUNNING_MODERATE|Level for onTrimMemory(int): the process is not an expendable background process, but the device is running moderately low on memory.|
|--------|--------|--------|
|int	|TRIM_MEMORY_UI_HIDDEN|Level for onTrimMemory(int): the process had been showing a user interface, and is no longer doing so.|
|--------|--------|--------|


## Feilds

protected FOCUSED_STATE_SET

##  Public constructors

Activity()

##  Public methods


|--------|--------|
|name    |desc    |
|--------|--------|
|void	addContentView(View view, ViewGroup.LayoutParams params)|Add an additional content view to the activity.|
|void	closeContextMenu()|Programmatically closes the most recently opened context menu, if showing.|
|void	closeOptionsMenu()|Progammatically closes the options menu.|
|PendingIntent	createPendingResult(int requestCode, Intent data, int flags)|Create a new PendingIntent object which you can hand to others for them to use to send result data back to your onActivityResult(int, int, Intent) callback.|
|boolean	dispatchGenericMotionEvent(MotionEvent ev)|Called to process generic motion events.|
|boolean	dispatchKeyEvent(KeyEvent event)|Called to process key events.|
|boolean	dispatchKeyShortcutEvent(KeyEvent event)|Called to process a key shortcut event.|
|boolean	dispatchPopulateAccessibilityEvent(AccessibilityEvent event)|Called to process population of AccessibilityEvents.|
|boolean	dispatchTouchEvent(MotionEvent ev)|Called to process touch screen events.|
|boolean	dispatchTrackballEvent(MotionEvent ev)|Called to process trackball events.|
|void	dump(String prefix, FileDescriptor fd, PrintWriter writer, String[] args)|Print the Activity's state into the given stream.|
|View	findViewById(int id)|Finds a view that was identified by the id attribute from the XML that was processed in onCreate(Bundle).|
|void	finish()|Call this when your activity is done and should be closed.|
|void	finishActivity(int requestCode)| Force finish another activity that you had previously started with startActivityForResult(Intent, int).|
|void	finishActivityFromChild(Activity child, int requestCode)| This is called when a child activity of this one calls its finishActivity().|
|void	finishAffinity()| Finish this activity as well as all activities immediately below it in the current task that have the same affinity.|
|void	finishAfterTransition()| Reverses the Activity Scene entry Transition and triggers the calling Activity to reverse its exit Transition.|
|void	finishAndRemoveTask()| Call this when your activity is done and should be closed and the task should be completely removed as a part of finishing the root activity of the task.|
|void	finishFromChild(Activity child)| This is called when a child activity of this one calls its finish() method.|
|ActionBar	getActionBar()| Retrieve a reference to this activity's ActionBar.|
|final Application	getApplication()| Return the application that owns this activity.|
|ComponentName	getCallingActivity()|Return the name of the activity that invoked this activity.|
|String	getCallingPackage()|Return the name of the package that invoked this activity.|
|int	getChangingConfigurations()| If this activity is being destroyed because it can not handle a configuration parameter being changed (and thus its onConfigurationChanged(Configuration) method is not being called), then you can use this method to discover the set of changes that have occurred while in the process of being destroyed.|
|Scene	getContentScene()| Retrieve the Scene representing this window's current content.|
|TransitionManager	getContentTransitionManager()| Retrieve the TransitionManager responsible for default transitions in this window.|
|View	getCurrentFocus()|  Calls getCurrentFocus() on the Window of this Activity to return the currently focused view.|
|FragmentManager	getFragmentManager()|Return the FragmentManager for interacting with fragments associated with this activity.|
|Intent	getIntent()|Return the intent that started this activity.|
|Object	getLastNonConfigurationInstance()| Retrieve the non-configuration instance data that was previously returned by onRetainNonConfigurationInstance().|
|LayoutInflater	getLayoutInflater()|Convenience for calling getLayoutInflater().|
|LoaderManager	getLoaderManager()|Return the LoaderManager for this activity, creating it if needed.|
|String	getLocalClassName()| Returns class name for this activity with the package prefix removed.|
|final MediaController	getMediaController()| Gets the controller which should be receiving media key and volume events while this activity is in the foreground.|
|MenuInflater	getMenuInflater()| Returns a MenuInflater with this context.|
|final Activity	getParent()| Return the parent activity if this view is an embedded child.|
|Intent	getParentActivityIntent()| Obtain an Intent that will launch an explicit target activity specified by this activity's logical parent.|
|SharedPreferences	getPreferences(int mode)|Retrieve a SharedPreferences object for accessing preferences that are private to this activity.|
|Uri	getReferrer()|Return information about who launched this activity.|
|int	getRequestedOrientation()| Return the current requested orientation of the activity.|
|final SearchEvent	getSearchEvent()| During the onSearchRequested() callbacks, this function will return the SearchEvent that triggered the callback, if it exists.|
|Object	getSystemService(String name)|Return the handle to a system-level service by name.|
|int	getTaskId()|Return the identifier of the task this activity is in.|
|final CharSequence	|getTitle()|
|final int	|getTitleColor()|
|VoiceInteractor	getVoiceInteractor()|Retrieve the active VoiceInteractor that the user is going through to interact with this activity.|
|final int	getVolumeControlStream()|Gets the suggested audio stream whose volume should be changed by the hardware volume controls.|
|Window	getWindow()|Retrieve the current Window for the activity.|
|WindowManager	getWindowManager()|Retrieve the window manager for showing custom windows.|
|boolean	hasWindowFocus()| Returns true if this activity's main window currently has window focus.|
|void	invalidateOptionsMenu()|Declare that the options menu has changed, so should be recreated.|
|boolean	isChangingConfigurations()|Check to see whether this activity is in the process of being destroyed in order to be recreated with a new configuration.|
|final boolean	isChild()|Is this activity embedded inside of another activity?|
|boolean	isDestroyed()|Returns true if the final onDestroy() call has been made on the Activity, so this instance is now dead.|
|boolean	isFinishing()|Check to see whether this activity is in the process of finishing, either because you called finish() on it or someone else has requested that it finished.|
|boolean	isImmersive()|Bit indicating that this activity is "immersive" and should not be interrupted by notifications if possible.|
|boolean	isTaskRoot()|Return whether this activity is the root of a task.|
|boolean	isVoiceInteraction()|Check whether this activity is running as part of a voice interaction with the user.|
|boolean	isVoiceInteractionRoot()|Like isVoiceInteraction(), but only returns true if this is also the root of a voice interaction.|
|boolean	moveTaskToBack(boolean nonRoot)|Move the task containing this activity to the back of the activity stack.|
|boolean	navigateUpTo(Intent upIntent)|Navigate from this activity to the activity specified by upIntent, finishing this activity in the process.|
|boolean	navigateUpToFromChild(Activity child, Intent upIntent)|This is called when a child activity of this one calls its navigateUpTo(Intent) method.|
|void	onActionModeFinished(ActionMode mode)|Notifies the activity that an action mode has finished.|
|void	onActionModeStarted(ActionMode mode)|Notifies the Activity that an action mode has been started.|
|void	onActivityReenter(int resultCode, Intent data)|Called when an activity you launched with an activity transition exposes this Activity through a returning activity transition, giving you the resultCode and any additional data from it.|
|void	onAttachFragment(Fragment fragment)|Called when a Fragment is being attached to this activity, immediately after the call to its Fragment.onAttach() method and before Fragment.onCreate().|
|void	onAttachedToWindow()| Called when the main window associated with the activity has been attached to the window manager.|
|void	onBackPressed()|Called when the activity has detected the user's press of the back key.|
|void	onConfigurationChanged(Configuration newConfig)|Called by the system when the device configuration changes while your activity is running.|
|void	onContentChanged()|This hook is called whenever the content view of the screen changes (due to a call to Window.setContentView or Window.addContentView).|
|boolean	onContextItemSelected(MenuItem item)|This hook is called whenever an item in a context menu is selected.|
|void	onContextMenuClosed(Menu menu)|This hook is called whenever the context menu is being closed (either by the user canceling the menu with the back/menu button, or when an item is selected).|
|void	onCreate(Bundle savedInstanceState, PersistableBundle persistentState)|Same as onCreate(android.os.Bundle) but called for those activities created with the attribute persistableMode set to persistAcrossReboots.|
|void	onCreateContextMenu(ContextMenu menu, View v, ContextMenu.ContextMenuInfo menuInfo)|Called when a context menu for the view is about to be shown.|
|CharSequence	onCreateDescription()|Generate a new description for this activity.|
|void	onCreateNavigateUpTaskStack(TaskStackBuilder builder)|Define the synthetic task stack that will be generated during Up navigation from a different task.|
|boolean	onCreateOptionsMenu(Menu menu)|Initialize the contents of the Activity's standard options menu.|
|boolean	onCreatePanelMenu(int featureId, Menu menu)|Default implementation of onCreatePanelMenu(int, Menu) for activities.|
|View	onCreatePanelView(int featureId)|Default implementation of onCreatePanelView(int) for activities.|
|boolean	onCreateThumbnail(Bitmap outBitmap, Canvas canvas)|Generate a new thumbnail for this activity.|
|View	onCreateView(View parent, String name, Context context, AttributeSet attrs)|Standard implementation of onCreateView(View, String, Context, AttributeSet) used when inflating with the LayoutInflater returned by getSystemService(Class).|
|View	onCreateView(String name, Context context, AttributeSet attrs)|Standard implementation of onCreateView(String, Context, AttributeSet) used when inflating with the LayoutInflater returned by getSystemService(Class).|
|void	onDetachedFromWindow()|Called when the main window associated with the activity has been detached from the window manager.|
|void	onEnterAnimationComplete()|Activities cannot draw during the period that their windows are animating in.|
|boolean	onGenericMotionEvent(MotionEvent event)|Called when a generic motion event was not handled by any of the views inside of the activity.|
|boolean	onKeyDown(int keyCode, KeyEvent event)|Called when a key was pressed down and not handled by any of the views inside of the activity.|
|boolean	onKeyLongPress(int keyCode, KeyEvent event)|Default implementation of KeyEvent.Callback.onKeyLongPress(): always returns false (doesn't handle the event).|
|boolean	onKeyMultiple(int keyCode, int repeatCount, KeyEvent event)|Default implementation of KeyEvent.Callback.onKeyMultiple(): always returns false (doesn't handle the event).|
|boolean	onKeyShortcut(int keyCode, KeyEvent event)|Called when a key shortcut event is not handled by any of the views in the Activity.|
|boolean	onKeyUp(int keyCode, KeyEvent event)|Called when a key was released and not handled by any of the views inside of the activity.|
|void	onLowMemory()|This is called when the overall system is running low on memory, and actively running processes should trim their memory usage.|
|boolean	onMenuItemSelected(int featureId, MenuItem item)|Default implementation of onMenuItemSelected(int, MenuItem) for activities.|
|boolean	onMenuOpened(int featureId, Menu menu)|Called when a panel's menu is opened by the user.|
|boolean	onNavigateUp()|This method is called whenever the user chooses to navigate Up within your application's activity hierarchy from the action bar.|
|boolean	onNavigateUpFromChild(Activity child)|This is called when a child activity of this one attempts to navigate up.|
|boolean	onOptionsItemSelected(MenuItem item)|This hook is called whenever an item in your options menu is selected.|
|void	onOptionsMenuClosed(Menu menu)|This hook is called whenever the options menu is being closed (either by the user canceling the menu with the back/menu button, or when an item is selected).|
|void	onPanelClosed(int featureId, Menu menu)|Default implementation of onPanelClosed(int, Menu) for activities.|
|void	onPostCreate(Bundle savedInstanceState, PersistableBundle persistentState)|This is the same as onPostCreate(Bundle) but is called for activities created with the attribute persistableMode set to persistAcrossReboots.|
|void	onPrepareNavigateUpTaskStack(TaskStackBuilder builder)|Prepare the synthetic task stack that will be generated during Up navigation from a different task.|
|boolean	onPrepareOptionsMenu(Menu menu)|Prepare the Screen's standard options menu to be displayed.|
|boolean	onPreparePanel(int featureId, View view, Menu menu)|Default implementation of onPreparePanel(int, View, Menu) for activities.|
|void	onProvideAssistContent(AssistContent outContent)|This is called when the user is requesting an assist, to provide references to content related to the current activity.|
|void	onProvideAssistData(Bundle data)|This is called when the user is requesting an assist, to build a full ACTION_ASSIST Intent with all of the context of the current application.|
|void	onProvideKeyboardShortcuts(List<KeyboardShortcutGroup> data, Menu menu, int deviceId)|Called when Keyboard Shortcuts are requested for the current window.|
|Uri	onProvideReferrer()|Override to generate the desired referrer for the content currently being shown by the app.|
|void	onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)|Callback for the result from requesting permissions.|
|void	onRestoreInstanceState(Bundle savedInstanceState, PersistableBundle persistentState)|This is the same as onRestoreInstanceState(Bundle) but is called for activities created with the attribute persistableMode set to persistAcrossReboots.|
|Object	onRetainNonConfigurationInstance()|Called by the system, as part of destroying an activity due to a configuration change, when it is known that a new instance will immediately be created for the new configuration.|
|void	onSaveInstanceState(Bundle outState, PersistableBundle outPersistentState)|This is the same as onSaveInstanceState(Bundle) but is called for activities created with the attribute persistableMode set to persistAcrossReboots.|
|boolean	onSearchRequested(SearchEvent searchEvent)|This hook is called when the user signals the desire to start a search.|
|boolean	onSearchRequested()|Called when the user signals the desire to start a search.|
|void	onStateNotSaved()|Called when an onResume() is coming up, prior to other pre-resume callbacks such as onNewIntent(Intent) and onActivityResult(int, int, Intent).|
|boolean	onTouchEvent(MotionEvent event)|Called when a touch screen event was not handled by any of the views under it.|
|boolean	onTrackballEvent(MotionEvent event)|Called when the trackball was moved and not handled by any of the views inside of the activity.|
|void	onTrimMemory(int level)|Called when the operating system has determined that it is a good time for a process to trim unneeded memory from its process.|
|void	onUserInteraction()|Called whenever a key, touch, or trackball event is dispatched to the activity.|
|void	onVisibleBehindCanceled()|Called when a translucent activity over this activity is becoming opaque or another activity is being launched.|
|void	onWindowAttributesChanged(WindowManager.LayoutParams params)|This is called whenever the current window attributes change.|
|void	onWindowFocusChanged(boolean hasFocus)|Called when the current Window of the activity gains or loses focus.|
|ActionMode	onWindowStartingActionMode(ActionMode.Callback callback, int type)|Called when an action mode is being started for this window.|
|ActionMode	onWindowStartingActionMode(ActionMode.Callback callback)|Give the Activity a chance to control the UI for an action mode requested by the system.|
|void	openContextMenu(View view)|Programmatically opens the context menu for a particular view.|
|void	openOptionsMenu()|Programmatically opens the options menu.|
|void	overridePendingTransition(int enterAnim, int exitAnim)|Call immediately after one of the flavors of startActivity(Intent) or finish() to specify an explicit transition animation to perform next.|
|void	postponeEnterTransition()|Postpone the entering activity transition when Activity was started with makeSceneTransitionAnimation(Activity, android.util.Pair[]).|
|void	recreate()|Cause this Activity to be recreated with a new instance.|
|void	registerForContextMenu(View view)|Registers a context menu to be shown for the given view (multiple views can show the context menu).|
|boolean	releaseInstance()|Ask that the local app instance of this activity be released to free up its memory.|
|final void	removeDialog(int id)|This method was deprecated in API level 13. Use the new DialogFragment class with FragmentManager instead; this is also available on older platforms through the Android compatibility package.|
|void	reportFullyDrawn()|Report to the system that your app is now fully drawn, purely for diagnostic purposes (calling it does not impact the visible behavior of the activity).|
|final void	requestPermissions(String[] permissions, int requestCode)|Requests permissions to be granted to this application.|
|boolean	requestVisibleBehind(boolean visible)|Activities that want to remain visible behind a translucent activity above them must call this method anytime between the start of onResume() and the return from onPause().|
|final boolean	requestWindowFeature(int featureId)|Enable extended window features.|
|final void	runOnUiThread(Runnable action)|Runs the specified action on the UI thread.|
|void	setActionBar(Toolbar toolbar)|Set a Toolbar to act as the ActionBar for this Activity window.|
|void	setContentTransitionManager(TransitionManager tm)|Set the TransitionManager to use for default transitions in this window.|
|void	setContentView(View view, ViewGroup.LayoutParams params)|Set the activity content to an explicit view.|
|void	setContentView(View view)|Set the activity content to an explicit view.|
|void	setContentView(int layoutResID)|Set the activity content from a layout resource.|
|final void	setDefaultKeyMode(int mode)|Select the default key handling for this activity.|
|void	setEnterSharedElementCallback(SharedElementCallback callback)|When makeSceneTransitionAnimation(Activity, android.view.View, String) was used to start an Activity, callback will be called to handle shared elements on the launched Activity.|
|void	setExitSharedElementCallback(SharedElementCallback callback)|When makeSceneTransitionAnimation(Activity, android.view.View, String) was used to start an Activity, callback will be called to handle shared elements on the launching Activity.|
|final void	setFeatureDrawable(int featureId, Drawable drawable)|Convenience for calling setFeatureDrawable(int, Drawable).|
|final void	setFeatureDrawableAlpha(int featureId, int alpha)|Convenience for calling setFeatureDrawableAlpha(int, int).|
|final void	setFeatureDrawableResource(int featureId, int resId)|Convenience for calling setFeatureDrawableResource(int, int).|
|final void	setFeatureDrawableUri(int featureId, Uri uri)|Convenience for calling setFeatureDrawableUri(int, Uri).|
|void	setFinishOnTouchOutside(boolean finish)|Sets whether this activity is finished when touched outside its window's bounds.|
|void	setImmersive(boolean i)|Adjust the current immersive mode setting.|
|void	setIntent(Intent newIntent)|Change the intent returned by getIntent().|
|final void	setMediaController(MediaController controller)|Sets a MediaController to send media keys and volume changes to.|
|final void	setProgress(int progress)|This method was deprecated in API level 24. No longer supported starting in API 21.|
|final void	setProgressBarIndeterminate(boolean indeterminate)|This method was deprecated in API level 24. No longer supported starting in API 21.|
|final void	setProgressBarIndeterminateVisibility(boolean visible)|This method was deprecated in API level 24. No longer supported starting in API 21.|
|final void	setProgressBarVisibility(boolean visible)|This method was deprecated in API level 24. No longer supported starting in API 21.|
|void	setRequestedOrientation(int requestedOrientation)|Change the desired orientation of this activity.|
|final void	setResult(int resultCode, Intent data)|Call this to set the result that your activity will return to its caller.|
|final void	setResult(int resultCode)|Call this to set the result that your activity will return to its caller.|
|final void	setSecondaryProgress(int secondaryProgress)|This method was deprecated in API level 24. No longer supported starting in API 21.|
|void	setTaskDescription(ActivityManager.TaskDescription taskDescription)|Sets information describing the task with this activity for presentation inside the Recents System UI.|
|void	setTheme(int resid)|Set the base theme for this context.|
|void	setTitle(CharSequence title)|Change the title associated with this activity.|
|void	setTitle(int titleId)|Change the title associated with this activity.|
|void	setTitleColor(int textColor)|This method was deprecated in API level 21. Use action bar styles instead.|
|void	setVisible(boolean visible)|Control whether this activity's main window is visible.|
|final void	setVolumeControlStream(int streamType)|Suggests an audio stream whose volume should be changed by the hardware volume controls.|
|boolean	shouldShowRequestPermissionRationale(String permission)|Gets whether you should show UI with rationale for requesting a permission.|
|boolean	shouldUpRecreateTask(Intent targetIntent)|Returns true if the app should recreate the task when navigating 'up' from this activity by using targetIntent.|
|boolean	showAssist(Bundle args)|Ask to have the current assistant shown to the user.|
|final boolean	showDialog(int id, Bundle args)|This method was deprecated in API level 13. Use the new DialogFragment class with FragmentManager instead; this is also available on older platforms through the Android compatibility package.|
|final void	showDialog(int id)|This method was deprecated in API level 13. Use the new DialogFragment class with FragmentManager instead; this is also available on older platforms through the Android compatibility package.|
|void	showLockTaskEscapeMessage()|Shows the user the system defined message for telling the user how to exit lock task mode.|
|ActionMode	startActionMode(ActionMode.Callback callback, int type)|Start an action mode of the given type.|
|ActionMode	startActionMode(ActionMode.Callback callback)|Start an action mode of the default type TYPE_PRIMARY.|
|void	startActivities(Intent[] intents, Bundle options)|Launch a new activity.|
|void	startActivities(Intent[] intents)|Same as startActivities(Intent[], Bundle) with no options specified.|
|void	startActivity(Intent intent)|Same as startActivity(Intent, Bundle) with no options specified.|
|void	startActivity(Intent intent, Bundle options)|Launch a new activity.|
|void	startActivityForResult(Intent intent, int requestCode)|Same as calling startActivityForResult(Intent, int, Bundle) with no options.|
|void	startActivityForResult(Intent intent, int requestCode, Bundle options)|Launch an activity for which you would like a result when it finished.|
|void	startActivityFromChild(Activity child, Intent intent, int requestCode)|Same as calling startActivityFromChild(Activity, Intent, int, Bundle) with no options.|
|void	startActivityFromChild(Activity child, Intent intent, int requestCode, Bundle options)|This is called when a child activity of this one calls its startActivity(Intent) or startActivityForResult(Intent, int) method.|
|void	startActivityFromFragment(Fragment fragment, Intent intent, int requestCode, Bundle options)|This is called when a Fragment in this activity calls its startActivity(Intent) or startActivityForResult(Intent, int) method.|
|void	startActivityFromFragment(Fragment fragment, Intent intent, int requestCode)|Same as calling startActivityFromFragment(Fragment, Intent, int, Bundle) with no options.|
|boolean	startActivityIfNeeded(Intent intent, int requestCode, Bundle options)|A special variation to launch an activity only if a new activity instance is needed to handle the given Intent.|
|boolean	startActivityIfNeeded(Intent intent, int requestCode)|Same as calling startActivityIfNeeded(Intent, int, Bundle) with no options.|
|void	startIntentSender(IntentSender intent, Intent fillInIntent, int flagsMask, int flagsValues, int extraFlags)|Same as calling startIntentSender(IntentSender, Intent, int, int, int, Bundle) with no options.|
|void	startIntentSender(IntentSender intent, Intent fillInIntent, int flagsMask, int flagsValues, int extraFlags, Bundle options)|Like startActivity(Intent, Bundle), but taking a IntentSender to start; see startIntentSenderForResult(IntentSender, int, Intent, int, int, int, Bundle) for more information.|
|void	startIntentSenderForResult(IntentSender intent, int requestCode, Intent fillInIntent, int flagsMask, int flagsValues, int extraFlags)|Same as calling startIntentSenderForResult(IntentSender, int, Intent, int, int, int, Bundle) with no options.|
|void	startIntentSenderForResult(IntentSender intent, int requestCode, Intent fillInIntent, int flagsMask, int flagsValues, int extraFlags, Bundle options)|Like startActivityForResult(Intent, int), but allowing you to use a IntentSender to describe the activity to be started.|
|void	startIntentSenderFromChild(Activity child, IntentSender intent, int requestCode, Intent fillInIntent, int flagsMask, int flagsValues, int extraFlags, Bundle options)|Like startActivityFromChild(Activity, Intent, int), but taking a IntentSender; see startIntentSenderForResult(IntentSender, int, Intent, int, int, int) for more information.|
|void	startIntentSenderFromChild(Activity child, IntentSender intent, int requestCode, Intent fillInIntent, int flagsMask, int flagsValues, int extraFlags)|Same as calling startIntentSenderFromChild(Activity, IntentSender, int, Intent, int, int, int, Bundle) with no options.|
|void	startLockTask()|Request to put this Activity in a mode where the user is locked to the current task.|
|void	startManagingCursor(Cursor c)|This method was deprecated in API level 11. Use the new CursorLoader class with LoaderManager instead; this is also available on older platforms through the Android compatibility package.|
|boolean	startNextMatchingActivity(Intent intent, Bundle options)|Special version of starting an activity, for use when you are replacing other activity components.|
|boolean	startNextMatchingActivity(Intent intent)|Same as calling startNextMatchingActivity(Intent, Bundle) with no options.|
|void	startPostponedEnterTransition()|Begin postponed transitions after postponeEnterTransition() was called.|
|void	startSearch(String initialQuery, boolean selectInitialQuery, Bundle appSearchData, boolean globalSearch)|This hook is called to launch the search UI.|
|void	stopLockTask()|Allow the user to switch away from the current task.|
|void	stopManagingCursor(Cursor c)|This method was deprecated in API level 11. Use the new CursorLoader class with LoaderManager instead; this is also available on older platforms through the Android compatibility package.|
|void	takeKeyEvents(boolean get)|Request that key events come to this activity.|
|void	triggerSearch(String query, Bundle appSearchData)|Similar to startSearch(String, boolean, Bundle, boolean), but actually fires off the search query after invoking the search dialog.|
|void	unregisterForContextMenu(View view)|Prevents a context menu to be shown for the given view.|

##  Protected methods

|--------|--------|
|name    |desc    |
|--------|--------|
|void	onActivityResult(int requestCode, int resultCode, Intent data)|Called when an activity you launched exits, giving you the requestCode you started it with, the resultCode it returned, and any additional data from it.|
|void	onApplyThemeResource(Resources.Theme theme, int resid, boolean first)|Called by setTheme(int) and getTheme() to apply a theme resource to the current Theme object.|
|void	onChildTitleChanged(Activity childActivity, CharSequence title)|
|void	onCreate(Bundle savedInstanceState)|Called when the activity is starting.|
|Dialog	onCreateDialog(int id)|This method was deprecated in API level 8. Old no-arguments version of onCreateDialog(int, Bundle).|
|Dialog	onCreateDialog(int id, Bundle args)|This method was deprecated in API level 13. Use the new DialogFragment class with FragmentManager instead; this is also available on older platforms through the Android compatibility package.|
|void	onDestroy()|Perform any final cleanup before an activity is destroyed.|
|void	onNewIntent(Intent intent)|This is called for activities that set launchMode to "singleTop" in their package, or if a client used the FLAG_ACTIVITY_SINGLE_TOP flag when calling startActivity(Intent).|
|void	onPause()|Called as part of the activity lifecycle when an activity is going into the background, but has not (yet) been killed.|
|void	onPostCreate(Bundle savedInstanceState)|Called when activity start-up is complete (after onStart() and onRestoreInstanceState(Bundle) have been called).|
|void	onPostResume()|Called when activity resume is complete (after onResume() has been called).|
|void	onPrepareDialog(int id, Dialog dialog, Bundle args)|This method was deprecated in API level 13. Use the new DialogFragment class with FragmentManager instead; this is also available on older platforms through the Android compatibility package.|
|void	onPrepareDialog(int id, Dialog dialog)|This method was deprecated in API level 8. Old no-arguments version of onPrepareDialog(int, Dialog, Bundle).|
|void	onRestart()|Called after onStop() when the current activity is being re-displayed to the user (the user has navigated back to it).|
|void	onRestoreInstanceState(Bundle savedInstanceState)|This method is called after onStart() when the activity is being re-initialized from a previously saved state, given here in savedInstanceState.|
|void	onResume()|Called after onRestoreInstanceState(Bundle), onRestart(), or onPause(), for your activity to start interacting with the user.|
|void	onSaveInstanceState(Bundle outState)|Called to retrieve per-instance state from an activity before being killed so that the state can be restored in onCreate(Bundle) or onRestoreInstanceState(Bundle) (the Bundle populated by this method will be passed to both).|
|void	onStart()|Called after onCreate(Bundle) — or after onRestart() when the activity had been stopped, but is now again being displayed to the user.|
|void	onStop()|Called when you are no longer visible to the user.|
|void	onTitleChanged(CharSequence title, int color)|
|void	onUserLeaveHint()|Called as part of the activity lifecycle when an activity is about to go into the background as the result of user choice.|

##  Inherited methods

|--------|
|name    |
|--------|
|android.view.ContextThemeWrapper
|android.content.ContextWrapper
|android.content.Context
|java.lang.Object
|android.view.LayoutInflater.Factory2
|android.view.Window.Callback
|android.view.KeyEvent.Callback
|android.view.View.OnCreateContextMenuListener
|android.content.ComponentCallbacks2
|android.view.LayoutInflater.Factory
|android.content.ComponentCallbacks






