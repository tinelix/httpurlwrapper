Using HttpUrlConnection with Android 2.1+ devices
=================================================
Copyright (C) 2012 Pixmob (http://github.com/pixmob)

Android provides two methods for making Http(s) requests:
[HttpURLConnection](http://developer.android.com/reference/java/net/HttpURLConnection.html) and [Apache HttpClient](http://developer.android.com/reference/org/apache/http/impl/client/DefaultHttpClient.html).

The Android development team [recommends](http://android-developers.blogspot.com/2011/09/androids-http-clients.html) the use of HttpURLConnection for newer applications, as this interface is getting better over Android releases.

However, using HttpURLConnection on earlier Android devices (before ICS) is troublesome because of the underlying implementation bugs:

 1. [connection pool poisoning](http://stackoverflow.com/a/4261005/422906)
 2. [missing SSL certificates on some Android devices](http://stackoverflow.com/a/3998257/422906)
 3. [slow POST requests](http://code.google.com/p/android/issues/detail?id=13117)
 4. [headers in lower-case](http://code.google.com/p/android/issues/detail?id=6684)
 5. [incomplete read](http://docs.oracle.com/javase/6/docs/technotes/guides/net/http-keepalive.html)
 6. [transparent Gzip compression](http://code.google.com/p/android/issues/detail?id=16227)

The framework HttpClientLibrary (HCL) provides a clean interface to HttpURLConnection, with
workarounds for known bugs, from Android 2.1 to Android 4.0.

Using HCL will make your code easier to understand, while leveraging the Android native network layer.

Usage
-----

Making Http requests with HCL is easy.

    HttpClient hc = new HttpClient();
    hc.get("http://www.google.com").execute();

Downloading a file cannot be easier:

    File logoFile = new File(context.getCacheDir(), "logo.png");
    hc.get("http://www.mysite.com/logo.png").setHandler(HttpResponseHandler.toFile(logoFile)).execute();

Please read JavaDoc and [source code](http://github.com/pixmob/hcl/tree/master/src/org/pixmob/hcl) for advanced use.

A sample application is available in the Market: [HCL Demo](https://market.android.com/details?id=org.pixmob.hcl.demo)

License
-------

All of the source code in this project is licensed under the Apache 2.0 license except as noted.

How to use this library in my project?
--------------------------------------

This project is actually a [library project](http://developer.android.com/guide/developing/projects/projects-cmdline.html#ReferencingLibraryProject).