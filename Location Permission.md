## Requesting location permissions 
```kotlin
private fun requestForegroundAndBackgroundLocationPermissions() {
   if (foregroundAndBackgroundLocationPermissionApproved())
       return
   var permissionsArray = arrayOf(Manifest.permission.ACCESS_FINE_LOCATION)
   val resultCode = when {
       runningQOrLater -> {
           permissionsArray += Manifest.permission.ACCESS_BACKGROUND_LOCATION
           REQUEST_FOREGROUND_AND_BACKGROUND_PERMISSION_RESULT_CODE
       }
       else -> REQUEST_FOREGROUND_ONLY_PERMISSIONS_REQUEST_CODE
   }
   Log.d(TAG, "Request foreground only location permission")
   ActivityCompat.requestPermissions(
       this@HuntMainActivity,
       permissionsArray,
       resultCode
   )
}
```

#Handling location permissions 
```kotlin
override fun onRequestPermissionsResult(
   requestCode: Int,
   permissions: Array<String>,
   grantResults: IntArray
) {
   Log.d(TAG, "onRequestPermissionResult")

   if (
       grantResults.isEmpty() ||
       grantResults[LOCATION_PERMISSION_INDEX] == PackageManager.PERMISSION_DENIED ||
       (requestCode == REQUEST_FOREGROUND_AND_BACKGROUND_PERMISSION_RESULT_CODE &&
               grantResults[BACKGROUND_LOCATION_PERMISSION_INDEX] ==
               PackageManager.PERMISSION_DENIED))
   {
       Snackbar.make(
           binding.activityMapsMain,
           R.string.permission_denied_explanation, 
           Snackbar.LENGTH_INDEFINITE
       )
           .setAction(R.string.settings) {
               startActivity(Intent().apply {
                   action = Settings.ACTION_APPLICATION_DETAILS_SETTINGS
                   data = Uri.fromParts("package", BuildConfig.APPLICATION_ID, null)
                   flags = Intent.FLAG_ACTIVITY_NEW_TASK
               })
           }.show()
   } else {
       checkDeviceLocationSettingsAndStartGeofence()
   }
}
```
