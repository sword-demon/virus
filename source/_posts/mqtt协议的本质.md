---
title: mqtt协议的本质
date: 2025-02-06 11:00:00
tags: [MQTT]
categories: [MQTT]
---

## 发布/订阅模式的优点

1. 适合于网络稳定性不好的场景
2. 便于数据实时更新
3. MQTT 协议需要客户端 Client 和消息代理服务器 Broker 通信完成
4. MQTT 传输的消息分为 2 部分：主题 Topic 和消息内容 Payload
5. MQTT 消息传递模式：发布/订阅

## 和 TCP 的关系

1. MQTT 协议是基于 TCP/IP 协议之上
2. MQTT 消息传输时基于 TCP 长连接

<img src="/images/mqtt.png" alt="mqtt" />
