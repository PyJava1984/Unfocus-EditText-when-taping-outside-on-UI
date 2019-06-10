# Unfocus-EditText-when-taping-outside-on-UI

In activity : 
edittext.setOnFocusChangeListener(new View.OnFocusChangeListener() { 
            @Override 
            public void onFocusChange(View v, boolean hasFocus) { 
                if (!hasFocus) { 
                    Log.d("focus", "focus loosed"); 
                    // Do whatever you want here 
                } else { 
                    Log.d("focus", "focused"); 
                } 
            } 
        }); 


@Override 
public boolean dispatchTouchEvent(MotionEvent event) {  
        if (event.getAction() == MotionEvent.ACTION_DOWN) { 
            View v = getCurrentFocus(); 
            if ( v instanceof EditText) { 
                Rect outRect = new Rect(); 
                v.getGlobalVisibleRect(outRect); 
                if (!outRect.contains((int)event.getRawX(), (int)event.getRawY())) { 
                    Log.d("focus", "touchevent"); 
                    v.clearFocus(); 
                    InputMethodManager imm = (InputMethodManager) getSystemService(Context.INPUT_METHOD_SERVICE); 
                    imm.hideSoftInputFromWindow(v.getWindowToken(), 0); 
                } 
            } 
        } 
        return super.dispatchTouchEvent(event); 
} 
 
In xml : 
<LinearLayout ... 
android:focusable="true" 
android:focusableInTouchMode="true" 
...> 
 
  <EditText..></EditText> 
   
</LinearLayout..> 
