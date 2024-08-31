---
description: 桌游电子设备的总体方案，包括了各个模块的实现，系统的通讯实现等
coverY: 0
---

# 总体方案

方案的独立模块总共需要包括如下的几个模块：

* 电磁铁或类似电磁铁模块，用于执行机构动作
* NFC模块用于读取卡片的信息
* 主控与通讯总线，用于连接所有的执行机构、卡片等

其中，电磁铁与NFC的模块，作为一个单独的模块，主控模块为一个模块，所以从实物上来说，总共有3种：

1. 卡（NFC的卡）
2. 棋盘块（NFC，电磁铁，以及控制单片机）
3. 主控模块（Auduino或者树莓派）

***

## 1. 控制总线

首先需要确定控制总线的形式，即，主控模块与棋盘块（20个至40个之间，用什么连接）。 成本永远是需要最先考虑的，所以可以用有线连接的情况下，用有线的方式一定是最经济的，无线芯片总是比有线更贵（因为有线直接用导线就把主控模块和被控制模块连接好了，而无线模块则需要额外的芯片来进行连接）。所以可以考虑如下的连接方式：

* RS232/RS485总线&#x20;
* 网线
* CAN总线

RS485总线通常会更便宜一些，所以此处我们选选用rs485总线作为控制总线，总计需要约50～100元。

{% embed url="https://item.taobao.com/item.htm?abbucket=2&id=642084183666&ns=1&pisk=fc0sht_cbx3eTCRpGtdUA4p1GxzfnxTPCsNxZjQNMPUTHDGohRRDjPoQhvHQBNRMjoejIPEmb-yahrGmFBJyzUlisr4wUL8PiwmZMzbYMlB49MFujpRFLUlis-f1HQopziwzMIIAD-HYJkF8grBY6NdQv7PYkNEAWMBLKJeYkoeY9WF86-FTDodCv7V4HteYX6eLN7SYkrHYJXFm_RtgTswn1BH9u8iO7KezdZQ5t0q9ujSVci_L6lebp9bcoIV_f8hTKL-MysqjClge5TVsvbMa1xYlSPEjX0UtlLT_JbmEBWMvFiwKVV0b4V95qR3gnYatApQ_kP3s4u4XV1VE5X3ucVv1JRMn90ziypbjeXlrSk0XF9emb74L1DOAvREA4y7zFgn5c6ZllWwyOBscmHwxIppm_u9zXWVFMBOC4NqTtWO6OBscmlF3ToOBOg7G.&priceTId=2100c80117251173385223357e0c57&skuId=5088333281958&spm=a21n57.1.item.55.2db3523c9dPu2A&utparam={%22aplus_abtest%22:%22bd04b19aabd072a3c932e47f766432c6%22}" %}
树莓派的UART转RS485模块，50元
{% endembed %}

NFC模块本身支持SPI、IIC、UART。

电磁铁需要配合uart继电器才可以使用

{% embed url="https://item.taobao.com/item.htm?abbucket=2&id=614212294667&ns=1&pisk=fFuqhTiKTPD5tjD3-SUaavmI5PzA-Pkwdtu_s5ct6120o-izsAMJ6IUjsRkZF8QjcnE_Q1zxPm__hKUZsvawdpTBRjhYuPvBd1dmcR439SXGCRclZofJNUTBRjhPGSAIZeOTdTDzTGbiIo2lrSwuiRVgiQruO54GolbcqT28ER4gjRVuZWV0ISqgjQSu1WVgilqMr7VUOt4gSAco9JZQbpP_mBSGJKb2bFLaLj2P8XBuMovjHG6V33F0mJwkda_W6Sr4Kj2JdnLh6lk404TVpSooTxNqBeQYolomxr0wLEzo90M0aAvFb8mEkVrIupSLnqetLrmyEZzgoqoQvP-FM7gqZ2EZkK7u3YhoAr3HeNknNXgY2VJFERnb9zVq4CjunljPLOFoxp3t0Ojam7FzdQRrA10WTRC-w-sOXoB4aJOmjGITmdVzdQRPXGEYo7yBicf..&priceTId=215040f217251183055548462e1edd&skuId=4671730372726&spm=a21n57.1.item.192.2db3523c9dPu2A&utparam={%22aplus_abtest%22:%22306042c92dc09319e095be5583f6f36d%22}" %}
485继电器
{% endembed %}
