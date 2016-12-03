# HybridBridge
A basic framework for Android hybrid development, bridge between JavaScript and java.

##use in android
### step.1
    webView.loadUrl("you url");
    JsBridge.getInstance().init(this, webView);
### step.2
    public class JsDeviceInfo extends JsAction {
      public static final String ACTION = "deviceinfo";
      @Override
      protected void handleAction(Activity context, String jsonStr) {
        HandleResult resultEntity =new HandleResult();
        ...
        resultEntity.setData(...);
        RxBus.getInstance().post(resultEntity);
      }
     }
    JsBridge.getInstance().addJsAction(JsDeviceInfo.ACTION, JsDeviceInfo.class);
### step.3
     JsBridge.getInstance().destroy();
##use in js
### step.1
    window.nativeCallback = function(data) {...}
### step.2    
    var Senddata={
    		action:params.action,
    		callback:"nativeCallback",
    		data:params.data,
    	}
### step.3
    window.native.sendMessage(sendDataStr);