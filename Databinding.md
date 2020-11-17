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

To enable DataBinding in a layout, the root element should start with <layout> tag. Along with it, <data> and <variable> tags are used.

Below is the structure of data-binding layout.

* The layout should have <layout> as root element. Inside <layout> the usual code of layout will be placed.
* A <data> tag follows the <layout>. All the binding variables and methods should go inside <data> tag.
* Inside <data> tags, a variable will be declared using <variable> tag. The variable tag takes one attribute `name`. name attribute will be alias name.
* To bind a value, @ annotation should be used. In the below layout, user name is bound to TextView using @{user.name} .

