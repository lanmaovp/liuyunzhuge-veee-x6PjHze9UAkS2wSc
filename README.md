
## 模块介绍


该模块主要用于python的任务调度，使用简便友好的python语法定期运行python函数或者一些其他的调用对象，这个模块就类似于windows的任务计划和linux的crontab，都是用于在服务器上周期性执行某段python脚本。


相较于linux的crontab对比：


1. schedule模块支持以秒为单位的周期性任务，而crontab只能完成以分钟为单位的。
2. schedule模块当有很多个任务需要执行时管理起来很方便，直接内嵌到代码当中，crontab还需要每一个脚本去设置一次，增加了复杂度。
3. 轻量级，无需任何依赖


## 模块安装



```
pip install schedule
# pip3 安装
pip3 install schedule

```

国内安装获取软件包可能会很慢，可以采用国内各大加速进行安装



```
# 清华大学源
pip install schedule -i https://pypi.tuna.tsinghua.edu.cn/simple	
# 阿里云源
pip install schedule -i https://mirrors.aliyun.com/pypi/simple
# 豆瓣源
pip instal lschedule -i http://pypi.douban.com/simple

```

## 模块案例



```
# 载入模块
import schedule 

# 创建需要的方法
def job():
    print("输出结果")

# 设置执行方法
schedule.every().minutes.do(job)

# 设置循环执行
while True:
    schedule.run_pending()	# 运行定时任务
    time.sleep(1)	# 上一次定时任务执行完后间隔1S再执行第二次

```


> 代码解释：以上代码是定义了每分钟执行一次job方法，执行完成后中间间隔一秒执行下一次job方法


## 模块参数用法


schedule模块提供了多种定时方法，比如按秒、按分钟、按小时、按周、按月、按年等等，都可以进行自定义，针对不同的定时任务选用特定的定时方法。



```
# 每秒执行一次
schedule.every().seconds.do(job)

# 每30秒执行一次
schedule.every(30).seconds.do(job)

# 每分钟执行一次
schedule.every().minutes.do(job)

# 每30分钟执行一次
schedule.every(30).minutes.do(job)

# 每小时执行一次
schedule.every().hour.do(job)

# 每2小时执行一次
schedule.every(2).hour.do(job)

# 每天执行一次 
schedule.every().day.do(job)

# 每天11点执行一次
schedule.every().day。at("11:00").do(job)

# 每周执行一次
schedule.every().week.do(job)

# 每周三执行一次
schedule.every().wednesday.do(job)

```


> 周一到周日用 monday、tuesday、wednesday、thursday、friday、saturday、sunday


## 单次执行


上面说的都是重复执行的任务，如果想单词执行一次任务的话，可以return一下就可以了



```
# 载入模块
import schedule 

# 创建需要的方法
def job():
    print("输出结果")
    return schedule.CancelJob	# 取消执行任务

# 设置执行方法
schedule.every().minutes.do(job)

# 设置循环执行
while True:
    schedule.run_pending()	# 运行定时任务
    time.sleep(1)	# 上一次定时任务执行完后间隔1S再执行第二次

```

## 取消指定任务


如果有多个任务想单独某个任务停止执行或者可以设置判断某个情况下停止执行任务



```
# 载入模块
import schedule 

# 创建需要的方法
def job():
    print("输出结果")
    return schedule.CancelJob	# 取消执行任务

# 设置执行方法
schedule.every().minutes.do(job).tag(job)	# 设置标签为job
schedule.every(10).minutes.do(job).tag(job10)	# 设置标签为job10
schedule.every(20).minutes.do(job).tag(job20)	# 设置标签为job20

schedule.clear('job')	# 取消标签为job的定时任务
# 设置循环执行
while True:
    schedule.run_pending()	# 运行定时任务
    time.sleep(1)	# 上一次定时任务执行完后间隔1S再执行第二次

```

## 方法传输参数



```
# 载入模块
import schedule 

# 创建需要的方法
def job(name):
    print(name)

# 设置执行方法
schedule.every().minutes.do(job, name=job)

# 设置循环执行
while True:
    schedule.run_pending()	# 运行定时任务
    time.sleep(1)	# 上一次定时任务执行完后间隔1S再执行第二次

```

 本博客参考[slower加速器](https://chundaotian.com)。转载请注明出处！
