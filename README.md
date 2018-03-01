# URl_SchemeA
在开发中我们会有一种需求，就是想让我们的app跳转另一个app，比如打开游戏，打开某个应用

1、添加URL Schemes
如果我们想要A应用跳转到B应用，在B应用的info->URL Types 添加一条scheme，
在AppTest0中设置： 
TARGETS->Info->URL Types 
Identifier：com.AppTest0
URL Schemes: app0 

同样在AppTest1设置 
TARGETS->Info->URL Types 
Identifier: com.test.app1 
URL Schemes: app1

2.实现跳转
A应用代码如下：
-(void)clickAction{
    NSURL *url = [NSURL URLWithString:@"app1://app0"];
    if ([[UIApplication sharedApplication] canOpenURL:url]) {
        [[UIApplication sharedApplication] openURL:url];
    }else{
        NSLog(@"您未安装B");
    }
}

注：iOS9+需添加白名单，即在info.plist添加键值LSApplicationQueriesSchemes，其value为数组类型，将你要跳转的app的scheme添加进去，即可完成跳转

