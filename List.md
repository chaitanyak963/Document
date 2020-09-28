# ListView
* Android ListView is a view which groups several items and display them in vertical scrollable list.
* The list items are automatically inserted to the list using an Adapter that pulls content from a source such as an array or database.
* It’s one of the basic and most used UI components of android.
* The most common usages include displaying data in the form of a vertical scrolling list.

### Using an Adapter
An adapter actually bridges between UI components and the data source that fill data into UI Component. Adapter holds the data and send the data to adapter view, the view can take the data from adapter view and shows the data on different views like as spinner, list view, grid view etc. The adapter pulls the items out of a data source, an array for example, and then converts each item into a view which it then inserts into the ListView.

The **ListView** and **GridView** are subclasses of **AdapterView** and they can be populated by binding them to an Adapter, which retrieves data from an external source and creates a View that represents each data entry. The common adapters are ***ArrayAdapter, BaseAdapter, CursorAdapter, SimpleCursorAdapter, SpinnerAdapter and WrapperListAdapter***.

### Handling Android ListView Clicks
The **onListItemClick()** method is used to process the clicks on android ListView item. This method receives 4 parameters:

1. **ListView** : The ListView containing the item views
2. **View** : The specific item view that was selected
3. **Position** : The position of the selected item in the array. Remember that the array is zero indexed, so the first item in the array is at position 0
4. **Id** : The id of the selected item. Not of importance for our tutorial but is important when using data retrieved from a database as you can use the id (which is the id of the row containing the item in the database) to retrieve the item from the database.

### Android ListView Example Project Structure

![picture alt](https://github.com/chaitanyak963/Document/raw/master/project.png)

### strings.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <string-array name="teams">
        <item>India</item>
        <item>South Africa</item>
        <item>Australia</item>
        <item>England</item>
        <item>New Zealand</item>
        <item>Sri Lanka</item>
        <item>Pakistan</item>
        <item>West Indies</item>
        <item>Bangladesh</item>
        <item>Ireland</item>
    </string-array>
</resources>
```

Each list view item will be represented by an xml layout,so lets define the xml layout comprising of a single textview as follows:

### list_item.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<!--  Single List Item Design -->
<TextView xmlns:android="https://schemas.android.com/apk/res/android"
    android:id="@+id/textview"
        android:layout_width="fill_parent"
        android:layout_height="fill_parent"
        android:padding="10dip"
        android:textSize="16dip"
        android:textStyle="bold" >
</TextView>
```

### Following snippet shows how to import the xml resources data and store them in data followed by binding them to the adapter:

```
// storing string resources into Array
String[] teams = getResources().getStringArray(R.array.teams);
```
```
// Binding resources Array to ListAdapter
this.setListAdapter(new ArrayAdapter<String>(this, R.layout.list_item, R.id.textview, teams));
In the following code we fetch the data value from the selected item and pass it as a bundle to the next activity using intents.
```
### MainActivity.java

```java
package journaldev.com.listview;


import android.app.ListActivity;
import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.AdapterView;
import android.widget.ArrayAdapter;
import android.widget.ListView;
import android.widget.TextView;

public class MainActivity extends ListActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        // storing string resources into Array
        String[] teams = getResources().getStringArray(R.array.teams);

        // Binding resources Array to ListAdapter
        this.setListAdapter(new ArrayAdapter<String>(this, R.layout.list_item, R.id.textview, teams));

        ListView lv = getListView();

        // listening to single list item on click
        lv.setOnItemClickListener(new AdapterView.OnItemClickListener() {
            public void onItemClick(AdapterView<?> parent, View view,
                                    int position, long id) {

                // selected item 
                String team = ((TextView) view).getText().toString();

                // Launching new Activity on selecting single List Item
                Intent i = new Intent(getApplicationContext(), SecondActivity.class);
                // sending data to new activity
                i.putExtra("team", team);
                startActivity(i);

            }
        });
    }
}
```

The SecondActivity class retrieves the text label from the list item selected and displays it in a textview as shown in the following snippet.

### SecondActivity.java

```java
package journaldev.com.listview;

import android.app.Activity;
import android.content.Intent;
import android.os.Bundle;
import android.widget.TextView;

public class SecondActivity extends Activity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_second);
        TextView txtProduct = (TextView) findViewById(R.id.team_label);

        Intent i = getIntent();
        // getting attached intent data
        String product = i.getStringExtra("team");
        // displaying selected product name
        txtProduct.setText(product);
    }
}
```

![picture alt](https://raw.githubusercontent.com/chaitanyak963/Document/master/output.gif)
