### 下载步骤
```
pip install playwright
```
成功下载playwright后，执行下面的命令以成功安装驱动
```
playwright install
```
这之后就可以进行代码的编写了

### 使用playwright获取登录用户哔哩哔哩所有视频的BV号
```python
from playwright.sync_api import sync_playwright
from time import sleep
import re
# cookie = [{}] # 设置cookie，从all_cookies 处获取
path = "https://space.bilibili.com/1804321873/video"
video_prefix = "https://www.bilibili.com/video/" # 后面跟着BV号

BV_lists = []

def getBV_number():
    """根据用户的cookie登陆后，到个人页面下获取每一个的视频的链接，从链接中提取出来BV号
    """
    with sync_playwright() as p:
        browser_type = p.chromium
        browser = browser_type.launch(headless=False) # 设置浏览器可见
        context = browser.new_context() # 新建上下文
        
        context.add_cookies(cookies=cookies) # 加载cookie
        # all_cookies = context.cookies() # 获取登录后用户的cookie
        # print(all_cookies)
        page = context.new_page() # 新建tab页
        page.goto('https://www.bilibili.com')
        page.reload()
        page.goto(path)
        # sleep(30)
        sleep(3)
        eles = page.query_selector_all(".list-list>li>a") # 定位多个元素
        for i in eles:
            link = i.get_attribute("href") # 获取到链接
            target = link.split("/")[-2]
            BV_lists.append(target)
        while next_page_button:=page.query_selector("#submit-video-list > ul.be-pager > li.be-pager-next"):
            if not next_page_button.is_visible(): # 如果页面中没有该元素，则结束
                break
            next_page_button.click()
            sleep(3)
            eles = page.query_selector_all(".list-list>li>a") # 定位多个元素
            for i in eles:
                url = i.get_attribute("href") # 获取到链接
                BV_lists.append(url.split("/")[-2])

        print(BV_lists)
        page.close()
        context.close()
        browser.close()
        
getBV_number()
```

