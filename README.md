* [com.airbnb.lottie-跨平台动画库](#comairbnblottie-跨平台动画库)
* [com.scwang.smartrefresh:SmartRefreshLayout-列表刷新控件](#comscwangsmartrefreshsmartrefreshlayout-列表刷新控件)
* [com.youth.banner:banner-首页banner](#comyouthbannerbanner-首页banner)
* [com.flyco.tablayout.SlidingTabLayout-可嵌入ViewPager的TabLayout](#comflycotablayoutslidingtablayout-可嵌入viewpager的tablayout)
* [q.rorbin:VerticalTabLayout-垂直方向的TabLayout](#qrorbinverticaltablayout-垂直方向的tablayout)
* [com.just.agentweb:agentweb-高度封装的WebView](#comjustagentwebagentweb-高度封装的webview)
* [com.github.CymChad:BaseRecyclerViewAdapterHelper-通用适配器](#comgithubcymchadbaserecyclerviewadapterhelper-通用适配器)
* [com.hyman:flowlayout-lib-流式布局标签](#comhymanflowlayout-lib-流式布局标签)
* [okhttp中的cookieJar](#okhttp中的cookiejar)
* [com.squareup.leakcanary-内存泄漏检测](#comsquareupleakcanary-内存泄漏检测)
* [org.greenrobot.greendao-数据库GreenDao](#orggreenrobotgreendao-数据库greendao)
* [com.tencent.bugly:crashreport_upgrade-bugly异常上报](#comtencentbuglycrashreport_upgrade-bugly异常上报)
* [com.tencent.bugly:crashreport_upgrade-bugly应用升级](#comtencentbuglycrashreport_upgrade-bugly应用升级)
* [CompositeDisposable-RxJava中内存管理](#compositedisposable-rxjava中内存管理)


### com.airbnb.lottie-跨平台动画库
Lottie是一个支持Android、iOS、React Native，并由 Adobe After Effects制作aep格式的动画，然后经由bodymovin插件转化渲染为json格式可被移动端本地识别解析的Airbnb开源库。实时呈现After Effects动画效果，让应用程序可以像使用静态图片一样轻松地使用动画。Lottie支持API 14及以上
```
implementation "com.airbnb.android:lottie:2.3.0"
```
```
<com.airbnb.lottie.LottieAnimationView
    android:id="@+id/one_animation"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_marginStart="@dimen/dp_36"
    android:layout_marginTop="@dimen/dp_88"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintTop_toTopOf="parent" />
```
```
@BindView(R.id.one_animation)
LottieAnimationView oneAnimation;
```

```
oneAnimation.setAnimation("W.json");
oneAnimation.playAnimation();
....
if (oneAnimation != null)
{
    oneAnimation.cancelAnimation();
}
```

### com.scwang.smartrefresh:SmartRefreshLayout-列表刷新控件
```
implementation 'com.scwang.smartrefresh:SmartRefreshLayout:1.0.5.1'
implementation 'com.scwang.smartrefresh:SmartRefreshHeader:1.0.5.1'
```

```
<com.scwang.smartrefresh.layout.SmartRefreshLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:id="@+id/normal_view"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:visibility="invisible">
<!-- com.scwang.smartrefresh.layout.header.ClassicsHeader -->
    <com.scwang.smartrefresh.header.PhoenixHeader
        android:layout_width="match_parent"
        android:layout_height="wrap_content" />

    <android.support.v7.widget.RecyclerView
        android:id="@+id/recyclerView"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:background="@color/colorBackground" />
<!-- com.scwang.smartrefresh.layout.footer.ClassicsFooter -->
    <com.scwang.smartrefresh.header.TaurusHeader
        android:layout_width="match_parent"
        android:layout_height="wrap_content" />
</com.scwang.smartrefresh.layout.SmartRefreshLayout>
```
```
@BindView(R.id.normal_view)
SmartRefreshLayout refreshLayout;
```
```
private void setRefresh()
{
    refreshLayout.setOnRefreshListener( refreshLayout1 ->
    {
        presenter.autoRefresh();
        refreshLayout1.finishRefresh(1000);
    });

    refreshLayout.setOnLoadMoreListener(refreshLayout1 ->
    {
        presenter.loadMore();
        refreshLayout1.finishLoadMore(1000);
    });
}
```
### com.youth.banner:banner-首页banner
```
implementation "com.youth.banner:banner:1.4.10"
```
```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <com.youth.banner.Banner
        android:id="@+id/head_banner"
        android:layout_width="match_parent"
        android:layout_height="@dimen/dp_200"
        android:padding="@dimen/dp_10" />
</LinearLayout>
```
```
private Banner banner;

LinearLayout headerGroup = ((LinearLayout) LayoutInflater.from(_mActivity).inflate(R.layout.head_banner, null));
banner = headerGroup.findViewById(R.id.head_banner);
headerGroup.removeView(banner);
// public class ArticleListAdapter extends BaseQuickAdapter<FeedArticleData, KnowledgeHierarchyListViewHolder> {
adapter.addHeaderView(banner);

...............
banner.setBannerStyle(BannerConfig.NUM_INDICATOR_TITLE);
banner.setImageLoader(new GlideImageLoader());
banner.setImages(bannerImageList);
banner.setBannerAnimation(Transformer.DepthPage);
banner.setBannerTitles(bannerTitleList);
banner.isAutoPlay(true);
banner.setDelayTime(bannerDataList.size() * 400);
banner.setIndicatorGravity(BannerConfig.CENTER);
mBanner.setOnBannerListener(i -> JudgeUtils.startArticleDetailActivity(_mActivity,
                0, mBannerTitleList.get(i), mBannerUrlList.get(i),
                false, false, true));

banner.start();

```
```
@Override
public void onResume() {
    super.onResume();

    if (banner != null)
    {
        banner.startAutoPlay();
    }
}

@Override
public void onStop() {
    super.onStop();

    if (banner != null)
    {
        banner.stopAutoPlay();
    }
}
```

### com.flyco.tablayout.SlidingTabLayout-可嵌入ViewPager的TabLayout
```
implementation "com.flyco.tablayout:FlycoTabLayout_Lib:2.1.2@aar"
```
```
<android.support.design.widget.AppBarLayout
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:fitsSystemWindows="false"
    android:theme="@style/AppTheme.AppBarOverlay"
    app:elevation="@dimen/dp_0">

    <include layout="@layout/common_toolbar_no_scroll" />

    <com.flyco.tablayout.SlidingTabLayout
        android:id="@+id/knowledge_hierarchy_detail_tab_layout"
        android:layout_width="match_parent"
        android:layout_height="@dimen/dp_48"
        android:background="@color/colorPrimary"
        app:tl_textAllCaps="false"
        app:tl_textBold="BOTH"
        app:tl_textsize="@dimen/sp_14" />
</android.support.design.widget.AppBarLayout>

<android.support.v4.view.ViewPager
    android:id="@+id/knowledge_hierarchy_detail_viewpager"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="@color/white"
    app:layout_behavior="@string/appbar_scrolling_view_behavior" />
```
```
@BindView(R.id.knowledge_hierarchy_detail_tab_layout)
SlidingTabLayout slidingTabLayout;
```
```
viewPager.setAdapter(new FragmentPagerAdapter(getSupportFragmentManager()) {
    @Override
    public Fragment getItem(int position) {
        return fragments.get(position);
    }

    @Override
    public int getCount() {
        return fragments.size();
    }

    @Override
    public CharSequence getPageTitle(int position) {
        if (getIntent().getBooleanExtra(Constants.IS_SINGLE_CHAPTER, false))
        {
            return  chapterName;
        }
        else {
            return knowledgeHierarchyDataList.get(position).getName().trim();
        }
    }
});
slidingTabLayout.setViewPager(viewPager);
```
### q.rorbin:VerticalTabLayout-垂直方向的TabLayout
```
implementation "q.rorbin:VerticalTabLayout:1.2.5"
```
```
<q.rorbin.verticaltablayout.VerticalTabLayout
    android:id="@+id/navigation_tab_layout"
    android:layout_width="@dimen/dp_100"
    android:layout_height="match_parent"
    android:background="@color/grey_bg"
    app:tab_height="@dimen/dp_50"
    app:indicator_color="@color/white"
    app:indicator_gravity="fill"
    app:tab_margin="@dimen/dp_15"
    app:tab_mode="scrollable" />
```
```
@BindView(R.id.navigation_tab_layout)
VerticalTabLayout verticalTabLayout;
```
```
verticalTabLayout.setTabAdapter(new TabAdapter() {
    @Override
    public int getCount() {
        return navigationListDataList == null ? 0 : navigationListDataList.size();
    }

    @Override
    public ITabView.TabBadge getBadge(int position) {
        return null;
    }

    @Override
    public ITabView.TabIcon getIcon(int position) {
        return null;
    }

    @Override
    public ITabView.TabTitle getTitle(int position) {
        return new TabView.TabTitle.Builder()
                .setContent(navigationListDataList.get(position).getName())
                .setTextColor(R.color.blue, R.color.black)
                .build();
    }

    @Override
    public int getBackground(int position) {
        return -1;
    }
});

verticalTabLayout.addOnTabSelectedListener(new VerticalTabLayout.OnTabSelectedListener() {
    @Override
    public void onTabSelected(TabView tab, int position) {
        isClickTab = true;
        selectTag(position);
    }

    @Override
    public void onTabReselected(TabView tab, int position) {

    }
});

private void selectTag(int i)
{
    index = i;
    recyclerView.stopScroll();
    smoothScrollToPosition(i);
}
```


### com.just.agentweb:agentweb-高度封装的WebView
* 支持进度条以及自定义进度条
* 支持文件下载, 断点续传
* 支持下载通知形式提示进度
* 简化 Javascript 通信
* 支持返回事件处理
* 支持注入 Cookies
* WebView 安全
```
implementation 'com.just.agentweb:agentweb:3.1.0'
```
```
<FrameLayout
        android:id="@+id/article_detail_web_view"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:clipToPadding="false" />
```
```
@BindView(R.id.article_detail_web_view)
FrameLayout webview;

private AgentWeb agentWeb;
```
```
@Override
protected void initEventAndData() {
    agentWeb = AgentWeb.with(this)
            .setAgentWebParent(webview, new LinearLayout.LayoutParams(-1, -1))
            .useDefaultIndicator()
            .defaultProgressBarColor()
            .setMainFrameErrorView(R.layout.webview_error_view, -1)
            .createAgentWeb()
            .ready()
            .go(link);
}

@Override
protected void onPause() {
    super.onPause();
    agentWeb.getWebLifeCycle().onPause();
}

@Override
protected void onResume() {
    super.onResume();
    agentWeb.getWebLifeCycle().onResume();
}

@Override
protected void onDestroy() {
    agentWeb.getWebLifeCycle().onDestroy();
    super.onDestroy();
}
```

### com.github.CymChad:BaseRecyclerViewAdapterHelper-通用适配器
```
implementation 'com.github.CymChad:BaseRecyclerViewAdapterHelper:2.9.34'
```
```
private ProjectListAdapter adapter;

adapter = new ProjectListAdapter(R.layout.item_project_list, dataList);
adapter.setOnItemClickListener(((adapter1, view, position) ->
{
    StartActivityUtils.startArticleDetailActivity(_mActivity,
            adapter.getData().get(position).getId(),
            adapter.getData().get(position).getTitle().trim(),
            adapter.getData().get(position).getLink().trim(),
            adapter.getData().get(position).isCollect(),
            false, true);
}));
adapter.setOnItemChildClickListener(((adapter1, view, position) ->
{
    switch (view.getId())
    {
        case R.id.item_project_list_install_tv:
            if (TextUtils.isEmpty(adapter.getData().get(position).getApkLink()))
            {
                return;
            }
            else
            {
                startActivity(new Intent(Intent.ACTION_VIEW, Uri.parse(adapter.getData().get(position).getApkLink())));
            }
            break;
        default:
            break;
    }
}));

recyclerView.setAdapter(adapter);
```
```
public class ProjectListAdapter extends BaseQuickAdapter<FeedArticleData, ProjectListViewHolder>{

    public ProjectListAdapter(int layoutResId, @Nullable List<FeedArticleData> data) {
        super(layoutResId, data);
    }

    @Override
    protected void convert(ProjectListViewHolder helper, FeedArticleData item) {
      if (!TextUtils.isEmpty(item.getApkLink()))
        {
            helper.getView(R.id.item_project_list_install_tv).setVisibility(View.VISIBLE);
        }
        else
        {
            helper.getView(R.id.item_project_list_install_tv).setVisibility(View.GONE);
        }

        helper.addOnClickListener(R.id.item_project_list_install_tv);
    }
```
```
public class ProjectListViewHolder extends BaseViewHolder{
  @BindView(R.id.item_project_list_install_tv)
  TextView install;

public ProjectListViewHolder(View view) {
    super(view);
    ButterKnife.bind(this, view);
  }
}
```
### com.hyman:flowlayout-lib-流式布局标签
```
implementation "com.hyman:flowlayout-lib:1.1.2"
```
```
<com.zhy.view.flowlayout.TagFlowLayout
                android:id="@+id/top_search_flow_layout"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                app:max_select="0" />
```
```
@BindView(R.id.top_search_flow_layout)
TagFlowLayout topSearchTagFlow;
```
```
topSearchTagFlow.setAdapter(new TagAdapter<TopSearchData>(topSearchDataList) {
            @Override
            public View getView(FlowLayout parent, int position, TopSearchData topSearchData) {
                assert getActivity() != null;

                TextView tv = (TextView)LayoutInflater.from(getActivity()).inflate(R.layout.flow_layout_tv, parent, false);
                if (topSearchData != null)
                {
                    tv.setText(topSearchData.getName());
                }

                topSearchTagFlow.setOnTagClickListener((view, position1, parent1) ->
                {
                    presenter.addHistoryData(topSearchDataList.get(position1).getName().trim());
                    setHistoryTvStatus(false);
                    searchEdit.setText(topSearchDataList.get(position1).getName().trim());
                    searchEdit.setSelection(searchEdit.getText().length());
                    return true;
                });

                return tv;
            }
        });
```
### okhttp中的cookieJar
```
new OkHttpClient.Builder().builder.cookieJar(new CookiesManager());
```
```
public class CookiesManager implements CookieJar {
    private static final PersistentCookieStore COOKIE_STORE = new PersistentCookieStore();

    @Override
    public void saveFromResponse(HttpUrl url, List<Cookie> cookies) {
        if (cookies.size() > 0)
        {
            for (Cookie cookie:cookies) {
                COOKIE_STORE.add(url, cookie);
            }
        }
    }

    @Override
    public List<Cookie> loadForRequest(HttpUrl url) {
        return COOKIE_STORE.get(url);
    }

    public static void clearAllCookies()
    {
        COOKIE_STORE.removeAll();
    }
}
```
```
CookiesManager.clearAllCookies();
```

### com.squareup.leakcanary-内存泄漏检测
```
debugImplementation 'com.squareup.leakcanary:leakcanary-android:1.5.4'
releaseImplementation 'com.squareup.leakcanary:leakcanary-android-no-op:1.5.4'
androidTestImplementation 'com.squareup.leakcanary:leakcanary-android-no-op:1.5.4'
```   
`在Application的onCreate中初始化`  
```
private RefWatcher refWatcher;

public static RefWatcher getRefWatcher(Context context)
{
    GeeksApp application = (GeeksApp)context.getApplicationContext();
    return application.refWatcher;
}
```
```
refWatcher = LeakCanary.install(this);
```

### org.greenrobot.greendao-数据库GreenDao
```
apply plugin: 'org.greenrobot.greendao'
...
greendao {
    schemaVersion 1
    targetGenDir 'src/main/java'
    daoPackage 'com.hsf1002.sky.wanandroid.core.dao'
}
...
implementation 'org.greenrobot:greendao:3.2.2'
```
```
@Entity
public class HistoryData {
    private long date;
    private String data;

    @Generated(hash = 1452354993)
    public HistoryData(long date, String data) {
        this.date = date;
        this.data = data;
    }
    @Generated(hash = 422767273)
    public HistoryData() {
    }
    public long getDate() {
        return this.date;
    }
    public void setDate(long date) {
        this.date = date;
    }
    public String getData() {
        return this.data;
    }
    public void setData(String data) {
        this.data = data;
    }
}
```
`创建实例文件后make project,会自动生成3个文件,HistoryDataDao, DaoMaster和DaoSession,接着在Application的onCreate中初始化`  
```
private DaoSession mDaoSession;

private void initGreenDao()
{
    DaoMaster.DevOpenHelper devOpenHelper = new DaoMaster.DevOpenHelper(this, Constants.DB_NAME);
    SQLiteDatabase database = devOpenHelper.getWritableDatabase();
    DaoMaster daoMaster = new DaoMaster(database);
    mDaoSession = daoMaster.newSession();
}

public DaoSession getDaoSession()
{
    return mDaoSession;
}
```
`最后根据daoSession和HistoryDataDao进行增删改插操作`  
```
@Override
public List<HistoryData> loadAllHistoryData() {
    HistoryDataDao historyDataDao = daoSession.getHistoryDataDao();

    return historyDataDao.loadAll();
}
...
```

### com.tencent.bugly:crashreport_upgrade-bugly异常上报
```
implementation 'com.tencent.bugly:crashreport_upgrade:latest.release'
```
[腾讯bugly](https://bugly.qq.com/v2/workbench/apps)   

`在Application的onCreate中初始化`  

```
private void initBugly()
{
    String packageName = getApplicationContext().getPackageName();
    String processName = CommonUtils.getProcessName(android.os.Process.myPid());    CrashReport.UserStrategy strategy = new CrashReport.UserStrategy((getApplicationContext()));
    strategy.setUploadProcess((processName == null) || processName.equals(packageName));
    CrashReport.initCrashReport(getApplicationContext(), Constants.BUGLY_ID, false, strategy);
}
```

### com.tencent.bugly:crashreport_upgrade-bugly应用升级
```
implementation 'com.tencent.bugly:nativecrashreport:latest.release'
```
`在Application的onCreate中初始化`    

```
private void initBugly()
{
    //String packageName = getApplicationContext().getPackageName();
    //String processName = CommonUtils.getProcessName(android.os.Process.myPid());

    //CrashReport.UserStrategy strategy = new CrashReport.UserStrategy((getApplicationContext()));
    //strategy.setUploadProcess((processName == null) || processName.equals(packageName));
    //CrashReport.initCrashReport(getApplicationContext(), Constants.BUGLY_ID, false, strategy);
    Bugly.init(getApplicationContext(), Constants.BUGLY_ID, false);
}
```

1. 需要将CrashReport相关代码屏蔽掉
2. 做升级包的versioncode不得低于原始包
```
versionCode 6
versionName "1.3"
```
3. 升级包在网站[bugly后台](https://beta.bugly.qq.com/apps/8943890099/allupdate?pid=1)启动后,需杀死并重启应用才能生效
4. 如果升级安装包时提示:已安装了存在签名冲突的同名数据包,则原始包需要先签名,并在此基础上做升级包(Build->Generate Singed APK,如无签名文件先创建之)  

```
signingConfigs{
    releaseConfig{
        keyAlias 'key0'
        keyPassword '123456'
        storeFile file('/home/workspace1/workplace/android/Awesome-WanAndroid/awesome/key.jks')
        storePassword '123456'
    }
}

buildTypes {
    release {
        minifyEnabled false
        signingConfig signingConfigs.releaseConfig
        proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
    }

    debug {
        signingConfig signingConfigs.releaseConfig
    }
```
5. 编译错误提示:`Keystore not found for signing config`,storeFile要使用完整路径

```
storeFile file('/home/workspace1/workplace/android/Awesome-WanAndroid/awesome/key.jks')
```
6. 编译错误提示:`not found for signing config 'externalOverride'`,需要确保storeFile路径正确

`支持手动升级,只需两步操作`  

```
private void initBugly()
{
    com.tencent.bugly.beta.Beta.autoCheckUpgrade = false;
    Bugly.init(getApplicationContext(), Constants.BUGLY_ID, false);
}
```
`在比如点击按钮时检测更新`  

```
navigationView.getMenu().findItem(R.id.nav_item_update)
        .setOnMenuItemClickListener( item ->
        {
            Beta.checkUpgrade();
            return true;
        });
```

### CompositeDisposable-RxJava中内存管理
订阅了事件后没有及时取阅，会导致在activity或者fragment销毁后仍然占用着内存，无法释放。而disposable便是这个订阅事件，可以用来取消订阅, compositeDisposable是一个disposable的容器，可以容纳多个disposable，添加和去除的复杂度为O(1),用CompositeDisposable来管理订阅事件disposable，然后在acivity或fragment销毁的时候，调用compositeDisposable.dispose()就可以切断所有订阅事件，防止内存泄漏  

```
public class BasePresenter<T extends BaseView> implements AbstractPresenter<T> {

    protected T mView;
    private CompositeDisposable compositeDisposable;

    protected void addSubscribe(Disposable disposable) {
        if (compositeDisposable == null) {
            compositeDisposable = new CompositeDisposable();
        }
        compositeDisposable.add(disposable);
    }

    @Override
    public void attachView(T view) {
        this.mView = view;
    }

    @Override
    public void detachView() {
        this.mView = null;
        if (compositeDisposable != null) {
            compositeDisposable.clear();
        }
    }
}
```
