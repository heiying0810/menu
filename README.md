**首页导航应用**

------

> 使用Django开发,可以使用后台管理具体导航内容。数据库支持MySQL和文件数据库，部署方式适配了docker和k8s。

![image-20220526165029791](C:\Users\heiying\AppData\Roaming\Typora\typora-user-images\image-20220526165029791.png)

# 一、功能说明

1. 自定义修改业务版块

   ![image-20220526164623693](C:\Users\heiying\AppData\Roaming\Typora\typora-user-images\image-20220526164623693.png)

2. 自定义修改具体每个业务版块的不同环境

   ![image-20220526164651697](C:\Users\heiying\AppData\Roaming\Typora\typora-user-images\image-20220526164651697.png)

3. 支持按具体某个业务版块的某个环境检索

   ![image-20220526165202711](C:\Users\heiying\AppData\Roaming\Typora\typora-user-images\image-20220526165202711.png)

4. 支持通过搜索框检索(需要APP名称中有检索内容)

   ![image-20220526165256826](C:\Users\heiying\AppData\Roaming\Typora\typora-user-images\image-20220526165256826.png)

5. 支持后台管理导航列表内容

   ![image-20220526165443991](C:\Users\heiying\AppData\Roaming\Typora\typora-user-images\image-20220526165443991.png)

6. 新增导航内容

   ![image-20220526165658609](C:\Users\heiying\AppData\Roaming\Typora\typora-user-images\image-20220526165658609.png)

7. 支持用户管理

   > 01.用户管理使用的是Django的用户管理功能
   >
   > 02.默认管理员账号信息 admin/123456

8. 404页面

   ![image-20220526170839563](C:\Users\heiying\AppData\Roaming\Typora\typora-user-images\image-20220526170839563.png)

# 二、部署

## 2.1、修改配置文件

1. 选择数据库

   `注意`：默认使用文件数据库可以不做修改

   ```
   vim settings.py
   ```

   

2. 编辑业务线结构

   ```
   vim settings.py
   COMPANY = [
       ("0", "业务版块01"),
       ("1", "业务版块02"),
   ]
   COMPANY_ENV = [
       ("pro", "PRO生产环境"),
       ("fat", "FAT测试环境"),
       ("uat", "UAT演示环境"),
   ]
   ```

   

## 2.1、使用docker部署

```
## 01.使用docker启动Django后台
docker run --name menu --restart=always -d -p 8000:8000 -v /home/settings.py:/home/menu/menu/settings.py menu:v1
## 02.使用nginx代理,并处理静态文件
vim nginx.conf
	proxy_pass http://127.0.0.1:8000;	//按实际修改docker的代理地址
	root /home/nginx/menu/;				//按实际修改静态文件路径
```

## 2.2、使用K8S部署

```
## 
```


