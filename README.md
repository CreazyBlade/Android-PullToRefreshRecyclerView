# Android-PullToRefreshRecyclerView

![Screenshot](https://github.com/HomHomLin/Android-PullToRefreshRecyclerView/blob/master/screenshot.gif)

这是一个可以下拉刷新的RecyclerView，并且支持方便添加Header、滑动到底部自动加载更多以及其他ListView的功能，可以帮助你在RecyclerView里实现ListView拥有但RecyclerView没有的功能。

**Latest version：v1.0.0**

## Feature
 * 基于原生RecyclerView的封装
 * 支持下拉刷新
 * 支持滑动到底部自动加载更多
 * 实现了ListView大部分API
 * 支持方便添加Header头部（原生RecyclerView不支持）
 * 支持设置EmptyView
 * 目前支持的LayoutManager模式:
 	* **LinearLayoutManager**
 	* **GridLayoutManager**

Project site： <https://github.com/HomHomLin/Android-PullToRefreshRecyclerView>.

## Sample
There has a Sample in project:[Sample](https://github.com/HomHomLin/Android-PullToRefreshRecyclerView/blob/master/sample.apk)

##Using library in your application

**Gradle dependency:**
``` groovy
compile 'homhomlin.lib:ptrrv-library:1.0.0'
```

or

**Maven dependency:**
``` xml
<dependency>
	<groupId>homhomlin.lib</groupId>
	<artifactId>ptrrv-library</artifactId>
	<version>1.0.0</version>
</dependency>
```

##Usage

PullToRefreshRecyclerView is easy to use just like ListView and RecyclerView.

**First: Config in xml**
``` xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <com.lhh.ptrrv.library.PullToRefreshRecyclerView
        android:id="@+id/ptrrv"
        android:layout_width="match_parent"
        android:layout_height="match_parent"/>

</RelativeLayout>
```

**Second: Find it in your Activity**
``` java
PullToRefreshRecyclerView mPtrrv = (PullToRefreshRecyclerView) this.findViewById(R.id.ptrrv);
```

**Third: Config it in java code**
``` java
        // set true to open swipe(pull to refresh, default is true)
        mPtrrv.setSwipeEnable(true);

        // set the layoutManager which to use
        mPtrrv.setLayoutManager(new LinearLayoutManager(this));

        // set PagingableListener
        mPtrrv.setPagingableListener(new PullToRefreshRecyclerView.PagingableListener() {
            @Override
            public void onLoadMoreItems() {
                //do loadmore here
            }
        });

        // set OnRefreshListener
        mPtrrv.setOnRefreshListener(new SwipeRefreshLayout.OnRefreshListener() {
            @Override
            public void onRefresh() {
                // do refresh here
            }
        });

        // add item divider to recyclerView
        mPtrrv.getRecyclerView().addItemDecoration(new DividerItemDecoration(this,
                DividerItemDecoration.VERTICAL_LIST));

        // add headerView
        mPtrrv.addHeaderView(View.inflate(this, R.layout.header, null));

        //set EmptyVIEW
        mPtrrv.setEmptyView(View.inflat(this,R.layout.empty_view, null));

        // set loadmore String
        mPtrrv.setLoadmoreString("loading");

        // set loadmore enable, onFinishLoading(can load more? , select before item)
        mPtrrv.onFinishLoading(true, false);
```

**Finally: Set the adapter which extends RecyclerView.Adpater**
``` java
        PtrrvAdapter mAdapter = new PtrrvAdapter(this);
        mPtrrv.setAdapter(mAdapter);
```

##License
Copyright 2015 LinHongHong

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.