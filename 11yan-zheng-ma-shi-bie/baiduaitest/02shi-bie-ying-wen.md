```
#!C:\Python36\python.exe
# -*- coding:utf-8 -*-

from aip import AipOcr

""" 你的 APPID AK SK """
APP_ID = '9588288'
API_KEY = 'lchwrQNmq2868qS6rNFXYtNG'
SECRET_KEY = 'EvlfpbVnUqWjq22EVpuR6Rjd56xV8sWg'


# 读取图片
def get_file_content(filePath):
    with open(filePath, 'rb') as fp:
        return fp.read()

# 调用通用文字识别接口

aipOcr = AipOcr(APP_ID, API_KEY, SECRET_KEY)
# result = apiOcr.basicGeneral('http://www.xxxxxx.com/img.jpg')

""" 如果有可选参数 """
options = {}
options["detect_language"] = "true"


result = aipOcr.basicGeneral(get_file_content(r"C:\Users\Administrator\Desktop\test\haibao.png"), options=options)
for key in result:
    print(key, result[key])
print(result["words_result"][0]["words"])

```



