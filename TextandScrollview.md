# What is TextView 

The TextView class is a subclass of the View class that displays text on the screen. You can control how the text appears with TextView attributes in the XML layout file. This practical shows how to work with multiple TextView elements, including one in which the user can scroll its contents vertically.

If you have more information than fits on the device's display, you can create a scrolling view so that the user can scroll vertically by swiping up or down, or horizontally by swiping right or left.

You would typically use a scrolling view for news stories, articles, or any lengthy text that doesn't completely fit on the device display. You can also use a scrolling view to enable users to enter multiple lines of text, or to combine UI elements (such as a text field and a button) within a scrolling view.

# What is ScrollView

The ScrollView class provides the layout for the scrolling view. ScrollView is a subclass of FrameLayout, and developers should place only one view as a child within it, where the child view contains the entire contents to scroll. This child view may itself be a view group (such as a layout manager like LinearLayout) with a complex hierarchy of objects. Note that complex layouts may suffer performance issues with child views such as images. A good choice for a view within a ScrollView is a LinearLayout that is arranged in a vertical orientation, presenting top-level items that the user can scroll through.

With a ScrollView, all of the views are in memory and in the view hierarchy even if they aren't displayed on screen. This makes ScrollView ideal for scrolling pages of free-form text smoothly, because the text is already in memory. However, ScrollView can use up a lot of memory, which can affect the performance of the rest of your app. To display long lists of items that users can add to, delete from, or edit, consider using a RecyclerView, which is described in a separate practical.

## App overview
The Scrolling Text app demonstrates the ScrollView UI component. ScrollView is a view group that in this example contains a TextView. It shows a lengthy page of text—in this case, a music album review—that the user can scroll vertically to read by swiping up and down. A scroll bar appears in the right margin. The app shows how you can use text formatted with minimal HTML tags for setting text to bold or italic, and with new-line characters to separate paragraphs. You can also include active web links in the text.

![picture alt](https://github.com/chaitanyak963/Document/raw/master/dg_scrolling_text_composite.png)

In the above figure, the following appear:

1. An active web link embedded in free-form text
2. The scroll bar that appears when scrolling the text

### Add several text views
In this practical, you will create an Android project for the Scrolling Text app, add TextViews to the layout for an article title and subtitle, and change the existing "Hello World" TextView element to show a lengthy article. The figure below is a diagram of the layout.

![picture alt](https://github.com/chaitanyak963/Document/raw/master/dg_layout_diagram_just_textviews.png)

### Project

#### Add the below code in the xml file
```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingBottom="@dimen/activity_vertical_margin"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    tools:context="com.example.android.scrollingtext.MainActivity">

    <TextView
        android:id="@+id/article_heading"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:background="@color/colorPrimary"
        android:textColor="@android:color/holo_orange_light"
        android:textColorHighlight="@color/colorAccent"
        android:padding="10dp"
        android:textAppearance="@android:style/TextAppearance.Large"
        android:textStyle="bold"
        android:text="@string/article_title"/>

    <TextView
        android:id="@+id/article_subheading"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_below="@id/article_heading"
        android:padding="10dp"
        android:textAppearance="@android:style/TextAppearance"
        android:text="@string/article_subtitle"/>

    <TextView
        android:id="@+id/article"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@id/article_subheading"
        android:lineSpacingExtra="5sp"
        android:text="@string/article_text"/>

</RelativeLayout>
```
#### Add the text of an article
For this practical, you will create the article as a single long string in the strings.xml resource.

* In the app > res > values folder, open strings.xml.

![picture alt](https://raw.githubusercontent.com/chaitanyak963/Document/master/as_strings-xml_capture.png)
