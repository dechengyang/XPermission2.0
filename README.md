# XPermission
XPermissions权限管理框架，用于快速友好的给用户提示、开发接入管理权限

Android6.0上需要运行时的权限，如果我们不处理那么在6.0上权限申请不到app就会闪退，被摧残了这么久，是时候来管理你的权限了！
那么我们需要怎么管理呢？开发者方便的接入使用，XPermissions告诉你需要这么做。。。

申请一个危险的权限我们先要告诉用户，我们需要这个权限来干嘛？其次再去申请，如果是被拒绝，需要提示用户要不要重试，如果是被永久拒绝了，神仙也没办法了，
但是我们需要做一步去引导用户把我们需要申请的权限开启

XPermissions接入只需3步

1、在项目的 BaseActivity上初始化XPermission
     
    
    XPermissions.init(this);
      

2、调用申请运行时权限


     XPermissions.requestPermissions().setRequestCode(203).setShouldShow(true).setPermissions(new String[]     
     {Manifest.permission.READ_PHONE_STATE
                        ,Manifest.permission.CAMERA}).setOnXPermissionsListener(new XPermissionsListener() {
                    @Override
                    public void onXPermissions(int requestCode, int resultCode) {
                        Logger.log("resultCode:"+resultCode);
                        if (resultCode == XPermissions.PERMISSION_SUCCESS){
                            //权限申请成功，可以继续往下走
                        }else{
                            //权限申请失败，此时应该关闭界面或者退出程序
                        }
                    }
                }).builder();
                
                
3、重写activity的onRequestPermissionsResult方法
  
     @TargetApi(23)
     @Override
     public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults) {
        super.onRequestPermissionsResult(requestCode, permissions, grantResults);
        XPermissions.handlerPermissionResult(requestCode,permissions,grantResults);


    }
    
 4、builder参数说明
    
     
      //申请权限的code
      private int requestCode;
      
      //需要申请的权限数组
      private String[] permissions;
      
      //是否需要显示说明申请权限的弹窗提示？
      private boolean shouldShow;
      
      //申请权限回调
      private XPermissionsListener xPermissionsListener;
     
    
 5、下载Download下的arr直接引用即可使用，或者引用library module
   
  注：对于弹框的提示，可以提示更友好的，demo只是一个测试
    
    <string name="calendar">查看日历</string>
    <string name="camera">使用拍照和查看相册</string>
    <string name="contacts">查看联系人</string>
    <string name="location">定位</string>
    <string name="microphone">使用麦克风</string>
    <string name="phone">读取联系人</string>
    <string name="sensors">使用传感器</string>
    <string name="sms">使用短信功能</string>
    <string name="storage">存储</string>
