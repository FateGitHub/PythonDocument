```py
'''
使用Semaphore控制进程的最大并发
'''
import multiprocessing

import time


def func(sem):
    with sem:
        print("%s开始执行..." % (multiprocessing.current_process().name))
        time.sleep(3)
        print("%sdone!" % (multiprocessing.current_process().name))


if __name__ == "__main__":
    sem = multiprocessing.Semaphore(3)
    for i in range(7):
        multiprocessing.Process(target=func, name="劳资的队伍-%d" % (i), args=(sem,)).start()

    print("main over")

```



