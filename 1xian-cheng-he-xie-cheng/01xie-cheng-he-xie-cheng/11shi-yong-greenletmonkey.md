```py
'''
使用gevent +　monkey.patch_all()自动调度网络IO协程
'''
import gevent
import requests
import time
from gevent import monkey


def getPageText(url, order=0):
    print("No%d:%s请求开始..." % (order, url))
    resp = requests.get(url)  # 发起网络请求，返回需要时间——阻塞IO

    html = resp.text
    print("No%d:%s成功返回：长度为%d" % (order, url, len(html)))
    pass


# 将【标准库-阻塞IO实现】替换为【gevent-非阻塞IO实现】
monkey.patch_all()
if __name__ == '__main__':
    start = time.time()
    time.clock()
    gevent.joinall([
        gevent.spawn(getPageText, "http://www.sina.com", order=1),
        gevent.spawn(getPageText, "http://www.qq.com", order=2),
        gevent.spawn(getPageText, "http://www.baidu.com", order=3),
        gevent.spawn(getPageText, "http://www.163.com", order=4),
        gevent.spawn(getPageText, "http://www.4399.com", order=5),
        gevent.spawn(getPageText, "http://www.sohu.com", order=6),
        gevent.spawn(getPageText, "http://www.youku.com", order=7),
        gevent.spawn(getPageText, "http://www.iqiyi.com", order=8),
    ])

    end = time.time()
    print("over，耗时%d秒" % (end - start))
    print(time.clock())
    pass

```



