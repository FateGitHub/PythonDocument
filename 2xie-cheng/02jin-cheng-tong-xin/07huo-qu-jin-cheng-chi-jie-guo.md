```py
'''
about what
'''

# 异步进程池示例
import multiprocessing
import random

import time


def func(arg, name):
    print("正在执行{0}...".format(arg))
    time.sleep(random.randint(1, 5))
    print("进程%d完毕！" % (name))

    return random.sample(["fuck", "阿西吧", "雅蠛蝶", "你妹"], 1)
    pass


# 结束回调函数
def onFuncReturn(result):
    print("得到结果{0}".format(result))
    pass


def getPoolResultAsync():
    # 创建一个3并发的进程池
    pool = multiprocessing.Pool(3)

    # 添加5条异步进程，执行函数各不相同，有统一的结束回调
    reslist = []
    for i in range(5):
        # 立刻返回一个结果的包装器（包装器内暂时还没有func的真正返回值）
        res = pool.apply_async(func=func, args=("hello", i), callback=onFuncReturn)
        print("立刻打印结果：", res)  # <multiprocessing.pool.ApplyResult object at 0x000001FA4FB70908>

        # 收集结果（的包装器）
        reslist.append(res)

    # 关闭进程池，不再接收新的进程
    pool.close()
    # 开始所有任务，令主进程阻塞等待池中所有进程执行完毕
    pool.join()

    # 打印结果(包装器内已有进程函数的执行结果)
    for res in reslist:
        print(res.get())  # 从结果包装器中拿到返回值并打印


def getPoolResultSync():
    # 创建一个3并发的进程池
    pool = multiprocessing.Pool(3)

    # 添加5条异步进程，执行函数各不相同，有统一的结束回调
    reslist = []
    for i in range(5):
        # 直接获得返回值【异步结果.get()】【源码：return self.apply_async(func, args, kwds).get()——异步变同步！】
        res = pool.apply(func=func, args=("hello", i))

        # 收集结果
        reslist.append(res)

    # 关闭进程池，不再接收新的进程
    pool.close()
    # 开始所有任务，令主进程阻塞等待池中所有进程执行完毕
    pool.join()

    # 打印结果
    for res in reslist:
        print(res)


if __name__ == "__main__":
    getPoolResultAsync()
    # getPoolResultSync()
    print("main over")

```



