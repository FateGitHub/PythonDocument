```py
'''
通过继承Process实现自定义进程
'''
import multiprocessing
import os

import time

# 通过继承于Process实现自定义进程
class MyProcess(multiprocessing.Process):

    def __init__(self,name):
        super().__init__()
        self.name = name

    def run(self):
        pid = os.getpid()
        ppid = os.getppid()
        pname = multiprocessing.current_process().name
        print("劳资名叫%s,ID是%d,我爸ID是%d"%(pname,pid,ppid))
        time.sleep(10000)
        print("-----劳资卒于%s-----"%(time.ctime()))


def func():
    pass


if __name__ == "__main__":
    MyProcess("战狼中队冷锋").start()
    MyProcess("战狼中队热风").start()
    MyProcess("战狼中队暴风").start()

    print("主进程ID是",multiprocessing.current_process().pid)

    # 获取CPU核数
    coreCount = multiprocessing.cpu_count()
    print("劳资的CPU是%d核的"%(coreCount))

    # 获得当前活动进程列表
    plist = multiprocessing.active_children()
    for p in plist:
        print(p.name)

    print("main over")
```



