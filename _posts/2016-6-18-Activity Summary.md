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
|--------|--------|
|
|--------|--------|
|
|--------|--------|
|
|--------|--------|
|
|--------|--------|
|
|--------|--------|
|
|--------|--------|
|
|--------|--------|
|
|--------|--------|
