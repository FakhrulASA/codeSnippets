## Navigation Controller
```kotlin
@Composable
fun Navigation(navController: NavHostController) {
    NavHost(navController, startDestination = NavigationItem.Home.route) {
        composable(NavigationItem.Home.route) {
            HomeScreenView()
        }
        composable(NavigationItem.Group.route) {

            GroupScreenView()
        }
        composable(NavigationItem.Document.route) {
            DocumentScreen()
        }
        composable(NavigationItem.Setting.route) {
            SettingScreenView()
        }

    }
}
```

## Navigation Item
```kotlin
sealed class NavigationItem(var route:String,var icon:Int, var title:String){
    object Home: NavigationItem("home", R.drawable.ic_baseline_dashboard_24,"Board")
    object Group: NavigationItem("group", R.drawable.ic_baseline_event_note_24,"Task")
    object Document: NavigationItem("Document", R.drawable.ic_baseline_attach_file_24,"Document")
    object Setting: NavigationItem("setting", R.drawable.ic_baseline_settings_applications_24,"Setting")
}
```
