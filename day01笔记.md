# p11 总结

## day1

#### 1.本地上传到远程库

- 1-1. git 密钥
- 1-2. touch 创建一个文件
- 1-3. git add .
- 1-4. git status 类似于；查看是否创建成功
- 1-5. git commit -m "写上传文件的备注"
- 1-6. git push 上传到远程库

## 2.背诵

1. 本地版本控制
   - 优点: 本地保存代码,方便个人操作,个人保管代码
   - 缺点: 一旦本地机器销毁,代码将会丢失
2. 集中版本控制 svn
   - 优点: 所有的东西都放在服务器上,本地内存占用少,安全性高
   - 缺点: 一旦中央服务器崩溃,代码将不存在和丢失
3. 分布式版本控制 git
   - 优点: 每个人都是单独的一个服务器,所有的人都拥有完整代码历史记录,不管服务器怎么崩,代码始终都能找回
   - 缺点: 本地占用量高,安全性比较弱


### 3. 本地创建仓库并关联至远程

1. 执行

   ```
   git init
   ```

2. 新建README.md文件

   ```
   touch README.md
   ```

3. 执行以下命令

   ```
   git add .
   git status // 查看暂存区是否有代码储存
   git commit -m '新增了一个md文档'
   git remote add origin https://github.com/threeSunlight/demo3.git
   git push -u origin main
   ```

方法二: 本地仓库关联线上仓库

第一步: 从线上仓库赋值ssh路径

第二步: 将线上仓库克隆至本地

```
1. git clone git@github.com:threeSunlight/2301C.git(复制来的地址)
2. 进入到克隆后的文件夹路径下
3. 把代码放进去
4. git add .
5. git status // 查看暂存区是否有代码储存
6. git commit -m '描述这块代码的作用'
7. git push 
```



###  总结: 本地仓库关联远程仓库方法

1. 直接clone远段仓库到本地

   ```
   1. 现在github上新建仓库
   2. 选择自己喜欢的盘符,执行git clone xxxx(远端git地址)   ---------这个时候已经建立联系
   3. cd 进入克隆的文件夹,开始编写代码
   4. 上传
   		git add .
   		git status
   		git commit -m ''
   		git status
   		git push
   ```

   

3. 本地初始化仓库,和远端建立联系

   ```
   1. 在github新建一个仓库
   2. 在本地新建一个文件夹,执行git init 方法,初始化本地仓库
   3. 在本地文件夹新建文件,编写代码
   4. git add . 将本地代码提交至暂存区
   5. git status
   6. git commit -m ''
   7. git status
   8. git branch -M master/main(分支名)     ----具体看仓库分支叫法
   9. git remote add origin git@github.com:threeSunlight/2301C--.git   跟远端建立联系
   10. git push -u origin master  上传代码
   ```
