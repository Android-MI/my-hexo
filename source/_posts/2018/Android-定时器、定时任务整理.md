---
title: Android 定时器、定时任务整理

date: 2018-01-30 13:30:12

urlname: Android-Timer

updated: 2018-01-30 13:32:22

tags:
- Android

categories: 
- 工作
- Android

comments: true
---

## 1. ScheduledExecutorService
1. Timer不支持多线程。全部挂在Timer下的任务都是单线程的，任务仅仅能串行运行。假设当中一个任务运行时间过长。会影响到其它任务的运行，然后就可能会有各种接踵而来的问题。

2. Timer的线程不捕获异常。TimerTask假设抛出异常，那么Timer唯一的进程就会挂掉，这样挂在Timer下的全部任务都会无法继续运行。

    为了弥补Timer的缺陷，jdk1.5中引入了并发包。这里面提供的ScheduledExecutorService。详细实现类是：ScheduledThreadPoolExecutor。ScheduledThreadPoolExecutor支持多线程。同一时候在线程中对异常进行了捕获。

  使用实例：

```
public class Task2 extends TimerTask{

	@SuppressWarnings("deprecation")
	@Override
	public void run() {
		System.out.println("----task2 start--------"+new Date().toLocaleString());
		try {
			Thread.sleep(5000);
		} catch (InterruptedException e) {
			e.printStackTrace();
		}
		System.out.println("----5s later, task2 end--------"+new Date().toLocaleString());
	}
}

public static void main(String[] args) {

		ScheduledExecutorService pool = Executors.newScheduledThreadPool(2);//启用2个线程
		
		Task1 t1 = new Task1();
		// 马上运行，任务消耗3秒。运行结束后等待2秒。【有空余线程时】，再次运行该任务
		pool.scheduleWithFixedDelay(t1, 0, 2, TimeUnit.SECONDS);
		
		// 马上运行，任务消耗5秒，运行结束后等待2秒。【有空余线程时】，再次运行该任务
		Task2 t2 = new Task2();
		pool.scheduleWithFixedDelay(t2, 0, 2, TimeUnit.SECONDS);
	}
```

运行结果：
![运行结果.png](http://upload-images.jianshu.io/upload_images/1552105-89b0568020832ccd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这样任务之间就不会相互影响了。并且能够同一时候运行。可是线程数量要设置好了。

#### 在Android 使用也是如此：
```
private ScheduledExecutorService scheduleTaskExecutor;

scheduleTaskExecutor = new ScheduledThreadPoolExecutor(1, new ThreadFactory() {
                    private AtomicInteger atoInteger = new AtomicInteger(0);

                    @Override
                    public Thread newThread(Runnable r) {
                        Thread t = new Thread(r);
                        t.setName("App-Thread" + atoInteger.getAndIncrement());
                        return t;
                    }
                });

// 开启执行
private void startScheduledTask() {
        scheduleTaskExecutor.scheduleAtFixedRate(new Runnable() {
            @Override
            public void run() {
                Message message = new Message();
                message.what = UPDATE_DATA;
                mHandler.sendMessage(message);
            }
        }, 1, 3, TimeUnit.SECONDS);

    }

 @Override
    protected void onDestroy() {
        super.onDestroy();
        if (scheduleTaskExecutor != null && !scheduleTaskExecutor.isShutdown()) {
            scheduleTaskExecutor.shutdown();
       }
    }
```

## 2. Timer定时器
```
private Timer mTimer;
mTimer = new Timer();

// 开启任务
private void startTimerTask() {
        mTimer.schedule(new TimerTask() {
            @Override
            public void run() {
                Message message = new Message();
                message.what = UPLOAD_RIDING_LBS;
                mMapLocHandler.sendMessage(message);
            }
        }, 1000, 3000);
}

// 取消任务
private void cancelTask(){
        if (mTimer != null) {
            mTimer.cancel();
        }
    }
```

------
## 3.定时器的三种方法
1. 第一种方法:Thread.sleep();方法

```
Runnable runnable = new Runnable() {
            @Override
            public void run() {
                while (true) {
                    mHandler.sendEmptyMessage(0);
                    try {
                        Thread.sleep(1000);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
            }
        };
new Thread(runnable).start();
```

2. 第二种方法:Handler的postDelay()方法

```
 final Runnable runnable = new Runnable() {
            @Override
            public void run() {
                if (isStart2) {
                    mHandler.sendEmptyMessage(0);
                    mHandler.postDelayed(this, 1000);
                }
            }
        };
 mHandler.postDelayed(runnable, 1000);
```

3. 第三种:Timer和TimerTask

```
 private Timer timer = new Timer();
        private TimerTask timerTask = new TimerTask() {
            @Override
            public void run() {
                mHandler.sendEmptyMessage(0);
            }
        };
timer.schedule(timerTask, 1000, 1000);
```


