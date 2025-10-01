---
layout: post
title: "React Start Path"
date: 2023-09-01 14:39:00
category: react
tags: [react]
---

https://stackoverflow.com/questions/40853235/tomcat-maven-how-to-add-the-static-pages-to-the-war-file
Put all your static files inside src/main/webapp and it should work like a charm.
To build your application, try running the command mvn clean install -U.
但是專案啟動時, index.html 會試著去讀取 /localhost/static/...
	有試著改 setupProxy.js 但是沒有用
https://escuela-tech.medium.com/how-to-deploy-reactjs-app-in-apache-tomcat-server-16a77e6b56e6
	教要在 package.json 加入參數   "homepage": "myJAXRS",
		Jersey2 專案反而能正常讓 index.html 載入 /myJAXRS/xxx.js
		但是在點了其它頁面時, URL 的專案名稱就消失了!!
	這時候如果是 範例的 Spring-Boot-ReactJS-Starter-master 佈署在 tomcat 後, index.html 有讀到, 但是會想去載入 /專案名/專案名/xxx.js
目前手動的方式是可行的! 佈署到測試機的 JAXRS 也用 postman 測試有讀到
先看看可不可以用 pom.xml 設定自動做這些複製的動作?
	pom automatic copy file to src/main/webapp
react path
	https://stackoverflow.com/questions/72240026/should-i-use-react-router-redirect-or-package-json-homepage-property-for-setti
	https://create-react-app.dev/docs/deployment/#building-for-relative-paths
		佈署的這章節可能還是需要看一下


[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


