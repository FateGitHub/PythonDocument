```py
'''
使用Semaphore调度线程：控制最大并发量
'''
import threading

import time

# 允许最大并发量3
sem = threading.Semaphore(3)


def doSth(arg):
    with sem:
        tname = threading.current_thread().getName()
        print("%s正在执行【%s】" % (tname, arg))
        time.sleep(1)
        print("-----%s执行完毕!-----\n" % (tname))
        time.sleep(0.1)


if __name__ == '__main__':

    # 开启10条线程
    for i in range(10):
        threading.Thread(target=doSth, args=("巡山",), name="小分队%d" % (i)).start()
    pass

```



