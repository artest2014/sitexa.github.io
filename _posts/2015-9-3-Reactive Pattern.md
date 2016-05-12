---
layout: post
title: Reactive Pattern, RxJava & RxAndroid & Retrofit
category: 'java'
---

## 基础

RxJava最核心的两个东西是Observables（观察者，事件源）和Subscribers（订阅者）。Observables发出一系列事件，Subscribers处理这些事件。这里的事件可以是任何你感兴趣的东西（触摸事件，web接口调用返回的数据。。。）

一个Observable可以发出零个或者多个事件，知道结束或者出错。每发出一个事件，就会调用它的Subscriber的onNext方法，最后调用Subscriber.onComplete()或者Subscriber.onError()结束。

Rxjava的看起来很象设计模式中的观察者模式，但是有一点明显不同，那就是如果一个Observerble没有任何的的Subscriber，那么这个Observable是不会发出任何事件的。

### Hello world

创建一个Observable对象很简单，直接调用Observable.create即可.

    Observable<String> myObservable = Observable.create(  
        new Observable.OnSubscribe<String>() {  
            @Override  
            public void call(Subscriber<? super String> sub) {  
                sub.onNext("Hello, world!");  
                sub.onCompleted();  
            }  
        }  
    );  
    
接着我们创建一个Subscriber来处理Observable对象发出的字符串。

    Subscriber<String> mySubscriber = new Subscriber<String>() {  
        @Override  
        public void onNext(String s) { System.out.println(s); }  
      
        @Override  
        public void onCompleted() { }  
      
        @Override  
        public void onError(Throwable e) { }  
    };  
    
通过subscribe函数就可以将我们定义的myObservable对象和mySubscriber对象关联起来，这样就完成了subscriber对observable的订阅。
    
    myObservable.subscribe(mySubscriber);  
    
subscribe方法有一个重载版本，接受三个Action1类型的参数，分别对应OnNext，OnComplete， OnError函数。
    
    myObservable.subscribe(onNextAction, onErrorAction, onCompleteAction);  
    
定义onNextAction:
    
    Action1<String> onNextAction = new Action1<String>() {  
        @Override  
        public void call(String s) {  
            System.out.println(s);  
        }  
    };
    
指定订阅者：
    
    myObservable.subscribe(onNextAction); 
    
或者写成：
    
    Observable.just("Hello, world!")  
        .subscribe(new Action1<String>() {  
            @Override  
            public void call(String s) {  
                  System.out.println(s);  
            }  
        });  
        
或者使用Java8的lambda写成：

    Observable.just("Hello, world!")  
        .subscribe(s -> System.out.println(s));  
    
### 操作符(Operators)

####  map
    
    Observable.just("Hello, world!")  
        .map(s -> s + " -Dan")  
        .subscribe(s -> System.out.println(s)); 
        
    Observable.just("Hello, world!")  
        .map(s -> s.hashCode())  
        .subscribe(i -> System.out.println(Integer.toString(i)));  
                
####  flatMap

Observable.flatMap()接收一个Observable的输出作为输入，同时输出另外一个Observable。
    
    query("Hello, world!")  
        .flatMap(urls -> Observable.from(urls))  
        .subscribe(url -> System.out.println(url));  

它可以返回任何它想返回的Observable对象.
    
    query("Hello, world!")  
        .flatMap(urls -> Observable.from(urls))  
        .flatMap(url -> getTitle(url))  
        .subscribe(title -> System.out.println(title));  

####  filter

从返回的title列表中过滤掉null值.
    
    query("Hello, world!")  
        .flatMap(urls -> Observable.from(urls))  
        .flatMap(url -> getTitle(url))  
        .filter(title -> title != null)  
        .subscribe(title -> System.out.println(title));  
####  take

我们只想要最多5个结果：

    query("Hello, world!")  
        .flatMap(urls -> Observable.from(urls))  
        .flatMap(url -> getTitle(url))  
        .filter(title -> title != null)  
        .take(5)  
        .subscribe(title -> System.out.println(title));
        
####  doOnNext

把每个标题保存到磁盘：

    query("Hello, world!")  
        .flatMap(urls -> Observable.from(urls))  
        .flatMap(url -> getTitle(url))  
        .filter(title -> title != null)  
        .take(5)  
        .doOnNext(title -> saveTitle(title))  
        .subscribe(title -> System.out.println(title));  

### 异常处理
    Observable.just("Hello, world!")
        .map(s -> potentialException(s))
        .map(s -> anotherPotentialException(s))
        .subscribe(new Subscriber<String>() {
            @Override
            public void onNext(String s) { System.out.println(s); }
    
            @Override
            public void onCompleted() { System.out.println("Completed!"); }
    
            @Override
            public void onError(Throwable e) { System.out.println("Ouch!"); }
        });
    
### 调度器

使用RxJava，你可以使用subscribeOn()指定观察者代码运行的线程，使用observerOn()指定订阅者运行的线程
    
    myObservableServices.retrieveImage(url)
        .subscribeOn(Schedulers.io())
        .observeOn(AndroidSchedulers.mainThread())
        .subscribe(bitmap -> myImageView.setImageBitmap(bitmap));
    
### 订阅（Subscriptions）
    
    Subscription subscription = Observable.just("Hello, World!")
        .subscribe(s -> System.out.println(s));
    subscription.unsubscribe();
    System.out.println("Unsubscribed=" + subscription.isUnsubscribed());
    
### RxAndroid

RxAndroid是RxJava的一个针对Android平台的扩展。它包含了一些能够简化Android开发的工具。

### Retrofit
    
    @GET("/user/{id}/photo")
    void getUserPhoto(@Path("id") int id, Callback<Photo> cb);
  
    @GET("/user/{id}/photo")
    Observable<Photo> getUserPhoto(@Path("id") int id);
  
    Observable.zip(
        service.getUserPhoto(id),
        service.getPhotoMetadata(id),
        (photo, metadata) -> createPhotoWithData(photo, metadata))
        .subscribe(photoWithData -> showPhoto(photoWithData));
        
