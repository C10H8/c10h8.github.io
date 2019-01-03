---
title: Thrift简介
date: 2017-09-02 21:06:41
categories: Java
tags: [RPC,thrift]
---

- - -
<!--more-->
Thrift简介
---

# 简介
Thrift提供了一种服务调用方式，由facebook开发，它的主要特点是次啊用接口描述语言定义并创建服务，支持可扩展的跨语言服务开发。
Thrift可以根据描述的服务接口生成多种语言，如C++，java，Python等等。与基于xml，json等消息格式的服务相比，其传输体积更小，
对于高并发，大数据量和异构的系统更有优势。Thrift包含一个完整的堆栈结构用语构建客户端和服务端，整体架构如下：

# thrift 接口的两种实现方法

## IDL
> 接口定义语言((interface definition language))，用于跨语言的RPC服务接口的定义

### 基本类型
  * bool，布尔型，1个字节；
  * byte，有符号单字节；
  * i16，有符号16位整型；
  * i32，有符号32位整型；
  * i64，有符号64位整型；
  * double，64位浮点数；
  * string，字符串；
  * binary，字节数组；

### 容器
  * map<t1,t2>，字典；
  * list，列表；
  * set，集合；
  
### 代码
* 结构定义

```thrift
struct CommonResponse{
  1:optional i32 status,       #状态码  0:成功  1:失败
  2:optional string errorCode, #错误码
  3:optional string errorMsg   #错误信息
}

struct OrderSearchDTO {
  1: required i32 siteId;
  2: optional list<i32> statusList;
  3: optional bool isFlagshipOrder;
  4: optional bool exOrderIdNotNull;
  5: optional string originalFlightOrderId;
}
```

* 服务接口定义
```thrift
namespace java com.xxx.flight.orderplatform.sdk.api.outer.plat.v1

include "MerchantOrderEntity.thrift"

service MerchantOrderOperate {
 
  // 异步生单
  CommonResponse updateOrderInfo4AsyncOrder(1: OrderSearchDTO orderSerchDTO);
}
```




## thrift注解
Java注解：
 * @ThriftService
 * @ThriftStruct
 * @ThriftField
 * @ThriftEnumValue
 * @ThriftMethod
 * @ThriftConstructor
 * @ThriftField

# 代码
* 结构定义
```thrift
@ThriftStruct
public class NotifyPaidReqThriftVo extend xxx {
    private String paymentNo;
    private String paymentSeq;
    private String payType;
    private int payAmount;
    private String payTime;

    @Override
    public String paramValidateSelfDefined() {
        return null;
    }

    @ThriftField(21)
    public String getPaymentNo() {
        return paymentNo;
    }

    @ThriftField
    public void setPaymentNo(String paymentNo) {
        this.paymentNo = paymentNo;
    }

    @ThriftField(22)
    public String getPaymentSeq() {
        return paymentSeq;
    }

    @ThriftField
    public void setPaymentSeq(String paymentSeq) {
        this.paymentSeq = paymentSeq;
    }

    @ThriftField(23)
    public String getPayType() {
        return payType;
    }

    @ThriftField
    public void setPayType(String payType) {
        this.payType = payType;
    }

    @ThriftField(24)
    public int getPayAmount() {
        return payAmount;
    }

    @ThriftField
    public void setPayAmount(int payAmount) {
        this.payAmount = payAmount;
    }

    @ThriftField(25)
    public String getPayTime() {
        return payTime;
    }

    @ThriftField
    public void setPayTime(String payTime) {
        this.payTime = payTime;
    }
}
```

* 接口

```thrift
@ThriftService
public interface FlagshipPayService {
    @ThriftMethod
    NotifyPaidResThriftVo notifyPaid(NotifyPaidReqThriftVo notifyPaidReqThriftVo);
}
```

# 总结
 本文只是对thrift进行简单的理解，从IDL和注解的两种方式使用thrift。并没有详细的介绍thrift的原理。后面理解深入了，补上。

# 参考：
(1)[thrift 的原理和使用](http://www.cnblogs.com/chenny7/p/4224720.html)
(2)[Thrift: The Missing Guide](http://diwakergupta.github.io/thrift-missing-guide/)


