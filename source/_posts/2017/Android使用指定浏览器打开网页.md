---
title: Android使用指定浏览器打开网页

date: 2017-10-30 13:30:12

urlname: Android-Browser

updated: 2017-10-30 13:32:22

tags:
- Android

categories: 
- 工作
- Android

comments: true
---

>梳理下流程：
>1. 枚举对应浏览器包名到数组中
>2. 数组循环根据包名找到对应的LaunchIntent
>3. 通过LaunchIntent找到对应的LaunchActivity的包名
>4. Intent通过设置activity的包名+类名

```
/**
* 工具类
*/
public class CheckApkExist {
    private static String ucPkgName = "com.uc.browser";

    public static boolean checkApkExist(Context context, String packageName){
        if (TextUtils.isEmpty(packageName))
            return false;
        try {
            ApplicationInfo info = context.getPackageManager()
                    .getApplicationInfo(packageName,
                            PackageManager.GET_UNINSTALLED_PACKAGES);
            return true;
        } catch (PackageManager.NameNotFoundException e) {
            return false;
        }
    }

    /** 示例：uc 浏览器检测*/
    public static boolean checkUCBrowserExist(Context context){
        return checkApkExist(context, ucPkgName);
    }
```

```
/** 
*   从手机上搜索已安装浏览器程序打开网页,默认使用系统浏览器。
*   将 context 替换为当前上下文环境，ActivityClass or  Context
*/
public void openBrowser(String url) { 
            String[] browser = {"com.tencent.mtt", "com.UCMobile", "com.uc.browser", "com.oupeng.browser", "com.oupeng.mini.android", "com.android.browser"};

            Intent intent = null;
            for (String br : browser) {
                if (CheckApkExist.checkApkExist(context, br)) {
                    String clsName = null;
                    try {
                        PackageManager pm = context.getApplicationContext().getPackageManager();
                        Intent intent1 = pm.getLaunchIntentForPackage(br);
                        ComponentName act = intent1.resolveActivity(pm);
                        clsName = act.getClassName();
                    } catch (Exception e) {
                    }
                    if (clsName == null) {
                        break;
                    }
                    intent = new Intent();
                    intent.setAction("android.intent.action.VIEW");
                    Uri content_url = Uri.parse(url);
                    intent.setData(content_url);
                    intent.setClassName(br, clsName);
                    break;
                }
            }
            if (intent == null) {
                intent = new Intent();
                intent.setAction("android.intent.action.VIEW");
                Uri content_url = Uri.parse(url);
                intent.setData(content_url);
            }
            context.startActivity(intent);
        }
```


