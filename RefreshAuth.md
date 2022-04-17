# Refresh your auth token easily with below function
```kotlin
    @Synchronized
    private fun refreshAuthentication(retryCount: Int): retrofit2.Response<Token>? {
        if (retryCount > Authentication.MAX_RETRY) {
            Timber.d("Retry count maximum")
            return null
        }

        val refreshToken = prefHelper.getToken()?.token
        if (refreshToken.isNullOrBlank()) {
            return null
        }

        val clientBuilder = OkHttpClient.Builder().apply {
            connectTimeout(HttpClient.CONNECT_TIMEOUT, TimeUnit.SECONDS)
            writeTimeout(HttpClient.READ_TIMEOUT, TimeUnit.SECONDS)
            readTimeout(HttpClient.WRITE_TIMEOUT, TimeUnit.SECONDS)

            if (BuildConfig.DEBUG) {
                addInterceptor(HttpLoggingInterceptor().apply {
                    level = HttpLoggingInterceptor.Level.BODY
                })
            }
        }

        val gBuilder = GsonBuilder()
            .setLenient()
            .disableHtmlEscaping()
            .create()
        val factory = GsonConverterFactory.create(gBuilder)

        val retrofit = Retrofit.Builder()
            .baseUrl(context.getString(R.string.base_url))
            .client(clientBuilder.build())
            .addConverterFactory(factory)
            .build()

        val authApi = retrofit.create(OAuthApi::class.java)
        return authApi.refreshToken(refreshToken).execute()
    }
 ```

