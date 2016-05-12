#简介
**innovation**  英  [ˌɪnəˈveɪʃn]  美  [,ɪnə'veʃən]  
	n. 创新，革新；新方法

**fundamental**  英  [fʌndə'ment(ə)l]  美  [,fʌndə'mɛntl]
	adj. 基本的，根本的n. 基本原理；基本原则

**concept** 英  ['kɒnsept]  美  ['kɑnsɛpt] 
	n. 观念，概念

**distinct** 
     英  [dɪ'stɪŋ(k)t]  美  [dɪ'stɪŋkt]  
	adj. 明显的；独特的；清楚的；有区别的

**invoke** 
     英  [ɪn'vəʊk]  美  [ɪn'vok]  
	vt. 调用；祈求；引起；恳求

**individual** 英  [ɪndɪ'vɪdjʊ(ə)l]  美  [,ɪndɪ'vɪdʒuəl]  
	adj. 个人的；个别的；独特的 n. 个人，个体


1. Application fundamental
2. Device Compatibility
3. System Permission


##应用基本原则：

一旦应用安装到设备上，每一个 Android 应用都运行在它自己的安全的沙箱中：


- Android 操作系统是一个多任务的 Linux 系统，每一个不同的应用都是一个不同的用户


- 默认情况下，系统分配给每个应用一个唯一的用户 ID(这个 ID 是只为系统使用，应用并不知道),系统给应用的每个文件都设置权限，这样就只有分配了用户 ID 的应用可以使用它们。


- 每一个进程都有一个它们自己的虚拟机，所以每个应用都是运行在相互独立的虚拟机中 。
默认情况下，每个应用运行在它自己的 Linux 进程中。Android 系统当任何一个应用的组件需要被执行时会启动一个进程，当不需要被执行或系统需要为其他应用回收内存时会杀死这个进程




###应用组件

	应用组件是一个 Android 应用的基础构造，每个空间都是一个系统进入应用的入口，并不是所有的控件都是一个真实的入口，一些控件需要依赖其他的控件，但是每一个都存在一个入口并扮演着特殊的角色-每个控件都是唯一的 building block 帮助你定义应用的所有行为。

	共有四个应用组件，每一个都提供不同的作用并且有不同的生命周期定义它是如何创建与销毁的


####Activities:
	activity 代表了一个用户界面的单独一个界面。activity 是作为 Activity 的一个子类。

####Services
	service 是运行在后台的组件，执行 long-running 的操作或者为远程进程执行操作。一个 service 不提供用户界面。例如，一个 service 可以当用户在一个应用时在后台播放音乐(这里播放音乐是另一个应用)，或者为了不阻塞用户与 Activity 交互可以使用 service 获取网络数据。另一个组件，例如 Activity，可以开启一个 service，或者为了可以与 service 交互可以绑定它。

	service 都是 Service 的子类

####Content Provider
	content provider 是为了管理应用的共享数据的组件。

####BroadcastReceiver

	BroadcastReceiver 是一个回应全路(system-wide)广播通告的组件。大多数的广播都来自于系统，例如，通知屏幕关闭了，电池电量低了，或者一个图片被捕捉了的广播。应用本身也可以自定义广播-例如，让其他应用一些数据已经下载到设备并且它们可以使用了。尽管广播不同显示用户界面，它可以当广播事件发生时创建一个状态栏通知提醒用户。**一般情况下，一个广播接收者只是作为进入其他组件的“入口”，只完成很少的工作。**例如，它可以初始化一个 service 去根据这个事件执行操作。

	originate from：来自…， 源于…; 起源;


Android 系统设计的一个独特方面就是任何应用都可以启动其他应用的组件。例如，如果你想用户使用设备的相机去拍摄一张照片，这就像是另一个应用完成这个操作然后你的应用使用它，并不是为你自己的应用开发一个拍摄照片的 activity。你不需要包含或者与相机应用的代码产生什么联系。你只需要开启相机应用的 activity 然后拍照，拍摄完成后，这张图片会返回到你的应用，你可以使用它。对于用户来说，就好像这个相机是你的应用的一部分。

当系统开启一个组件，它就是开启了这个 app(如果它还没运行) 所在的进程，并且初始化这个组件需要的 class 文件。例如，如果你打开相机的一个 activity 去拍摄照片，这个 activity 是运行在它所属于的相机应用的进程，而不是你的应用的进程，因此，不想其他系统的应用，Android app 没有一个单独的入口(没有 main()方法，例如)。

因为系统使用文件权限在相互隔离的进程中运行每个应用，这样就限制了进入到其他应用，你的应用不能直接的触发其他应用的组件。但是 Android 系统可以。所有为了触发其他应用的组件，你必须给系统发送一条消息，表明你想要打开的某个特定组件的意图。系统来触发你想打开的控件。


**restrict**

	英 [rɪˈstrɪkt]   美 [rɪˈstrɪkt]  
	vt.限制，限定; 约束，束缚;

**activate**

	英 [ˈæktɪveɪt]   美 [ˈæktəˌvet]  
	vt.使活动，起动，触发; 使开始作用;

###活动的组件

activities，services 和 broadcast receivers 是被叫做 intent 的一个异步信息触发的。Intents 连接了各个组件，不管这个组件是属于你的应用或其他应用

intent 定义了一些信息来激活一个特定的组件或一类组件-intent 可以是显式的也可以是隐式的。

**asynchronous**

	英 [eɪˈsɪŋkrənəs]   
	美 [e'sɪŋkrənəs]  
	adj.异步的;

**individual**

	英 [ˌɪndɪˈvɪdʒuəl]   美 [ˌɪndəˈvɪdʒuəl]  
	adj.个人的; 独特的; 个别的;
	n.个人; 个体;

respectively

explicit

implicit

indicate


###清单文件

在系统启动一个应用的组件前，系统必须通过读取这个应用的清单文件来确保这个组件存在。你的应用必须在清单文件中声明所有的组件，这个清单文件在应用的项目路径的根目录。

####声明组件

清单文件的主要任务是将应用的组件通知到系统。


**inform**

	英 [ɪnˈfɔ:m]   美 [ɪnˈfɔrm]  
	vt.通知; 使活跃，使充满; 预示;
	vi.通知; 告发;

**consequently**

	英 [ˈkɒnsɪkwəntli]  美 [ˈkɑnsəkwentli]  
	adv.所以，因此; 因此，因而; 终于，这样; 合乎逻辑的推论是;

####声明组件功能

使用 Intent 开启组件，可以使用显示 Intent，然而 Intent 真正的强大功能是隐式 Intent 的概念。隐式 Intent 简单的描述了要执行操作的动作的类型，并让系统去寻找设备上的可以执行这个动作的组件，并启动它。如果有多个组件可以执行 Intent 描述的动作，就需要用户选择使用哪个。

The way the system identifies the components that can respond to an intent is by comparing the intent received to the intent filters provided in the manifest file of other apps on the device.

当你在清单文件中声明一个 activity 时，你可以选择包含一个 intent filter 用来声明这个 activity 的功能，这样他就可以响应设备上其他应用的 intent 了。(声明了 intent filters 的 activity 就可以被其他应用打开了)


**draft** 

	英 [drɑ:ft]  美 [dræft] 
	n.汇票; 草稿; 选派; （尤指房间、烟囱、炉子等供暖系统中的）（小股）气流;
	vt.起草; 制定; 征募;
	vi.拟稿; 绘样; 作草图;
	adj.初步画出或（写出）的; （设计、草图、提纲或版本）正在起草中的，草拟的; 以草稿形式的; 草图的;
	sentence:you can draft and send an email.

####声明应用的必需内容

    <manifest ... >
    <uses-feature android:name="android.hardware.camera.any"
      android:required="true" />
    <uses-sdk android:minSdkVersion="7" android:targetSdkVersion="19" />
    ...
    </manifest>

	上面的内容标识了，如果设备没有相机或者 Android 的版本低于2.1，就不能从 Google Play 上安装这个应用。

**appropriate**

	英 [əˈprəʊpriət]  美 [əˈproʊpriət]  
	adj.适当的; 恰当的; 合适的;
	v.盗用; 侵吞; 拨（专款等） ;

###应用资源


**presentation**

	英 [ˌpreznˈteɪʃn]   美 [ˌprizenˈteɪʃn]  
	n. 提交; 演出; 陈述，报告; 颁奖仪式;
**visual presentation**

	视觉显示;

**various**

	英 [ˈveəriəs]   美 [ˈveriəs]  
	adj.各种各样的; 多方面的; 许多的; 各个的，个别的;

**variety**

	英 [vəˈraɪəti]   美 [vəˈraɪɪti]  
	n.多样; 种类; 杂耍; 变化，多样化;
	a variety of

**optimize**

	英 [ˈɒptɪmaɪz]   美 [ˈɑptɪmaɪz]  
	vt.使最优化，使尽可能有效;

**alternative**

	英 [ɔ:lˈtɜ:nətɪv]    美 [ɔlˈtɜrnətɪv]  
	adj. 替代的; 备选的; 其他的; 另类的;
	n. 可供选择的事物;

**qualifier**

	英 [ˈkwɒlɪfaɪə(r)]    美 [ˈkwɑlɪfaɪə(r)]  
	n. 合格者，已取得资格的人; [语]修饰语; 预选赛，资格赛;

**append to**

	追加

**portrait**

	英 [ˈpɔ:treɪt]   美 [ˈpɔrtrət]  
	n.肖像，肖像画; 模型，标本; 半身雕塑像; 人物描写;
	protrait orientation:纵向方向
	landscape orientation：横向方向


# Words: #
**suffix**

	英  ['sʌfɪks]  美  ['sʌfɪks]   
	vt. 添后缀n. 后缀；下标

**isolation** 

	 英  [aɪsə'leɪʃ(ə)n]  美  [,aɪsə'leʃən]  
	n. 隔离；孤立；[电] 绝缘；[化学] 离析

**access** 

     英  ['ækses]  美  ['æksɛs]  
	vt. 使用；存取；接近n. 进入；使用权；通路

**assign** 

     英  [ə'saɪn]  美  [ə'saɪn]  
	vt. 分配；指派；[计][数] 赋值vi. 将财产过户（尤指过户给债权人）

**privilege** 

     英  [ˈprɪvəlɪdʒ]  美  [ˈprɪvəlɪdʒ] 
	 n. 特权；优待；基本权利vt. 给与…特权；特免

**arrange** 

     英  [ə'reɪn(d)ʒ]  美  [ə'rendʒ]   
	vt. 安排；排列；整理vi. 安排；排列；协商

**conserve** 

     英  [kən'sɜːv]  美  [kən'sɝv]   
	vt. 保存；将…做成蜜饯；使守恒n. 果酱；蜜饯

**certificate** 

     英  [səˈtɪfɪkɪt; (for v.,) səˈtɪfɪˌkeɪt]  美  [sɚˈtɪfɪkɪt; (for v.,) sɚˈtɪfɪˌket]  
	 vt. 发给证明书；以证书形式授权给…；用证书批准n. 证书；执照，文凭

**explicitly** 

     英  [ik'splisitli]  美  [ɪk'splɪsɪtli]  
	adv. 明确地；明白地

**grant** 

     英  [grɑːnt]  美  [ɡrænt]    
	vt. 授予；允许；承认vi. 同意n. 拨款；[法] 授予物
    n. (Grant)人名；(瑞典、葡、西、俄、罗、英、塞、德、意)格兰特；(法)格朗

**graceful** 

     英  ['greɪsfʊl; -f(ə)l]  美  ['ɡresfl]    
	 adj. 优雅的；优美的

**optimize** 

    英  ['ɒptɪmaɪz]  美  ['ɑptɪmaɪz]    
	vt. 使最优化，使完善vi. 优化；持乐观态度

**building block**

	（儿童游戏用的）积木，构件; 建筑砌块; 基础材料;(Android 组件)

**compose**  

	英 [kəmˈpəʊz]   美 [kəmˈpoʊz]
	vt.组成，构成; 调解; [印刷]排（字）; 使安定;
	vt.& vi.创作（乐曲、诗歌等）; 为…谱曲;
	vi.构图，构成;

***


##Device Compatibility 设备兼容性


**audience**

	英 [ˈɔ:diəns]   美 [ˈɔdiəns]  
	n.观众; 读者; 接见; 听众;

**tolerate**

	英 [ˈtɒləreɪt]   美 [ˈtɑləreɪt]  
	vt.容许; 承认; 忍受; 容忍（不同意或不喜欢的事物）;

**variability**

	英 [ˌveəriəˈbɪləti]   美 [ˌveriəˈbɪləti]  
	n.变化性，易变，变化的倾向; 变率;

**facilitate**

	英 [fəˈsɪlɪteɪt]   美 [fəˈsɪlɪˌtet]  
	vt.促进，助长; 使容易; 帮助;
	To facilitate your effort toward that goal, Android provides a dynamic app framework in which you can provide configuration-specific app resources in static files (such as different XML layouts for different screen sizes).

**forethought**

	英 [ˈfɔ:θɔ:t]   美 [ˈfɔrθɔt]  
	n.事先的考虑[筹划]; 远见卓识;

###"兼容性"的意思？

有两种类型的适配：设备适配和应用适配



**encounter**

	英 [ɪnˈkaʊntə(r)]   美 [ɛnˈkaʊntɚ]  
	vt.不期而遇; 遭遇; 对抗;
	n.相遇，碰见; 遭遇战; 对决，冲突;
	vi.碰见，尤指不期而遇;

	As you read more about Android development, you'll probably encounter the term "compatibility" in various situations. There are two types of compatibility: device compatibility and app compatibility.

manufacturer





###为设备控制你的应用的适用性


####设备的特性



####平台版本


####屏幕配置



###为了商业原因控制应用的适用性




#数据存储

###存储类型：SharedPreference、内部存储、外部存储、SQLite 数据库、网络链接



**persistent**
	
	英 [pəˈsɪstənt]  美 [pərˈsɪstənt] 
	adj.持续的; 坚持不懈的; 持久的; 坚持不渝;

**expose**

	英 [ɪk'spəʊz]   美 [ɪkˈspoʊz]  
	vt.
	揭露，揭发; 使暴露; 使遭受; 使曝光;

**impose**

	英 [ɪmˈpəʊz]   美 [ɪmˈpoʊz]  
	vt.强加; 征税; 以…欺骗;
	vi.利用; 欺骗; 施加影响;

####SharedPreference

存储一些私有的、原始的、以 key-value 类型的数据，

####内部存储

在设备的内存中存储的私有数据


####外部存储

存储公共的数据

每一个兼容性的 Android 手机都支持一个可供你保存文件的共享的外部存储。这个外部存储可以是一个可移除的存储媒介(像一个SD卡)或者是一个内部的存储空间(不可移除的)。当文件存储到外部存储空间中，它就是全局可读的，并且当使用USB连接到电脑进行海量存储时就变得可编辑。

	注意：当用户将外部存储挂载到电脑上或移除了媒介，外部存储就会变得不可用，没有安全强制限制的文件，你可以存到外部存储中(and there's no security enforced upon files you save to the external storage.)。在外部存储中所有的应用都可以读写这些文件，并且用户可以删除它们。


为了可以操作外部存储，首先声明两个权限：

	READ_EXTERNAL_STORAGE、WRITE_EXTERNAL_STORAGE

如果需要读写文件，只需要申请 WRITE_EXTERNAL_STORAGE 权限就可以，因为它默认隐式的申请了读取的权限

	Note：从 Android 4.4 开始，当你往应用中读取或写入私有数据时，这些权限已经不需要申请了。

#####检查存储媒介可用

	/* Checks if external storage is available for read and write */
	public boolean isExternalStorageWritable() {
	    String state = Environment.getExternalStorageState();
	    if (Environment.MEDIA_MOUNTED.equals(state)) {
	        return true;
	    }
	    return false;
	}

	/* Checks if external storage is available to at least read */
	public boolean isExternalStorageReadable() {
	    String state = Environment.getExternalStorageState();
	    if (Environment.MEDIA_MOUNTED.equals(state) ||
	        Environment.MEDIA_MOUNTED_READ_ONLY.equals(state)) {
	        return true;
	    }
    	return false;
	}

#####保存可以共享到其他应用的文件

目录类型：
	DIRECTORY_MUSIC,DIRECTORY_PICTURES,DIRECTORY_RINGTONES

    public File getAlbumStorageDir(String albumName) {
	    // Get the directory for the user's public pictures directory.
	    File file = new File(Environment.getExternalStoragePublicDirectory(
	            Environment.DIRECTORY_PICTURES), albumName);
	    if (!file.mkdirs()) {
	        Log.e(LOG_TAG, "Directory not created");
	    }
	    return file;
	}

#####将文件保存为应用私有的



**appropriate**

	英 [əˈprəʊpriət]   美 [əˈproʊpriət]  
	adj.适当的; 恰当的; 合适的;
	v.盗用; 侵吞; 拨（专款等） ;

**correspond**

	回应

**USB mass storage**

	USB 海量存储

####SQLite 数据库

在私有的数据库中，存储有固定结构的数据

####网络连接

在自己的网络服务器上存储数据

####ContentProvider
这是 Android 提供的一种向其他应用暴露你的私有数据的一种方式。

***


#System Permission
系统权限

adversely 反对地，有害地

impact  影响，

grant: 同意，承认、consent： 准许，同意

revoke：英 [rɪˈvəʊk]   美 [rɪˈvoʊk]  
vt.撤销，取消; 废除;
vi.有牌不跟;

Android 6.0(API 23) 或以上版本，应用会在运行时请求权限，并且用户可以在任何时候取消特定的权限；Android 5.1(API 22) 或以下版本，是在安装前请求权限，一旦安装完应用，如果用户想取消特定权限就只能通过卸载应用

系统定义的权限：[http://developer.android.com/reference/android/Manifest.permission.html](http://developer.android.com/reference/android/Manifest.permission.html "系统定义的权限")

用户也可以自己定义权限

###自动权限调整


###正常和危险权限
系统权限被分为多个安全级别，主要的两个安全级别是：正常、危险权限

###权限组：

###定义与执行权限

enforce：英 [ɪnˈfɔ:s]   美 [ɪnˈfɔrs]  
vt.强迫服从; 实施，执行; 加强;


    <manifest xmlns:android="http://schemas.android.com/apk/res/android"
	    package="com.me.app.myapp" >
	    <permission android:name="com.me.app.myapp.permission.DEADLY_ACTIVITY"
	        android:label="@string/permlab_deadlyActivity"
	        android:description="@string/permdesc_deadlyActivity"
	        android:permissionGroup="android.permission-group.COST_MONEY"
	        android:protectionLevel="dangerous" />
	    ...
	</manifest>

标签：

	<protectionLevel> required

	<permissionGroup> optional

	<android:label> <android:description> 是在请求权限页，展示给用户看得内容


通过 shell 命令查看系统中定义的权限：adb shell pm list permissions （后面可以加上 -s 表示可以以用户看到的样式查看定义的权限）


###在 AndroidManifest.xml 中执行权限


**accomplish** 英 [əˈkʌmplɪʃ]   美 [əˈkɑmplɪʃ]  
vt.完成; 达到（目的）; 走完（路程、距离等）; 使完美;

arbitrarily 任意地; 武断地; 反复无常地; 肆意地;

###权限检测
Context.checkCallingPermission(String permission),通过传入的权限的名称，返回一个 Integer 值，这个值表示这个权限是否当前进程中已经声明。这种方式只是在 你是从其他的进程中执行这个操作的情况下使用，

还有其他几种方式监测权限：Context.checkPermission(String,int,int)，这种方式需要知道另一个进程的 pid;
如果你知道另一个应用的包名，可以使用：PackageManager.checkPermission(String,String),第一个参数为包名，第二个参数为权限名称。



###URI 权限

sufficient

