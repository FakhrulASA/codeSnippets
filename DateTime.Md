```kotlin
 fun getCurrentDate(): String {
        val calendar: Calendar = Calendar.getInstance()
        val sdf = SimpleDateFormat("dd/MM/yy")
        return sdf.format(calendar.time)
    }

    fun getCurrentTime(): String {
        val cal = Calendar.getInstance(TimeZone.getTimeZone("GMT+1:00"))
        val currentLocalTime = cal.time
        val date: DateFormat = SimpleDateFormat("HH:mm a")
        date.timeZone = TimeZone.getTimeZone("GMT+1:00")
        return date.format(currentLocalTime)
    }
```
