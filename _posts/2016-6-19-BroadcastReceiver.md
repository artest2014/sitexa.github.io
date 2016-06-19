---
layout: post
title: BroadcastReceiver
category: 'android'
---

Base class for code that will receive intents sent by sendBroadcast().

If you don't need to send broadcasts across applications, consider using this class with LocalBroadcastManager instead of the more general facilities described below. This will give you a much more efficient implementation (no cross-process communication needed) and allow you to avoid thinking about any security issues related to other applications being able to receive or send your broadcasts.

```
public abstract class BroadcastReceiver
extends Object

java.lang.Object
   ↳	android.content.BroadcastReceiver

```

-   Known Direct Subclasses
    -   AppWidgetProvider, DeviceAdminReceiver, MediaButtonReceiver, RestrictionsReceiver, WakefulBroadcastReceiver

Base class for code that will receive intents sent by sendBroadcast().

If you don't need to send broadcasts across applications, consider using this class with LocalBroadcastManager instead of the more general facilities described below. This will give you a much more efficient implementation (no cross-process communication needed) and allow you to avoid thinking about any security issues related to other applications being able to receive or send your broadcasts.

You can either dynamically register an instance of this class with Context.registerReceiver() or statically publish an implementation through the <receiver> tag in your AndroidManifest.xml.

>Note:    If registering a receiver in your Activity.onResume() implementation, you should unregister it in Activity.onPause(). (You won't receive intents when paused, and this will cut down on unnecessary system overhead). Do not unregister in Activity.onSaveInstanceState(), because this won't be called if the user moves back in the history stack.

There are two major classes of broadcasts that can be received:

-   Normal broadcasts (sent with Context.sendBroadcast) are completely asynchronous. All receivers of the broadcast are run in an undefined order, often at the same time. This is more efficient, but means that receivers cannot use the result or abort APIs included here.
-   Ordered broadcasts (sent with Context.sendOrderedBroadcast) are delivered to one receiver at a time. As each receiver executes in turn, it can propagate a result to the next receiver, or it can completely abort the broadcast so that it won't be passed to other receivers. The order receivers run in can be controlled with the android:priority attribute of the matching intent-filter; receivers with the same priority will be run in an arbitrary order.

Even in the case of normal broadcasts, the system may in some situations revert to delivering the broadcast one receiver at a time. In particular, for receivers that may require the creation of a process, only one will be run at a time to avoid overloading the system with new processes. In this situation, however, the non-ordered semantics hold: these receivers still cannot return results or abort their broadcast.

Note that, although the Intent class is used for sending and receiving these broadcasts, the Intent broadcast mechanism here is completely separate from Intents that are used to start Activities with Context.startActivity(). There is no way for a BroadcastReceiver to see or capture Intents used with startActivity(); likewise, when you broadcast an Intent, you will never find or start an Activity. These two operations are semantically very different: starting an Activity with an Intent is a foreground operation that modifies what the user is currently interacting with; broadcasting an Intent is a background operation that the user is not normally aware of.

The BroadcastReceiver class (when launched as a component through a manifest's <receiver> tag) is an important part of an application's overall lifecycle.

Topics covered here:

-   Security
-   Receiver Lifecycle
-   Process Lifecycle

##  Security

Receivers used with the Context APIs are by their nature a cross-application facility, so you must consider how other applications may be able to abuse your use of them. Some things to consider are:

-   The Intent namespace is global. Make sure that Intent action names and other strings are written in a namespace you own, or else you may inadvertently conflict with other applications.
-   When you use registerReceiver(BroadcastReceiver, IntentFilter), any application may send broadcasts to that registered receiver. You can control who can send broadcasts to it through permissions described below.
-   When you publish a receiver in your application's manifest and specify intent-filters for it, any other application can send broadcasts to it regardless of the filters you specify. To prevent others from sending to it, make it unavailable to them with android:exported="false".
-   When you use sendBroadcast(Intent) or related methods, normally any other application can receive these broadcasts. You can control who can receive such broadcasts through permissions described below. Alternatively, starting with ICE_CREAM_SANDWICH, you can also safely restrict the broadcast to a single application with Intent.setPackage

None of these issues exist when using LocalBroadcastManager, since intents broadcast it never go outside of the current process.

Access permissions can be enforced by either the sender or receiver of a broadcast.

To enforce a permission when sending, you supply a non-null permission argument to sendBroadcast(Intent, String) or sendOrderedBroadcast(Intent, String, BroadcastReceiver, android.os.Handler, int, String, Bundle). Only receivers who have been granted this permission (by requesting it with the <uses-permission> tag in their AndroidManifest.xml) will be able to receive the broadcast.

To enforce a permission when receiving, you supply a non-null permission when registering your receiver -- either when calling registerReceiver(BroadcastReceiver, IntentFilter, String, android.os.Handler) or in the static <receiver> tag in your AndroidManifest.xml. Only broadcasters who have been granted this permission (by requesting it with the <uses-permission> tag in their AndroidManifest.xml) will be able to send an Intent to the receiver.

##  Receiver Lifecycle

A BroadcastReceiver object is only valid for the duration of the call to onReceive(Context, Intent). Once your code returns from this function, the system considers the object to be finished and no longer active.

This has important repercussions to what you can do in an onReceive(Context, Intent) implementation: anything that requires asynchronous operation is not available, because you will need to return from the function to handle the asynchronous operation, but at that point the BroadcastReceiver is no longer active and thus the system is free to kill its process before the asynchronous operation completes.

In particular, you may not show a dialog or bind to a service from within a BroadcastReceiver. For the former, you should instead use the NotificationManager API. For the latter, you can use Context.startService() to send a command to the service.

##  Process Lifecycle

A process that is currently executing a BroadcastReceiver (that is, currently running the code in its onReceive(Context, Intent) method) is considered to be a foreground process and will be kept running by the system except under cases of extreme memory pressure.

Once you return from onReceive(), the BroadcastReceiver is no longer active, and its hosting process is only as important as any other application components that are running in it. This is especially important because if that process was only hosting the BroadcastReceiver (a common case for applications that the user has never or not recently interacted with), then upon returning from onReceive() the system will consider its process to be empty and aggressively kill it so that resources are available for other more important processes.

This means that for longer-running operations you will often use a Service in conjunction with a BroadcastReceiver to keep the containing process active for the entire time of your operation.

##  Nested classes

|-----------------|
| name            |
|-----------------|
|class	BroadcastReceiver.PendingResultState for a result that is pending for a broadcast receiver.

##  Public methods

|--------|--------|
|name    |desc    |
|--------|--------|
|final void	abortBroadcast()|Sets the flag indicating that this receiver should abort the current broadcast; only works with broadcasts sent through Context.sendOrderedBroadcast.
|final void	clearAbortBroadcast()|Clears the flag indicating that this receiver should abort the current broadcast.
|final boolean	getAbortBroadcast()|Returns the flag indicating whether or not this receiver should abort the current broadcast.
|final boolean	getDebugUnregister()|Return the last value given to setDebugUnregister(boolean).
|final int	getResultCode()|Retrieve the current result code, as set by the previous receiver.
|final String	getResultData()|Retrieve the current result data, as set by the previous receiver.
|final Bundle	getResultExtras(boolean makeMap)|Retrieve the current result extra data, as set by the previous receiver.
|final BroadcastReceiver.PendingResult	goAsync()|This can be called by an application in onReceive(Context, Intent) to allow it to keep the broadcast active after returning from that function.
|final boolean	isInitialStickyBroadcast()|Returns true if the receiver is currently processing the initial value of a sticky broadcast -- that is, the value that was last broadcast and is currently held in the sticky cache, so this is not directly the result of a broadcast right now.
|final boolean	isOrderedBroadcast()|Returns true if the receiver is currently processing an ordered broadcast.
|abstract void	onReceive(Context context, Intent intent)|This method is called when the BroadcastReceiver is receiving an Intent broadcast.
|IBinder	peekService(Context myContext, Intent service)|Provide a binder to an already-running service.
|final void	setDebugUnregister(boolean debug)|Control inclusion of debugging help for mismatched calls to Context.registerReceiver().
|final void	setOrderedHint(boolean isOrdered)|For internal use, sets the hint about whether this BroadcastReceiver is running in ordered mode.
|final void	setResult(int code, String data, Bundle extras)|Change all of the result data returned from this broadcasts; only works with broadcasts sent through Context.sendOrderedBroadcast.
|final void	setResultCode(int code)|Change the current result code of this broadcast; only works with broadcasts sent through Context.sendOrderedBroadcast.
|final void	setResultData(String data)|Change the current result data of this broadcast; only works with broadcasts sent through Context.sendOrderedBroadcast.
|final void	setResultExtras(Bundle extras)|Change the current result extras of this broadcast; only works with broadcasts sent through Context.sendOrderedBroadcast.
