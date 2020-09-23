# iOS14UIPageControlFix
兼容iOS14下设置currentImage

在iOS14下UIPageControl的currentImage与pageImage私有属性与方法做了保护措施，用汇编看了下，好像是调用setCurrentImage的时候，系统直接写了一个异常抛出，为什么系统自己调用没问题呢，是因为把具体实现放到了另一个地方(貌似是C函数)，直接调用那个函数来操作，有兴趣的哥们可以尝试直接去拿那个函数去设置。

```objc
// 兼容iOS14与iOS14之前
- (void)ios14_zjhourSetCurrentImage:(UIImage *)currentImage pageImage:(UIImage *)pageImage;
```

因为iOS14系统提供了设置图片的方法，但是系统的方法要配合color相关的方法来处理，会对设置的图片做tintColor的处理，因此本方法思路是拦截系统pageControl指示器图片设置图片对图片的渲染
