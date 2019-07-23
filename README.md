# AndroidStudio-Java-XML...CheatSheat
Android Studio - Cheat sheet for Java &amp; XML
# <em>~ ~ ~ IN PROGRESS... ~ ~ ~</em> #
# Table of Contents

### +[Animation](#animation-1)  
### +Drawable
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
# <a href="java"></a><em>Java</em>
1) Alert user when EditText limit exceeded
```
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
```

***
# <a href="kotlin"></a><em>Kotlin</em>   
1) Enable fullscreen mode
```
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
```
***
2) Transition button/text (button clicked, text come to life from GONE - reverse; all in lay1)
```
btn.setOnClickListener(View.OnClickListener {
            TransitionManager.beginDelayedTransition(lay1)

            txt.visibility = if (txt.visibility == View.VISIBLE){
                View.GONE
            } else{
                View.VISIBLE
            }
})
```
***
3) Animation code... 
```
//At the beginning...
private lateinit var btnFix: Button
private lateinit var anim_fix: Animation

//...

//Set animation (you have already created anim_fix inside anim folder...)
    anim_fix = AnimationUtils.loadAnimation(this, R.anim.anim_fix)
    btnFix.startAnimation(anim_fix)
