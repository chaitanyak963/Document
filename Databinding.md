# Databing

Android DataBinding provides a way to tie the UI with business logic allowing the UI values to update automatically without manual intervention. This reduces lot of boilerplate code in your business logic that you usually write to sync the UI when new data is available. DataBinding is one of the android architecture components suggested by android.

### Android Data Binding Integration

To enable data binding, add the following code in the app module’s build.gradle.

```java
android {
    ...
    dataBinding {
        enabled = true
    }
}
```

Syncing the Gradle makes Data Binding available for our project. Let’s proceed onto it’s implementation.

Android Data Binding Project Structure
We’ll use an empty Android Studio project for our implementation as shown below.

android-data-binding-project

The Layout
The earlier activity_main.xml layout we used to create looked like this:

```xml
<RelativeLayout android:layout_width="match_parent"
    android:layout_height="match_parent"

    android:paddingBottom="@dimen/activity_vertical_margin"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    tools:context="com.journaldev.databinding.MainActivity"
    xmlns:tools="https://schemas.android.com/tools"
    xmlns:android="https://schemas.android.com/apk/res/android">

    <TextView
        android:id="@+id/tvHeading"
        android:layout_width="wrap_content"
        android:layout_centerHorizontal="true"
        android:layout_height="wrap_content"
        android:text="JournalDev.com" />


    <TextView
        android:id="@+id/tvSubHeading"
        android:layout_width="wrap_content"
        android:layout_below="@+id/tvHeading"
        android:layout_centerHorizontal="true"
        android:layout_height="wrap_content"
        android:text="Android Tutorials" />
</RelativeLayout>
```
To use Data Binding we need to add a layout as the root tag.

We’ve modified the activity_main.xml layout to include the layout tags as shown below.

```xml
<layout xmlns:android="https://schemas.android.com/apk/res/android"
    xmlns:tools="https://schemas.android.com/tools">

<RelativeLayout
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingBottom="@dimen/activity_vertical_margin"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    tools:context="com.journaldev.databinding.MainActivity">

    <TextView
        android:id="@+id/tvHeading"
        android:layout_width="wrap_content"
        android:layout_centerHorizontal="true"
        android:layout_height="wrap_content"
        android:text="JournalDev.com" />


    <TextView
        android:id="@+id/tvSubHeading"
        android:layout_width="wrap_content"
        android:layout_below="@+id/tvHeading"
        android:layout_centerHorizontal="true"
        android:layout_height="wrap_content"
        android:text="Android Tutorials" />
</RelativeLayout>
</layout>
```
Note: You need to build your project once now so that the auto-generated field names from the layout are available in the MainActivity.java

Code
We’ll replace the default MainActivity.java with the following one to bring DataBinding into use.

```java
package com.journaldev.databinding;

import android.databinding.DataBindingUtil;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;

import com.journaldev.databinding.databinding.ActivityMainBinding;


public class MainActivity extends AppCompatActivity {

    ActivityMainBinding binding;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        binding = DataBindingUtil.setContentView(this, R.layout.activity_main);

        binding.tvHeading.setText("Welcome to JournalDev.com");
        binding.tvSubheading.setText("Welcome to this Android Tutorial on DataBinding");
    }
}
```

Few new things to note in the above code are:

The ActivityMainBinding class is generated from the xml layout file and it’s named this way because the xml layout file name is turned into Upper CamelCase and appended with Binding
We’re invoking the xml layout in the setContentView (this is a static method) by calling

DataBindingUtil.setContentView(this, R.layout.activity_main)
The IDs of the views of the xml layout get converted into camelCase field names too as it’s seen in the code above. As you can see it’s so easy to change the texts of the TextView widgets now
Note: If the ActivityMainBinding is not available even after building the project, try restarting Android Studio. It maybe because of the cache.

Few interesting Case Scenarios:

In the present layout we’ve defined the IDs in camelCase. What happens if you assign the same id as
android:id=”@+id/tv_Heading”?
Data Binding converts it into camelCase too and the field name remains the same.

What happens when the two IDs are like
android:id=”@+id/tvHeading” and android:id=”@+id/tv_Heading”?

Ideally DataBinding is smart enough and should convert the android:id=”@+id/tv_Heading” into tvHeading1 field name. But there is no surety. Also it can lead to confusion in tracking the field names with their respective IDs. Hence it’s recommended to stay with one type of naming convention. Ideally camelCase.

The output of the application is given below.

android data binding
