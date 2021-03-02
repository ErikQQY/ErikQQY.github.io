---
tags: Python
---
# Selenium抓取YouTube评论制作词云
作为黄老板的忠实歌迷，闲逛黄老板YouTube的时候发现有这么一条动态：
[跳转到YouTube](https://www.youtube.com/post/UgxSXlrxP5BQG0l5IZR4AaABCQ?lc=UgzSGOkB7gRj7WVdJ5R4AaABAg)
<br>
就像这样： &darr;
![post](https://s1.ax1x.com/2020/09/09/wlxNqA.png)
我想利用评论的数据来看看人们最喜欢**No.6 Collaboration Project**的哪首歌
说干就干！！！！
<!--more-->
原本想用Scrapy来爬取YouTube页面，但是感觉Google Developer API好麻烦，而且我对Scrapy还不是很熟练，于是决定有Selenium动态操作YouTube的页面，直接获取评论内容

遇到问题：
1. YouTube评论列表是动态更新的，需要不断地来向下拖动滚动条
	**可以直接利用Selenium能够解析运行JavaScript的功能对滚动条进行滑动**
2. YouTube最多显示1001条评论
	**无语(ˉ▽ˉ；)...**
<br>


代码如下：&darr;

```python
import time
from selenium import webdriver
from wordcloud import WordCloud,ImageColorGenerator
from PIL import Image
import matplotlib.pyplot as plt

#设定专辑内容，初始化歌曲提及频率
songs=["beautiful people","remember the name","put it all on me","antisocial","blow","way to break my heart","feels","nothing on you","best part of me","i don't care","south of the border","cross me","1000 nights","take me back to london","i don't want your money"]
songs_frequency=[0,0,0,0,0,0,0,0,0,0,0,0,0,0,0]
count1=0 #是否写入评论数
count2=0 #记录当前写入评论数
count3=0 #每循环10次输出一次时间

#提前为selenium中要用到的JavaScript代码初始化值
now_height=0
pre_height=0

#创建浏览器驱动
wd=webdriver.Chrome()
url="https://www.youtube.com/post/UgxSXlrxP5BQG0l5IZR4AaABCQ?lc=UgzSGOkB7gRj7WVdJ5R4AaABAg"
wd.get(url)

#YouTube上Selenium先滚动页面后提取内容
while True:
    try:
        #不断拖拉滚动条
        wd.execute_script("scrollBy(0,100000)")
        time.sleep(1)
        if count3%20==0:
            print("count:"+str(count3))
            now_height=wd.execute_script("return document.documentElement.scrollHeight;")
            if now_height==pre_height:
                break
            pre_height=now_height
        count3+=1
    except Exception as e:
        print(e)

#Selenium查找内容
comment=wd.find_elements_by_id("content-text")
comments=[com.text for com in comment]

for m in range(len(songs)):
    for i in range(len(comments)):
        if comments[i].lower().find(songs[m])!=-1:
            songs_frequency[m]+=1
            
#单纯为了美观~~~
songs_capital=[m.capitalize() for m in songs]

#形成字典
songs_frequency_dict=dict(zip(songs_capital,songs_frequency))

#画词云函数
def draw_cloud(dic):
    image=Image.open('project.jpg')

    wc=WordCloud(scale=4,font_path='simkai.ttf',background_color='white',max_font_size=60)
    wc.generate_from_frequencies(dic)
    plt.imshow(wc)
    plt.axis("off")
    plt.savefig("NO6.jpg",dpi=my_dpi)
    plt.show()
    

draw_cloud(songs_frequency_dict)
```

最后的词云就是这样啦：
<br>
![wordcloud](https://s1.ax1x.com/2020/09/09/wlvyH1.png)
<br>
(但是感觉分辨率还是不太好，emmmm，后面继续更新~~~)
