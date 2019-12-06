# BitPayX 




## 添加流程
如果发现添加错误，例如充值页面显示Slim Application Error，请严格按照这几部操作。

 1. 在添加任何东西之前，确保你的用户充值页面可以访问。（如果安全起见，可以备份代码）。
 2. 新增2个文件（BitPayX.php， bitpayx.tpl），请放入一模一样的位置。确保你的用户充值页面可以访问。
 3. Payment.php 修改3行代码。修改完后，确保你的用户充值页面可以访问。注意大小写，是BitPayX，不是BitpayX。
 4. .config.php 里面的参数 payment_system 设置为 bitpayx。确保你的用户充值页面可以访问。
 5. 付款，然后完成整个流程。

其中任意一步失败，请回退上一步，并且联系管理人员，并且告知第几步失败了。


## 获取授权(如果Bitpay操作过，请忽略)

 1. 先跟管理员获取邀请码
 2. 注册登录[商家后台](https://merchants.mugglepay.com)
 3. 选择"个人设置"->“API认证”->“用在后台服务器”，点击“添加密钥”，获得后端认证码（请注意，是”后端“）。
<img src="https://cdn.mugglepay.com/docs/whmcs/getapi.png" />


## 认证审核
 请去个人设置中，完成认证工作，点亮笑脸☺。<br />
 <img width="300" src="https://user-images.githubusercontent.com/50819254/59549161-21656f80-8f8c-11e9-8127-3b369ab85b4f.jpg" />
 
 
请确认您已经开通了需要的权限。
注意，如果你只有 “加密货币”，那只能接受加密货币。如需要开通其他支付方式，请按照该页面的流程操作。

<img src="https://cdn.mugglepay.com/docs/whmcs/permission.png" />

 
## 文件修改

需要新增2个文件，请放入一模一样的位置。
  *  app/Services/Gateway/BitPayX.php
  *  resources/views/material/user/bitpayx.tpl
  
  下载链接：
  https://raw.githubusercontent.com/bitpaydev/bitpayx/master/bitpayx/app/Services/Gateway/BitPayX.php
  https://raw.githubusercontent.com/bitpaydev/bitpayx/master/bitpayx/resources/views/material/user/bitpayx.tpl

需要修改2个配置文件。数字货币Bitpay与其他支付兼容。

 * config/.config.php

```
# 修改： config/.config.php
#取值 none | codepay |  bitpayx

$System_Config['payment_system']='bitpayx';

#请注意bitpay_secret 这个参数可能已经在config中，注意添加不要重复覆盖。
$System_Config['bitpay_secret']='XXXX';

```
  * app/Services/Payment.php 
  
```
# 新增BitPayX相关的3行改动。
    use App\Services\Gateway\{
        AopF2F, Codepay, DoiAMPay, PaymentWall, ChenPay, SPay, TrimePay, BitPayX
    };

    public static function getClient()
    {
        $method = Config::get('payment_system');
        switch ($method) {
            case ('bitpayx'):
                return new BitPayX(Config::get('bitpay_secret'));
            default:
                return null;
        }
    }

```
效果如下
<img src="https://cdn.mugglepay.com/docs/pics/payment-demo.jpg" />




