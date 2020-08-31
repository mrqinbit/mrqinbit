### 下载与安装
1. 在官网下载Nexus Repository Manager OSS 3.x, 解压至任意位置.
2. 管理员运行 powershell, 切换到 nexus-3.x/bin 目录

```
    $ nexus.exe /install 进行安装, 成功后会提示 Installed service 'nexus

    $ nexus.exe /run 运行服务, 第一次要耐心等待很久
```
### 说明文档
- [仓储配置](https://help.sonatype.com/repomanager3/configuration/repository-management)
- [权限配置](https://help.sonatype.com/repomanager3/security)
### 添加npm仓库
- 创建npm代理
- 创建本地npm
- 创建npm组
### 配置与验证npm仓库
- 查看并设置nodejs的默认仓库地址
```
npm config get registry  #http://registry.npmjs.org/
npm config set registry http://localhost:8081/repository/npm-group/
```
- 设置完成后，可以找到当前用户目录下的.npmrc文件
### 发布包到私服
1. 添加权限认证
设置权限, Realms 菜单, 将 npm Bearer Token Realm 添加到右边

2. 创建nx-deploy角色
给角色赋于一个nx-repository-view-*-*-*权限

3. 创建deployer 用户,密码也为 XXX,同时设定角色为nx-deploy

4. 客户端的.npmrc配置

```
registry=http://127.0.0.1:8081/repository/npm-group/
email=deployer@example.com
always-auth=true
_auth="ZGVwbG95ZXI6ZGVwbG95ZXI="
```
5. 发布控件到npm私服中
在package.json 配置
```
"publishConfig" : {
    "registry" : "http://localhost:8081/repository/npm-hosted/"
  }
```
在包根目录执行npm publish即可。

==注意：发布是npm-hosted，不是npm-group.==
### 相关文档：

- [nexus3配置](https://www.jianshu.com/p/9085f47726a2)
- [nexus3配置](https://help.sonatype.com/repomanager3/configuration)
- [包发布配置](https://levelup.gitconnected.com/deploying-private-npm-packages-to-nexus-a16722cc8166)
- [包发布配置](https://help.sonatype.com/repomanager3/formats/npm-registry#NpmRegistry-PublishingnpmPackages)
