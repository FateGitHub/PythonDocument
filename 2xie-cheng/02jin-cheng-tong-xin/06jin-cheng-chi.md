```py
'''
进程池示例
'''
import multiprocessing
import random

import time


def func(arg, name):
    print("正在执行{0}...".format(arg))
    time.sleep(random.randint(1, 5))
    print("进程%d完毕！" % (name))

    return "fuck"
    pass


def func2(arg, name):
    print("正在执行任务2{0}...".format(arg))
    time.sleep(random.randint(1, 5))
    print("进程%d完毕！" % (name))

    return "fuck"
    pass


# 结束回调函数
def onFuncReturn(result):
    print("得到结果{0}".format(result))
    pass


# 异步进程池示例
def asyncPoolDemo():
    # 创建一个3并发的进程池
    pool = multiprocessing.Pool(3)
    # 添加5条异步进程，执行函数各不相同，有统一的结束回调
    pool.apply_async(func=func, args=("hello", 1), callback=onFuncReturn)
    pool.apply_async(func=func2, args=("阿西吧", 2), callback=onFuncReturn)
    pool.apply_async(func=func, args=("fuck off", 3), callback=onFuncReturn)
    pool.apply_async(func=func2, args=("bye", 4), callback=onFuncReturn)
    pool.apply_async(func=func, args=("雅蠛蝶", 5), callback=onFuncReturn)
    # 关闭进程池，不再接收新的进程
    pool.close()
    # 开始所有任务，令主进程阻塞等待池中所有进程执行完毕
    pool.join()


# 同步进程池示例
def syncPoolDemo():
    # 创建一个3并发的进程池
    pool = multiprocessing.Pool(3)

    # 添加5条同步进程，执行函数各不相同
    pool.apply(func=func, args=("hello", 1))
    pool.apply(func=func2, args=("阿西吧", 2))
    pool.apply(func=func, args=("fuck off", 3))
    pool.apply(func=func2, args=("bye", 4))
    pool.apply(func=func, args=("雅蠛蝶", 5))

    # 关闭进程池，不再接收新的进程
    pool.close()
    # 开始所有任务，令主进程阻塞等待池中所有进程执行完毕
    pool.join()


if __name__ == "__main__":
    # asyncPoolDemo()
    syncPoolDemo()

    print("main over")

```



