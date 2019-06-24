# BitPayX 


如果需要[在线客服聊天](https://bitpay.dev) 以及 数字货币匿名支付[常见问题](https://github.com/bitpaydev/docs/blob/master/FAQ.md)。[技术交流群，或者获取邀请码](https://t.me/joinchat/GLKSKhUnE4GvEAPgqtChAQ)。

## 获取授权(如果Bitpay操作过，请忽略)

 1. 先跟管理员获取邀请码
 2. 注册登录[商家后台](https://merchants.mugglepay.com)
 3. 选择"个人设置"->“API认证”->“后台服务器”，获得后端认证码（请注意，是”后端“）。

## 认证审核
 请去个人设置中，完成认证工作，点亮笑脸☺。<br />
 <img width="300" src="https://user-images.githubusercontent.com/50819254/59549161-21656f80-8f8c-11e9-8127-3b369ab85b4f.jpg" />
 
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
#取值 none | codepay | trimepay | f2fpay | chenAlipay | paymentwall | spay |tomatopay | bitpayx

$System_Config['payment_system']='bitpayx';
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
