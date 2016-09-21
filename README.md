# DragSlopLayout
一个辅助开发的UI库，适用于某些特殊场景，如固定范围拖拽、动画、模糊效果等。

Screenshot
---

#### Drag模式，可以和 ViewPager 联动
![Drag](https://github.com/Rukey7/AndroidCommon/blob/master/ScreenShot/DragSlopLayout/drag.gif)

#### Animate模式，同样可以和 ViewPager 联动(自定义动画无联动效果)
![Animate](https://github.com/Rukey7/AndroidCommon/blob/master/ScreenShot/DragSlopLayout/animate.gif)

#### Blur模糊效果，包括局部模糊和全图模糊
![Local Blur](https://github.com/Rukey7/AndroidCommon/blob/master/ScreenShot/DragSlopLayout/local.jpg)  ![Full Blur](https://github.com/Rukey7/AndroidCommon/blob/master/ScreenShot/DragSlopLayout/full.jpg)

Gradle
---

### dependencies
```groovy
compile 'com.dl7.drag:dragsloplayout:1.0.1'
```
### Enable RenderScript support mode
```groovy
android {
    defaultConfig {
        renderscriptTargetApi 23
        renderscriptSupportModeEnabled true
    }
}
```

Usage
---

### 属性
|name|format|description|
|:---:|:---:|:---:|
| mode | enum | drag 或则 animate, 默认为 drag
| fix_height | dimension | drag模式收缩的高度, 默认为 0
| max_height | dimension | drag模式展开的高度，默认为布局高度的 2/3

### 布局
```xml
<com.dl7.drag.DragSlopLayout
	android:id="@+id/drag_layout"
	android:layout_width="match_parent"
	android:layout_height="match_parent"
	android:background="@android:color/black"
	app:fix_height="80dp"
	app:mode="drag">
		<!-- Content View -->
		<android.support.v4.view.ViewPager
		android:id="@+id/vp_photo"
		android:layout_width="match_parent"
		android:layout_height="match_parent"/>
		
		<!-- Drag View -->
		<LinearLayout
		android:layout_width="match_parent"
		android:layout_height="wrap_content"
		android:orientation="vertical">
		// ......
	</LinearLayout>
	// ......
</com.dl7.drag.DragSlopLayout>
```
	
### 如果 Content View 为 ViewPager，通过以下方法来实现联动效果：
```java
    mDragLayout.interactWithViewPager(true);
```
### 如果 Drag View 包含 ScrollView 或则 NestedScrollView，通过以下方法来实现平滑滚动：
```java
    mDragLayout.setAttachScrollView(mSvView);
```
### Content View 的模糊效果，这功能是通过模糊预处理再来动态加载的，所以对于 Content View  为 ViewPager 的界面不适用，主要用来模糊固定的背景界面
```java
    mDragLayout.setEnableBlur(true);	// 开启模糊
    mDragLayout.setBlurFull(true);	// 设置全背景模糊，默认为局部模糊
    mDragLayout.updateBlurView();	// 更新模糊背景
```
### 控制 Drag View 的进入和退出
```java
    mDragLayout.scrollInScreen(int duration);	// Drag 模式
    mDragLayout.scrollOutScreen(int duration);	// Drag 模式

    mDragLayout.startInAnim();	// Animate 模式
    mDragLayout.startOutAnim();	// Animate 模式
    mDsLayout.setAnimatorMode(DragSlopLayout.FLIP_Y);	// 设置动画模式
```
    
Thanks
---

- [500px-android-blur](https://github.com/500px/500px-android-blur)
- [AndroidViewAnimations](https://github.com/daimajia/AndroidViewAnimations)
    
License
-------

    Copyright 2016 Rukey7

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
