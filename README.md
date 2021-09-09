# Android App Development

##   Introduction     
you have to have android device or android emulator for make app)

mobile app have some pages and it's call activities. when open application have
"main" activity.    
we can transfer data one activity to another activity using "intent".   


 We are going to use "Android Studio" as IDE(integrated development environment)    

 needed tools   
  1. Android Studio.    
  2. Java JDK   

to start new project    
[open] "Android Studio" > [click] "Start a new Android Studio project"    
[select] "Empty Activity"> [input] Name > [select] language > [click] "Finish"    


to set java SDK path in "AndroidStudio" at first time.        
[click] "File" > [select] "Project Structure" > [select-tab] "SDK Location" >       
[input] "JDK Location"        

to run android virtual device           
[select] "open AVD manager" on tab near by run(play) button.    

to run android real device (for this you have to turn-on phone debug mode)         
[go] "settings" on android device >  [select] "General" or "System" >
[select] "About device" > [double-click] at several times on "Build number" >
[select] newly appeared "Development options" on settings. > [turn-on] "USB debugging" >
now you can connect your device to your computer.(windows have some drivers install
  "OEM USB divers")

##   Hello world application.   

 default empty project already have "Hello World" application. just hit the run(play) button.   
 main project file location.    
 project> app> src> main> java> your_package_name > MainActivity    

## Structure

 * to change font size on android studio.   


## about
"activity_main.xml" file for frontend design structure [app>java>com.example.mutx>MainActivity]
"MainActivity.java" for functionality [app>res>layout>activity_main.xml]

## id attribute
in "activity_main.xml" file have element id. It just not id name    
eg:android:id="@+id/hello"    
to access element in "MainActivity" file for dynamic    
 R.id.hello       

## static vs dynamic
 dynamic  element data output   
 dynamic  element data input    
 dynamic element position(for different screen size)    


## buttons(for all basic elements)
1. go to palette and grab the button element.
2. make position on screen
3. top of the "Desing+Blueprint" you can set your "default" margin for screen.


## event handling and methods
1. grab the button and position on layout.
2. in Attribute slide search the "onClik" and input your event method name there.

put following code inside MainActivity class
> MainActuvity.java
```java
    public void clickButton(View button){
        button.setEnabled(false);
    }
```
## make console.log()
```java
Log.d(tag:"sucess", msg:"button disable");
```
to see log
1. get Logcat(near to Terminal button)
2. write our tag value on search bar

## view agrument convert(casting) to it own class
this is posible because View is inside Button class or something like that.
in this way we can access fully button attributes.

```java
  public void clickButton(View v){
      v.setEnabled(false);
      Button button = (Button) v; // object casting
      button.setText("Disabled");
  }
```

## findViewById method
```java
    public void clickButton(View v){
          Button button = findViewById(R.id.button);
          TextView text = findViewById(R.id.textView);
          String tt = (String) text.getText();
          if(tt.equals("active")){
              button.setText("Disabled");
              text.setText("deactive");
          }else{
              button.setText("Click");
              text.setText("active");
          }
    }
```

## Casting    
```java
    public void clickButton(View v){
         // without assign to variable
         findViewById(R.id.button).setEnabled(false);
         // without assign to variable with casting
         ((Button) findViewById(R.id.button)).setText("Disabled");
    }
```


## get user input
1. grab the "Plain Text" from palette.  

```java
    public void clickButton(View v){
        TextView textInput = findViewById(R.id.textInput);
        // EditText textInput = findViewById(R.id.textInput); here we can use "EditText" class instance "TextView"
        String input = textInput.getText().toString();
        Log.d("info", input);
    }

```


### Alert (Toast)
here we are using

```java
    public void clickButton(View v){
        TextView textInput = findViewById(R.id.textInput);
        String input = textInput.getText().toString();
        //Toast.makeText(this,"my alert", Toast.LENGTH_LONG).show();
        Toast.makeText(this,input, Toast.LENGTH_LONG).show(); // show Toast Alert message
    }
```

toast alert popup position have issue with keyboard. we will correct it future.


## more activity

> on MainActivity

```Java
public void launchSettings(View v){
     // launch a new activity
    Intent i = new Intent(this, anotherActivity.class); // this = main method
    startActivity(i);
}
```

create a new activity
[dir]"app>java>com.example.mutx">[rclick] select "new>Activity>Empty Activity" >    
[input] name of activity name "anotherActivity"


## set global key values for string
if we have one string in different activities then we can set key for that string value.    
[dir]"app>res>values>string.xml"> [click] right-top "open editor" > [click] left-top "+" button   
add "key" and "value" for string.   

to add global string value for ui   
1. xml (myString > my_string converting by editor)    
android:text="@string/my_string"    
2. using attributes
[click] right corner little box on attribute palette and select the key there.      


## change launch activity when opening the application
[dir] "app>manifests>AndroidManifest.xml"  

change following code inside your activity that you want launch when start the application.

```xml
<intent-filter>
    <action android:name="android.intent.action.MAIN" />
    <category android:name="android.intent.category.LAUNCHER" />
</intent-filter>
```

## change application default icon
[dir] "app>manifests>AndroidManifest.xml"  

inside AndroidManifest.xml file you can see icon location definition.

you can replace icons on following location
[dir] "app>res>mipmap>"


## change title on activity
 we can change or add activity title in two ways
 1. on AndroidManifest file.     

 ```xml
<activity android:name=".anotherActivity"  android:label="Settings"></activity>
 ```
this change activity header name

 2. on Activity java file

 ```java
 @Override
 protected void onCreate(Bundle savedInstanceState) {
     super.onCreate(savedInstanceState);
     setContentView(R.layout.activity_main);
     setTitle("Home"); // here set MainActivity title.
 }
 ```

 when can change on Activity title on AndroidManifest file except ".MainActivity" because
 it will change app name also.

 default app name equals to "project name". but you can change it using AndroidManifest file in ".MainActivity" tag .


## back to parent activity.
[dir] "app>manifests>AndroidManifest.xml"
just test define parent activity name on your child activity.

```xml
<activity android:name=".anotherActivity"
          android:parentActivityName=".MainActivity"
></activity>
```

## pass data to one activity to another activity  ** Intent.

> parent activity

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }

    public void launchSettings(View v){ // click to open new activity
        Intent i = new Intent(this, anotherActivity.class); // define new activity
        i.putExtra("COOL","Hello"); // (key, value)  define data to send to new activity
        startActivity(i); // cmd to start activity
    }
}
```

> child activity

```java
public class anotherActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_another);

        Intent i = getIntent(); // add
        String message = i.getStringExtra("COOL"); // add get passing value from parent
        ( (TextView) findViewById(R.id.textView) ).setText(message); // value just set on text view
    }
}
```

## how to remove activity  

you have to delete following all reference
1. delete_activity.xml
2. delete_activity.java
3. AndroidManifest.xml

to see all the connections of the deleting activity.    
 [dir] "app>java>com.example.mutx>delete_activity.java"> [r-click] [select] "Find Usages"

 this will show error when connection broken and where.


## create tab system

the easiest way to create tab navigation that create project with tab navigation.

## change input Attribute types
1. select the element
2. get the Attribute pennal and click the inputType little arrow.
3. play with different types and it will change input type too.




## fragment
fragment is manage activity inside another activity and can reuse it.
