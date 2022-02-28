---
title: 阿里云oss静态页面与邮箱dns配置
date: 2021-02-07
tags: ['javascript']
---

1.  域名服务器需要设置为阿里云默认 dns 服务器，
2.  在 oss bucket 基础设置中设置首页和 404 页
3.  为邮箱和静态页面添加域名解析记录：
    <table>
        <tr>
            <td>主机记录</td>
            <td>记录类型</td>
            <td>解析线路</td>
            <td>记录值</td>
            <td>TTL</td>
        </tr>
        <tr>
            <td>@</td>
            <td>CNAME</td>
            <td>默认</td>
            <td>Bucket地址，如 xxx.oss-cn-xxx.aliyuncs.com</td>
            <td>10分钟</td>
            <td></td>
        </tr>
        <tr>
            <td>mail</td>
            <td>CNAME</td>
            <td>默认</td>
            <td>邮箱服务器,如 mail.mxhichina.com</td>
            <td>10分钟</td>
            <td></td>
        </tr>
        <tr>
            <td>smtp</td>
            <td>CNAME</td>
            <td>默认</td>
            <td>对应smtp, smtp.mxhichina.com</td>
            <td>10分钟</td>
            <td></td>
        </tr>
        <tr>
            <td>pop3</td>
            <td>CNAME</td>
            <td>默认</td>
            <td>对应pop3, pop3.mxhichina.com</td>
            <td>10分钟</td>
            <td></td>
        </tr>
        <tr>
            <td>@</td>
            <td>MX</td>
            <td>默认</td>
            <td>对应优先MX, mxn.mxhichina.com | 5 (mx优先级)</td>
            <td>10分钟</td>
        </tr>
        <tr>
            <td>@</td>
            <td>MX</td>
            <td>默认</td>
            <td>对应MX, mxw.mxhichina.com | 10 (mx优先级)</td>
            <td>10分钟</td>
        </tr>
    </table>

        MX优先级，用来指定邮件服务器接收邮件的先后顺序，数值越小优先级越高。

        当DNS服务器的解析记录中只有一条MX记录时，MX优先级没有意义。
        当DNS服务器的解析记录中存在多条MX记录时，邮件发送方的DNS服务器会优先把邮件投递到MX优先级高的邮件服务器。
        如果该服务器故障无法接收邮件，邮件发送方的DNS服务器会自动选择下一优先级的邮件服务器投递邮件。

### 参考资料:

- [MX 优先级有什么意义？](https://support.huaweicloud.com/dns_faq/dns_faq_014.html)
