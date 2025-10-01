---
layout: post
title: "Open Jdk6 Java Web Project in IDEA"
date: 2023-09-08 21:56:00
category: programming
tags: [idea]
---

## Download 2021.3.3 for Jdk6
Choose Version 2021.3.3 in the [Offical Download page](https://www.jetbrains.com/idea/download/other.html#2021.3).
![](https://hackmd.io/_uploads/rJ4kx1uR3.png)


## Setting SDK
1. Open Jdk6 project.  
2. Press Ctrl+Alt+Shift+S to open **Project Setting**:  
![](https://hackmd.io/_uploads/ry-dzJORn.png)
3. Use the `+` button to **Add SDK**:  
![](https://hackmd.io/_uploads/BkJifJ_0h.png)
4. Navigate to your jdk6 folder and Press `OK`:  
![](https://hackmd.io/_uploads/B1vyXydC2.png)
5. Choose project's **Language level** to **SDK default**:  
![](https://hackmd.io/_uploads/ByKIOt_C3.png)

## Install Tomcat6
1. Ensure **Tomcat and TomcatEE** plugin is installed.  
Press `Ctrl+Shift+A` and type in `Plugins` ↵ to open **Setting**.   
![](https://hackmd.io/_uploads/rkWizguR3.png)

2. Choose `Run` from menu bar, and click `Edit Configuration`  
![](https://hackmd.io/_uploads/SJ8Umx_R3.png)

3. Add new configuration from left upper `+` button, and click `Local` below `Tomcat Server`:  
![](https://hackmd.io/_uploads/SJJnmed0h.png)

4. Choose Tomcat6 folder like we did in NetBeans:  
![](https://hackmd.io/_uploads/BkhKNlOAn.png)

## Dependency
Add necessary libraries to the project configuration.  
1. Press `Ctrl`+`Alt`+`Shift`+`S` to open **Project Setting**.  
![](https://hackmd.io/_uploads/r1cwqKu0n.png)
2. Choose the library, and click `OK`.  
![](https://hackmd.io/_uploads/HymfjFO0h.png)
3. IDEA would popup to ask to set this library to the module.  Choose `OK`.  
![](https://hackmd.io/_uploads/HJw_iFOC3.png)
**library:**  
![](https://hackmd.io/_uploads/H1tSntu0n.png)


## Set the module
Before we deploy to Tomcat, we need to: **Add web module**.   
1. Press `Ctrl`+`Alt`+`Shift`+`S` to open **Project Setting**. 
2. Click `+` to add Web module in the **Mudules** Section:  
![](https://hackmd.io/_uploads/Hk0avOdR2.png)
And there would a warning:  
![](https://hackmd.io/_uploads/B1-UF__Rh.png)
By clicking the **Create Artificat**, IDEA would create **Facet** and **Artificat** for us.  
**Facet**:  
![](https://hackmd.io/_uploads/rJ4DJK_C3.png)
**Artifact**:  
![](https://hackmd.io/_uploads/rJxCn5uA2.jpg)
By clicking the `Fix` button, IDEA would popup to ask how to import the library:  
![](https://hackmd.io/_uploads/BkDv69_R2.png)
Choose **Add all missing dependencies...**:  
![](https://hackmd.io/_uploads/SJUAacd0n.png)


## Deploy to Tomcat
Click the menubar: **Run** -> **Edit Configuration**, and click **Deployment** tab in the configurations window:
![](https://hackmd.io/_uploads/SJHVWYuAn.png)
By clicking the **Artifact**, IDEA whould include the artifact which we just created.    
![](https://hackmd.io/_uploads/HJM3GKOR2.png)
Remember to erase the string: `_Web_exploded` in **Applcation context** field.


From now on, we could start tomcat with our project.  


## Packing war
1. Press `Ctrl`+`Alt`+`Shift`+`S` to open **Project Setting**.  
Adding **Web Application Archive**:  
![](https://hackmd.io/_uploads/BkdYdcuC2.png)
2. *PmbMgr:war* is the archive artifact:
![](https://hackmd.io/_uploads/S1uKQsOAh.png)
3. Menubar: **Build** -> **Build Artifacts...**:  
![](https://hackmd.io/_uploads/H1qbGoORn.png)
Choose **PmbMgr:web** -> **Build**:  
![](https://hackmd.io/_uploads/HyVdfiuR3.png)



## Hot Swap/Load
1. Menubar: **Run** -> **Edit Configuration**  
**On 'Update' action**: choose **Update classes and resources**
![](https://hackmd.io/_uploads/rJxnkou02.png)
2. Start tomcat in **DEBUG MODE**




[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

