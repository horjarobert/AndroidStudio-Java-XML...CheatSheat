# AndroidStudio-Java-XML...CheatSheat
Android Studio - Cheat sheet for Java &amp; XML
# <em>~ ~ ~ IN PROGRESS... ~ ~ ~</em> #
# Table of Contents

### +[Animation](#animation-1)  
### +Animator
### +[Drawable](#drawable-1)
### +Gradle
### +[Java](#java-1)
### +[Kotlin](#kotlin-1)
### +Layout

***
# <a href="animation"></a><em>Animation</em>   
1) Bottom to up - bottomToUp.xml (inside res/anim folder)  
````
<?xml version="1.0" encoding="utf-8"?>
<set xmlns:android="http://schemas.android.com/apk/res/android">
    <translate
        android:fromYDelta="500%"
        android:toYDelta="0%"
        android:duration="1000"

        />
</set>
```` 
***
2) Up to bottom - upToBottom.xml (inside res/anim folder)
````
<?xml version="1.0" encoding="utf-8"?>
<set xmlns:android="http://schemas.android.com/apk/res/android">
    <translate
        android:fromYDelta="-500%"
        android:toYDelta="0%"
        android:duration="1000"

        />
</set>
````
***
3) Left to right - leftToRight.xml (inside res/anim folder)
````
<?xml version="1.0" encoding="utf-8"?>
<set xmlns:android="http://schemas.android.com/apk/res/android">
    <translate
        android:fromXDelta="-100%"
        android:toXDelta="0%"
        android:duration="1000"

        />
</set>
````
***
4) Right to left - rightToLeft.xml (inside res/anim folder)
````
<?xml version="1.0" encoding="utf-8"?>
<set xmlns:android="http://schemas.android.com/apk/res/android">
    <translate
        android:fromXDelta="100%"
        android:toXDelta="0%"
        android:duration="1000"

        />
</set>
````
***
5) Bouncing - bounce.xml (inside res/anim folder) - from bottom to up
````
<?xml version="1.0" encoding="utf-8"?>
<set xmlns:android="http://schemas.android.com/apk/res/android"

android:interpolator="@android:anim/bounce_interpolator">

<translate
    android:duration="3000"
    android:fromYDelta="100%p"
    android:toYDelta="0%p" />
</set>
````
***
6) Fancy animation - rotate and go from left to right
````
<set xmlns:android="http://schemas.android.com/apk/res/android">
<translate
    android:fromXDelta="-500%"
    android:toXDelta="0%"
    android:duration="1000"
    />
    <rotate
        android:fromDegrees="0"
        android:toDegrees="360"
        android:pivotX="5%"
        android:pivotY="5%"
        android:duration="1000"
    />
</set>
````
***
# <a href="drawable"></a><em>Drawable</em>
1) Layout (for a button or any other component) with a transparent color and a dashed (continue) line on the bottom, regardless of the height (ripple effect)
````
<ripple xmlns:android="http://schemas.android.com/apk/res/android"
    android:color="@color/colorPrimaryDark">

    <item android:top="-20dp" android:right="-20dp" android:left="-20dp">
        <shape>
            <solid android:color="@android:color/transparent" />
            <stroke
                android:dashGap="0px"
                android:dashWidth="5px"
                android:width="5dp"
                android:color="#fff" />
        </shape>
    </item>

</ripple>
````
***
2) Round layout with ripple effect
````
<ripple xmlns:android="http://schemas.android.com/apk/res/android"
    android:color="@color/white">


    <item>
        <shape android:shape="rectangle">


            <solid android:color="@color/colorPrimaryDark">
            </solid>

            <stroke android:width="4dp"
                android:color="@color/colorAccent"
                />


            <size android:height="200dp"
                android:width="200dp">

            </size>

            <corners android:radius="100dp"/>

        </shape>
    </item>

</ripple>
````

***
# <a href="java"></a><em>Java</em>
1) Alert user when EditText limit exceeded
````
public class MainActivity extends AppCompatActivity //...

//On the top (roof)
private EditText editTextItem;
int n = 10;
...

//Inside onCreate...
editTextItem = findViewById(R.id.ediTextItem);

//...

//Lower...

editTextItem.addTextChangedListener(new TextWatcher() {
    @Override
        public void beforeTextChanged(CharSequence charSequence, int i, int i1, int i2) {
        }

    @Override
        public void onTextChanged(CharSequence charSequence, int i, int i1, int i2) {
            if (charSequence.length() == n)
            {
                new AlertDialog.Builder(MainActivity.this).setTitle("Limit ending").setMessage("You can't type more than " + n + " characters. Thank you!").setPositiveButton(android.R.string.ok, null).setCancelable(false).show();
            }
    }
    
    @Override
        public void afterTextChanged(Editable editable) {

        }

});
````
***
2) Enable fullscreen mode
````
//inside onCreate method

    //navbar-fullscreen
    hideNavigationBar();

//outside onCreate method
//hide the navigation bar and make full screen all app
    private void hideNavigationBar() {
        this.getWindow().getDecorView()
                .setSystemUiVisibility(
                        View.SYSTEM_UI_FLAG_FULLSCREEN |
                                View.SYSTEM_UI_FLAG_HIDE_NAVIGATION |
                                View.SYSTEM_UI_FLAG_IMMERSIVE_STICKY |
                                View.SYSTEM_UI_FLAG_LAYOUT_FULLSCREEN |
                                View.SYSTEM_UI_FLAG_LAYOUT_HIDE_NAVIGATION |
                                View.SYSTEM_UI_FLAG_LAYOUT_STABLE
                );
    }

    //when I exit for a moment from the app and I'll come back, the same effect must be continue
    @Override
    protected void onResume() {
        super.onResume();

        hideNavigationBar();
    }
````
***
3) Copy a TextView to the clipboard:
````
btn_copy.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                ClipboardManager clipboard = (ClipboardManager) getSystemService(Context.CLIPBOARD_SERVICE);
                clipboard.setText(text.getText());

                Toast.makeText(getApplicationContext(), "Copied...", Toast.LENGTH_LONG).show();
            }
});
````
4) Share a TextView to others:
````
btn_share.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                String s = text.getText().toString();
                Intent sharingIntent = new Intent(android.content.Intent.ACTION_SEND);
                sharingIntent.setType("text/plain");
                sharingIntent.putExtra(android.content.Intent.EXTRA_TEXT, s);
                startActivity(Intent.createChooser(sharingIntent, "Make a joy"));

                Toast.makeText(getApplicationContext(), "Share with...", Toast.LENGTH_LONG).show();

            }
});
````
5) Constraint layout - smooth effect:
```
//1) create a new layout - a clone of your main layout or of that layout on which you want to make the SMOOTH EFFECT
//2) after you have 2 layouts, make some arrangements in the clone one, for example, that button from bottom, put in on top (or wahtever...)
//3) use this in java class:

//**on top, declarations - initializations**:::
    //for main_programmer
    private boolean isProgrammer;
    private ConstraintSet constraintSet_main_programmer_OLD = new ConstraintSet();
    private ConstraintSet constraintSet_main_programmer_NEW = new ConstraintSet();
    
//*in onCreate function*::
        //clones
        constraintSet_main_programmer_OLD.clone(mainLayout);
        constraintSet_main_programmer_NEW.clone(this, R.layout.main_programmer);

//change layout to main_programmer
    @RequiresApi(api = Build.VERSION_CODES.KITKAT)
    public void ChangeIsProgrammer(View v){
        //navbar-fullscreen
        hideNavigationBar();

        TransitionManager.beginDelayedTransition(mainLayout);

        if(!isProgrammer){
            constraintSet_main_programmer_NEW.applyTo(mainLayout);
            isProgrammer = true;
            programmerBtn.setText(R.string.programmerBtnNew);
            programmerBtn.setBackgroundResource(R.drawable.main_ui_btns_background_without_corners);
        }
        else{
            constraintSet_main_programmer_OLD.applyTo(mainLayout);
            isProgrammer = false;
            programmerBtn.setText(R.string.programmerBtn);
            programmerBtn.setBackgroundResource(R.drawable.main_ui_btns_background);
        }
    }
```
***
# <a href="kotlin"></a><em>Kotlin</em>   
1) Enable fullscreen mode
````
override fun onWindowFocusChanged(hasFocus: Boolean) {
        super.onWindowFocusChanged(hasFocus)
        if (hasFocus) hideSystemUI()
}

private fun hideSystemUI() {
        window.decorView.systemUiVisibility = (
                        View.SYSTEM_UI_FLAG_FULLSCREEN or
                        View.SYSTEM_UI_FLAG_HIDE_NAVIGATION or
                        View.SYSTEM_UI_FLAG_IMMERSIVE_STICKY or
                        View.SYSTEM_UI_FLAG_LAYOUT_FULLSCREEN or
                        View.SYSTEM_UI_FLAG_LAYOUT_HIDE_NAVIGATION or
                        View.SYSTEM_UI_FLAG_LAYOUT_STABLE
        )
}

 private fun showSystemUI() {
        window.decorView.systemUiVisibility = (View.SYSTEM_UI_FLAG_LAYOUT_STABLE
                or View.SYSTEM_UI_FLAG_LAYOUT_HIDE_NAVIGATION
                or View.SYSTEM_UI_FLAG_LAYOUT_FULLSCREEN)
}
````
***
2) Transition button/text (button clicked, text come to life from GONE - reverse; all in lay1)
````
btn.setOnClickListener(View.OnClickListener {
            TransitionManager.beginDelayedTransition(lay1)

            txt.visibility = if (txt.visibility == View.VISIBLE){
                View.GONE
            } else{
                View.VISIBLE
            }
})
````
***
3) Animation code... 
````
//At the beginning...
private lateinit var btnFix: Button
private lateinit var anim_fix: Animation

//...

//Set animation (you have already created anim_fix inside anim folder...)
    anim_fix = AnimationUtils.loadAnimation(this, R.anim.anim_fix)
    btnFix.startAnimation(anim_fix)
````
***
 
    
