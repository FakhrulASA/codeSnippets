### create this function and set title and icon on demand
```kotlin
private fun TabLayout.setupWithViewPager2(viewPager: ViewPager2) {
        TabLayoutMediator(
            this, viewPager
        ) { tab, position ->
            if (position == 0) {
                tab.icon = resources.getDrawable(R.drawable.ic_baseline_home_24)
                tab.text = "Home"
            } else if (position == 1) {
                tab.icon = resources.getDrawable(R.drawable.ic_baseline_work_24)
                tab.text = "Jobs"
            } else if (position == 2) {
                tab.icon = resources.getDrawable(R.drawable.ic_baseline_insert_drive_file_24)
                tab.text = "Documents"
            } else if (position == 3) {
                tab.icon = resources.getDrawable(R.drawable.ic_baseline_wifi_calling_24)
                tab.text = "Appointments"
            }

        }.attach()
    }
```

### attach with viewpager
```
  binding.tabLayout.setupWithViewPager2(binding.viewPager)
```
