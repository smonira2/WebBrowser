# WebBrowser
Web Browser source Code
Xml code of Main activity:
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
 xmlns:app="http://schemas.android.com/apk/res-auto"
 xmlns:tools="http://schemas.android.com/tools"
 android:layout_width="match_parent"
 android:layout_height="match_parent"
 tools:context=".MainActivity">
 <EditText
 android:id="@+id/eturl"
 android:layout_width="295dp"
 android:layout_height="wrap_content"
 android:layout_alignParentStart="true"
 android:layout_alignParentTop="true"
 android:layout_marginTop="13dp"
 android:ems="10"
 android:inputType="textPersonName" />
 <Button
 android:id="@+id/btngo"
 android:layout_width="62dp"
 android:layout_height="43dp"
 android:layout_alignParentEnd="true"
 android:layout_alignParentTop="true"
 android:layout_marginEnd="12dp"
 android:layout_marginTop="10dp"
 android:text="GO"
 android:textSize="20sp"
 android:textStyle="bold" />
 <WebView
 android:id="@+id/mywebview"
 android:layout_width="match_parent"
 android:layout_height="380dp"
 android:layout_alignParentStart="true"
 android:layout_alignParentTop="true"
 android:layout_marginTop="68dp">
 </WebView>
 <Button
 android:id="@+id/btnback"
 android:layout_width="71dp"
 android:layout_height="wrap_content"
 android:layout_alignParentBottom="true"
 android:layout_alignParentStart="true"
 android:text="B"
 android:textSize="20sp"
 android:textStyle="bold" />
 <Button
 android:id="@+id/btnforward"
 android:layout_width="76dp"
 android:layout_height="wrap_content"
 android:layout_alignParentBottom="true"
 android:layout_alignParentStart="true"
 android:layout_marginStart="79dp"
 android:text="F"
 android:textSize="20sp"
 android:textStyle="bold" />
 <Button
 android:id="@+id/btnclear"
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:layout_alignParentBottom="true"
 android:layout_alignParentEnd="true"
 android:layout_marginEnd="127dp"
 android:text="C"
 android:textSize="20sp"
 android:textStyle="bold" />
 <Button
 android:id="@+id/btnreload"
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:layout_alignEnd="@+id/btngo"
 android:layout_alignParentBottom="true"
 android:text="Reload"
 android:textAllCaps="false"
 android:textSize="20sp"
 android:textStyle="bold" />
</RelativeLayout>
Java code of main activity:
import android.content.Context;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.view.inputmethod.InputMethodManager;
import android.webkit.WebView;
import android.widget.Button;
import android.widget.EditText;
public class MainActivity extends AppCompatActivity implements View.OnClickListener{
 EditText eturl;
 WebView mywebView;
 Button btngo,btnback,btnforward,btnclear,btnrelaod;
 @Override
 protected void onCreate(Bundle savedInstanceState) {
 super.onCreate(savedInstanceState);
 setContentView(R.layout.activity_main);
 mywebView = findViewById(R.id.mywebview);
 mywebView.setWebViewClient(new ourViewClient());
 mywebView.getSettings().setJavaScriptEnabled(true);
 mywebView.getSettings().getLoadWithOverviewMode();
 mywebView.getSettings().setUseWideViewPort(true);
 try{
 mywebView.loadUrl("http://www.google.com");
 }catch (Exception e){
 e.printStackTrace();
 }
 btngo = findViewById(R.id.btngo);
 btnback = findViewById(R.id.btnback);
 btnforward = findViewById(R.id.btnforward);
 btnclear = findViewById(R.id.btnclear);
 btnrelaod = findViewById(R.id.btnreload);
 eturl = findViewById(R.id.eturl);
 btngo.setOnClickListener(this);
 btnback.setOnClickListener(this);
 btnforward.setOnClickListener(this);
 btnclear.setOnClickListener(this);
 btnrelaod.setOnClickListener(this);
 }
 @Override
 public void onClick(View v) {
 switch(v.getId()){
 case R.id.btngo:
 String thewebsite=eturl.getText().toString();
 mywebView.loadUrl(thewebsite);
 InputMethodManager imm = 
(InputMethodManager)getSystemService(Context.INPUT_METHOD_SERVICE);
 imm.hideSoftInputFromWindow(eturl.getWindowToken(),0);
 break;
 case R.id.btnback:
 if (mywebView.canGoBack());
 mywebView.goBack();
 break;
 case R.id.btnforward:
 if(mywebView.canGoForward());
 mywebView.goForward();
 break;
 case R.id.btnreload:
 mywebView.reload();
 break;
 case R.id.btnclear:
 mywebView.clearHistory();
 break;
 }
 }
}
Create another java class for ourViewClient and then paste this code:
import android.webkit.WebView;
import android.webkit.WebViewClient;
public class ourViewClient extends WebViewClient{
 @Override
 public boolean shouldOverrideUrlLoading(WebView v,String url){
 v.loadUrl(url);
 return true;
 }
}
Manifest.xml Internet permission code:
<uses-permission android:name="android.permission.INTERNET"></uses-permission>
