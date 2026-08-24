# xiaozhou-mi
![ 刷步数](https://github.com/zhoudedi/xiaozhou-mi/actions/workflows/run.yml/badge.svg)
[![GitHub forks](https://img.shields.io/github/forks/zhoudedi/xiaozhou-mi?style=flat-square)](https://github.com/zhoudedi/xiaozhou-mi/network)
[![GitHub stars](https://img.shields.io/github/stars/zhoudedi/xiaozhou-mi?style=flat-square)](https://github.com/zhoudedi/xiaozhou-mi/stargazers)
[![GitHub issues](https://img.shields.io/github/issues/zhoudedi/xiaozhou-mi?style=flat-square)](https://github.com/zhoudedi/xiaozhou-mi/issues)

# 小米运动zepp life（原小米运动） APP自动刷步数

> zepp life（原小米运动） app自动刷步数

## Github Actions 部署指南

### 一、Fork 此仓库
![](https://cdn.jsdelivr.net/gh/wes-lin/Cloud189Checkin/image/fork.png)
### 二、设置账号密码
# 20260508修改新增
添加名为  **CONFIG**的变量: Settings-->Secrets-->New secret ,使用下面json模板配置多账户，支持邮箱,手机号
```
{
  "TG_BOT_TOKEN": "telegram TG_BOT_TOKEN，如果没有，请留空",
  "TG_USER_ID": "telegram TG_USER_ID，如果没有，请留空",
  "SKEY": "酷推skey，如果没有，请留空",
  "SCKEY": "server酱sckey，如果没有，请留空",
  "POSITION": "是否开启企业微信推送，如果没有，请留空",
  "CORPID": "企业ID， 登陆企业微信，在我的企业-->企业信息里查看，如果没有，请留空",
  "CORPSECRET": "企业微信自建自建应用，每个自建应用里都有单独的secret，如果没有，请留空",
  "AGENTID": "填写你的企业微信自建应用ID，不加引号，是个整型常数,就是AgentId，如果没有，请留空",
  "TOUSER": "指定接收消息的成员，成员ID列表（多个接收者用“;”分隔，最多支持1000个）。特殊情况：指定为”@all”，则向该企业应用的全部成员发送如果没有，请留空",
  "TOPARTY": "指定接收消息的部门，部门ID列表，多个接收者用“;”分隔，最多支持100个。当touser为”@all”时填写”@all”，如果没有，请留空",
  "TOTAG": "指定接收消息的标签，标签ID列表，多个接收者用“;”分隔，最多支持100个。当touser为”@all”时填写”@all”，如果没有，请留空",
  "OPEN_GET_WEATHER": "开启根据地区天气情况降低步数，如果没有，请留空",
  "AREA": "设置获取天气的地区（上面开启后必填）如 北京 ，如果没有，请留空",
  "QWEATHER": "此处填写和风天气 Private KEY，申请地址https://console.qweather.com/#/apps，如果没有，请留空",
  "MIMOTION": [
    {
      "max_step": "25000",
      "min_step": "20000",
      "password": "Sitoi",
      "user": "18888xxxxxx"
    },
    {
      "max_step": "多账号 最大步数填写，请参考上面",
      "min_step": "多账号 最小步数填写，请参考上面",
      "password": "多账号 密码填写，请参考上面",
      "user": "多账号 手机号填写，请参考上面"
    }
  ]
}
```
> 添加名为  **PAT** 的变量: Settings-->Secrets-->New secret

| Secrets |  格式  |
| -------- | ----- |
| PAT |   此处**PAT**需要申请，值为申请到的github token秘钥，申请秘钥教程：点击右上角 GitHub 用户设置页面 最下方的 Developer setting ，然后选择 Personal access tokens 来生成一个 token，由于我们只需要能够对普通仓库 push 就行了，所以把 repo 部分勾上即可。需要repo和workflow权限,此项必填，避免git push的权限错误。如图：![](https://github.com/zhoudedi/xiaozhou-mi/blob/main/tp.png) |

**CONFIG**示例如下:
```
{
  "TG_BOT_TOKEN": "",
  "TG_USER_ID": "",
  "SKEY": "",
  "SCKEY": "",
  "POSITION": "",
  "CORPID": "",
  "CORPSECRET": "",
  "AGENTID": "",
  "TOUSER": "",
  "TOPARTY": "",
  "TOTAG": "",
  "OPEN_GET_WEATHER": "",
  "AREA": "",
  "QWEATHER": "",
  "MIMOTION": [
    {
      "max_step": "25000",
      "min_step": "20000",
      "password": "账号1的密码",
      "user": "111111xxx账号1"
    },
    {
      "max_step": "30000",
      "min_step": "25000",
      "password": "账号2的密码",
      "user": "122222xxx账号2"
    },
    {
      "max_step": "多账号 最大步数填写，请参考上面",
      "min_step": "多账号 最小步数填写，请参考上面",
      "password": "多账号 密码填写，请参考上面",
      "user": "多账号 手机号填写，请参考上面"
    }
  ]
}
```

### 三、自定义启动时间

编辑 **random_cron.sh**
修改其中**if**语句的判断时间为UTC时间，即**北京时间-8**，如北京时间8点为UTC时间0点，需要运行的时间-8就是UTC时间



## 注意事项

1. 每天运行七次，由random_cron.sh控制，分钟为随机值

2. 多账户的数量和密码请一定要对上 不然无法使用!!!

3. 启动时间得是UTC时间!

4. server酱注册地址 [点我](https://sct.ftqq.com/)

5. 如果支付宝没有更新步数,到小米运动->设置->账号->注销账号->清空数据,然后重新登录,重新绑定第三方

6. 小米运动不会更新步数，只有关联的会同步！！！！！

7. 请各位在使用时Fork[主分支](https://github.com/zhoudedi/xiaozhou-mi/)，防止出现不必要的bug.

8. 请注意，账号不是 [小米账号]，而是 [小米运动] 的账号。

## 历史Star数 

1.从应用商店下载 zepp life（原小米运动） app，打开软件并选择----没有账号？立即注册

注：一定要在app中新注册zepp life账号。

 
<img width="442" height="722" alt="image" src="https://github.com/user-attachments/assets/11307d8d-256d-4081-a028-95ab139a3d21" />

 

2.注册之后，登录zepp life APP，在App首页，点击‘我的’->‘第三方接入’，绑定你需要 刷步的项目支付宝、微信、QQ等

<img width="460" height="330" alt="image" src="https://github.com/user-attachments/assets/4e2b454a-a03f-4492-9881-794c8f0de1f3" />


 

3.浏览器打开刷步网：http://xm.135top.com/

输入（zepp life）账号和密码，点击登录。

 

 

 

4.输入所需要的步数，点击提交即可同步。

注：刷步可能存在延时，刷后等待十分钟左右再查看同步情况。

若微信未同步请取消“amazfit华米”公众号关注，重新到zepp life app中绑定微信。

