# Databing

Android DataBinding provides a way to tie the UI with business logic allowing the UI values to update automatically without manual intervention. This reduces lot of boilerplate code in your business logic that you usually write to sync the UI when new data is available. DataBinding is one of the android architecture components suggested by android.

### Android Data Binding Integration

To enable data binding, add the following code in the app module’s build.gradle.

```java
android {
    dataBinding {
        enabled = true
    }
}
```

Syncing the Gradle makes Data Binding available for our project. Let’s proceed onto it’s implementation.

Let’s say we want to display user information from a **Name Model class**. We generally display the info in a **TextView** using **setText()** method. But instead of manually calling setText for each user property, DataBinding allows us to bind the values automatically.

The below **Model** class creates an User object with name.

```java
package com.example.exdatabinding;

public class Name{
    String name;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Name(String name) {
        this.name = name;
    }
}
```

To enable DataBinding in a layout, the **root** element should start with **<layout>** tag. Along with it, **<data>** and **<variable>** tags are used.

Below is the structure of data-binding layout.

* The layout should have **<layout>** as root element. Inside <layout> the usual code of layout will be placed.
* A **<data>** tag follows the **<layout>**. All the binding variables and methods should go inside **<data>** tag.
* Inside **<data>** tags, a variable will be declared using **<variable>** tag. The variable tag takes one attribute name. name attribute will be alias name.
* To bind a value, @ annotation should be used. In the below layout, user name is bound to TextView using **@{user.name}** .

```xml
<?xml version="1.0" encoding="utf-8"?>
<layout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools">

    <data>

        <variable
           name="n"
           type="com.example.exdatabinding.Name"/>
    </data>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical"
        tools:context=".MainActivity">

        <EditText
            android:id="@+id/name"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:hint="Enter Your Name" />

        <Button
            android:id="@+id/setBtn"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Set Name" />

        <TextView
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="@={n.name}"
            android:textSize="30sp"
            android:textStyle="bold" />
    </LinearLayout>

</layout>
```

* Once data binding is integrated in layout file, goto **Build -> Clean Project** and **Build -> Rebuild Project**. This will generate necessary binding classes.
* The generated binding classes follows the naming convention considering the layout file name in which binding is enabled. For the layout **activity_main.xml**, the generated binding class will be **ActivityMainBinding** (Binding suffix will be added at the end).
* To bind the data in UI, you need to inflate the binding layout first using the generated binding classes. Below, **ActivityMainBinding** inflates the layout first and **binding.setN()** binds the User object to layout.

```java
package com.example.exdatabinding;

import androidx.appcompat.app.AppCompatActivity;
import androidx.databinding.DataBindingUtil;

import android.os.Bundle;
import android.view.View;

import com.example.exdatabinding.databinding.ActivityMainBinding;

public class MainActivity extends AppCompatActivity {
    ActivityMainBinding binding;
    Name names;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        //setContentView(R.layout.activity_main);
        binding = DataBindingUtil.setContentView(this,R.layout.activity_main);
        binding.setBtn.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                String n = binding.name.getText().toString();
                names = new Name(n);
                names.setName(n);
                binding.setN(names);
            }
        });

    }
}
```
