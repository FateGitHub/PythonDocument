```py
'''
使用Barrier调度线程：足三而行
'''
import threading
import time


def sayGoodbye():
    print("我们先撤尔等殿后")


# 3=足三而行
# action=放行时回调
# timeout=超时时间（等待超时会抛出BrokenBarrierError异常）
bar = threading.Barrier(3, action=sayGoodbye, timeout=5)


def doSth(arg):
    # 阻塞等待足三而行
    # 等待超时会抛出BrokenBarrierError异常
    tname = threading.current_thread().getName()
    try:
        bar.wait()
    except threading.BrokenBarrierError:
        print("栅栏已被捣毁，呼叫总部支援！")
        print("%s：妈的智障，劳资还要回家学拍森呢!" % (tname))
        pass

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



