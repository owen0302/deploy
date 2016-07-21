#!/usr/bin/env python
# coding=utf-8

import dns.resolver
import os
import httplib

iplist=[]                     #定义域名IP列表变量
appdomain="www.whalemove.com" #定义业务域名

def get_iplist(domain=""):    #域名解析函数，解析成功IP将被追加到iplist
    try:
       A = dns.resolver.query(domain, 'A')
    except Exception,e:
       print "dns resolver error:"+str(e)
       return
    for i in A.response.answer:
       for j in i.items:
           iplist.append(j.address)        #追加到iplist
    return True

def checkip(ip):
    checkurl=ip+":80"
    getcontent=""
    httplib.socket.setdefaulttimeout(5)    #定义Http连接超时时间（5秒）
    conn=httplib.HTTPConnetion(checkurl)   #创建http连接对象

    try:
       conn.request("GET", "/",headers = {"Host": appdomain})  #发起URL请求，添加host主机头

       r=conn.getresponse()
       getcontent = r.read(15)             #获取URL页面前15个字符，以便做可用性校验
    finally:
       if getconntent=="<!doctype html>":  #监控URL页的内容以便是实现定义好的，比如"http200"等
           print ip+" [ok]"
       else:
           print ip+" [ERROR]"             #此处可放告警程序，可以邮件，也可以是短信通知

if_name_=="_main_"
   if get_iplist(appdomain) and len(iplist)>0:    #条件：域名解析正确且至少返回一个IP
           for ip in iplist:
               checkip(ip)
   else
          print "dns resolver error."



#####add branch integration





Creating a new branch is quick AND simple
