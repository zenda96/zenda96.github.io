---
layout: display
title:  "利用pytthon获取qq群成员的QQ号码等相关信息"
categories: python
digest: "只能爬取扫描登陆的人所加入的QQ群组"
---
<h2>{{ page.title }}</h2>
<p>{{ page.date | date_to_string }}</p>

最近应朋友需求 把朋友加入的所有QQ群群成员的号码给爬取下来 大概实现原理先用 selenium 模拟QQ登陆 然后模拟下拉加载全部的数据 然后保存到 txt 文件中 最后用 BeautifulSoup 解析保存下来的网页源代码 清洗成需要的格式 保存到xls中  
代码如下:  
{% highlight python %}

    import os
    import time
    import math
    from selenium import webdriver
    from selenium.webdriver.support.ui import WebDriverWait
    from selenium.webdriver.support import expected_conditions as EC
    from selenium.webdriver.common.by import By
    from bs4 import BeautifulSoup
    import re
    from xlwt import Workbook

    base = 'I:\\qqGroup\\'


    def init(totalGroups):
        driver = webdriver.Chrome()
        print("开始登录")
        #循环调用爬取
        for kk in range(len(totalGroups)):
            driver.get("https://qun.qq.com/member.html#gid=" + str(totalGroups[kk]))
            time.sleep(5)
            #手动刷新 防止上个页面缓存
            driver.refresh()
            wait = WebDriverWait(driver, 100)
            # 获取群员总数
            totals = wait.until(EC.element_to_be_clickable(
                (By.CSS_SELECTOR, "#groupMemberNum"))).text
            print(str(totalGroups[kk]) + '群总人数' + totals)
            #持续滚动到底部
            for page in range(math.ceil(int(totals)/21)):
                time.sleep(2)
                print('滚动第' + str(page)+'页')
                driver.execute_script("window.scrollTo(0,document.body.scrollHeight)")
            #获取网页源码
            res = driver.page_source
            #保存源码
            with open(base + 'html.txt', 'w', encoding='utf-8') as f:
                f.write(res)
            f.close()
            print('所有数据获取完毕,准备解析....')
            parser()
        # 关闭浏览器
        driver.quit()

    def parser():
        # 创建一个workbook 设置编码
        workbook = Workbook(encoding='utf-8')
        # 创建一个worksheet
        worksheet = workbook.add_sheet('群员统计')
        headers = ['角色', '昵称', '群名片', 'QQ', '性别', 'Q龄', '入群时间', '等级(积分)', '最后发言']
        for k in range(len(headers)):
                worksheet.write(0, k, headers[k])
        
        with open(base + 'html.txt', 'r', encoding='utf-8') as f:
            res = f.read()
        bs = BeautifulSoup(res, "lxml")
        trs = bs.find_all('tr', class_=re.compile(r'mb'))
        #群名称
        groupName = bs.find('span', id='groupTit').get_text(strip=True)
        #群成员数
        groupMemberNum = bs.find('span', id='groupMemberNum').get_text(strip=True)
        i = 0
        for tr in trs:
            i = i + 1
            tds = tr.find_all('td')
            #职位
            role = "群成员"
            master = tds[2].find('i', class_=re.compile(r'icon-group-master'))
            manager = tds[2].find('i', class_=re.compile(r'icon-group-manage'))
            if(master):
                role = ('群主')
            if(manager):
                role = ('管理员')
            nickName = tds[2].find('span').get_text(strip=True)  # 获取昵称
            card = tds[3].find('span').get_text(strip=True)  # 群名片
            QQ = tds[4].get_text(strip=True)  # QQ
            gender = tds[5].get_text(strip=True)  # 性别
            Qyear = tds[6].get_text(strip=True)  # Q龄
            joinGroupTime = tds[7].get_text(strip=True)  # 入群时间
            groupRank = tds[8].get_text(strip=True)  # 等级
            lastSpeak = tds[9].get_text(strip=True)  # 最后发言时间
            memberList = [role, nickName, card, QQ, gender,Qyear, joinGroupTime, groupRank, lastSpeak]
            # print(memberList)
            for j in range(len(memberList)):
                worksheet.write(i, j, memberList[j])
        # 保存excel
        workbook.save( base + groupName+'-'+groupMemberNum+'人.xls')
        print(groupName+'-'+groupMemberNum + '人保存成功')

    def main(number):
        #模拟登陆
        init(number)


    #参数为要爬取的QQ群号
    # main([808985336, 581829469, 631463323])
    # main([808895878, 631463323, 392972789, 193047134, 795851630])
    # main([808602642, 791970584, 780501079, 791617303, 704968368, 480333358, 451579727])
    main([809369396, 518486503, 773524292, 696665378,540536106, 781221268, 791970584, 823883693])

{% endhighlight %}
