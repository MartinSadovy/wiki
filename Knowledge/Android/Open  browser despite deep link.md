
https://developer.android.com/training/package-visibility/use-cases#check-browser-available




```
private fun getBrowsersResolveInfo(context: Context): List<ResolveInfo> {  
  val simpleBrowserIntent = Intent(Intent.ACTION_VIEW, Uri.parse("https://www.google.com/"))  
  
  return if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.TIRAMISU) {  
    val flags = PackageManager.ResolveInfoFlags.of(0)  
    context.packageManager.queryIntentActivities(simpleBrowserIntent, flags)  
  } else {  
    @Suppress("DEPRECATION")  
    context.packageManager.queryIntentActivities(simpleBrowserIntent, 0)  
  }  
}


private fun Intent.redirectToBrowser(context: Context): Intent =  
  applyIf(action == Intent.ACTION_VIEW) {  
    val browsers = getBrowsersResolveInfo(context)  
    browsers.firstOrNull()?.let { firstBrowser ->  
      `package` = firstBrowser.activityInfo.packageName  
    }  
  }
```

```
  
<queries>  
  
  <intent>    <action android:name="android.intent.action.VIEW"/>  
  </intent>  
  <intent>    <action android:name="android.intent.action.SENDTO"/>  
  </intent>  
  <intent>    <action android:name="android.intent.action.DIAL"/>  
  </intent>  
</queries>
```