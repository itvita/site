---
title: uniapp消息推送unipush
categories:
  - uniapp
tags:
  - 消息推送
mp3: /music/RS02061L5yKV0IVVGv.mp3
cover: /img/224839-1656514119b359.jpg
date: 2022-10-09 19:53:41
---
### 官方步骤
> 具体参考官方流程开通，如果需要离线推送，则需要配置厂商通道。

[官方UniPush使用指南](https://ask.dcloud.net.cn/article/35622)

### 不说废话~直上代码。

#### uniapp前端
> app.vue onLaunch
``` javascript
    // #ifdef APP-PLUS
    /* 设置竖屏 */
		plus.screen.lockOrientation('portrait-primary');
    /* 清除角标 */
    plus.runtime.setBadgeNumber(0);
    // 监听接收透传消息事件,苹果为透传消息
		plus.push.addEventListener(
			'receive',
			function(msg) {
				let payload = {};
				if (msg.payload) {
					console.log('msg.payload', msg.payload);
					payload = JSON.parse(msg.payload);
					if (payload.t) {
						return;
					}
				}
				payload.t = true;
				plus.push.createMessage(msg.content, JSON.stringify(payload), {
					title: msg.title
				});
			},
			false
		);
   
    // #endif
```

>index.vue onLoad

```javascript
 // #ifdef APP-PLUS
 // 监听系统通知栏消息点击事件
		plus.push.addEventListener(
			'click',
			function(msg) {
				let payload = msg.payload;
				if (payload instanceof String) {
					payload = JSON.parse(payload);
				}
				/*跳转到对应页面*/
				uni.navigateTo({
					url: payload.url
				});
			},
			false
		);
      // #endif
```

>login.vue done

```javascript
// 推送cid
  const clientInfo = plus.push.getClientInfo();
  const clientid = clientInfo.clientid;
  /* 设备类型 */
  const brand = uni.getSystemInfoSync().brand;
  /* save */
  addOrUpdate({
    userId: userInfo.id,
    mobileBrand: brand,
    mobileCid: clientid
  });
```

>java
```java

package com.itvita.utils.push;

import com.alibaba.fastjson.JSONObject;
import com.getui.push.v2.sdk.ApiHelper;
import com.getui.push.v2.sdk.GtApiConfiguration;
import com.getui.push.v2.sdk.api.PushApi;
import com.getui.push.v2.sdk.common.ApiResult;
import com.getui.push.v2.sdk.dto.req.Audience;
import com.getui.push.v2.sdk.dto.req.Settings;
import com.getui.push.v2.sdk.dto.req.Strategy;
import com.getui.push.v2.sdk.dto.req.message.PushChannel;
import com.getui.push.v2.sdk.dto.req.message.PushDTO;
import com.getui.push.v2.sdk.dto.req.message.PushMessage;
import com.getui.push.v2.sdk.dto.req.message.android.AndroidDTO;
import com.getui.push.v2.sdk.dto.req.message.android.ThirdNotification;
import com.getui.push.v2.sdk.dto.req.message.android.Ups;
import com.getui.push.v2.sdk.dto.req.message.ios.Alert;
import com.getui.push.v2.sdk.dto.req.message.ios.Aps;
import com.getui.push.v2.sdk.dto.req.message.ios.IosDTO;
import com.itvita.utils.IdGenerator;
import lombok.extern.slf4j.Slf4j;

import java.util.Map;


/**
 * 推送工具类（个推）
 *
 * @Author: liu.q
 * @Date: 2020/4/26 13:41
 */

@Slf4j
public class UniPush {

    /* unipush 后台配置 */
    private static final String AppID = "";
    private static final String appKey = "";
    private static final String masterSecret = "";
    private static final String domain = "https://restapi.getui.com/v2/";

    /**
     * 根据cid单推
     *
     * @param cid:     推送设备唯一标识
     * @param title:   通知标题
     * @param body:    通知内容
     * @param payload: 参数（长度不能超过100，可以为json字符串）
     * @return: void
     * @Time: 2021/9/7 9:52 上午
     * @author: liu.q [916000612@qq.com]
     */
    public static void toSingleCid(String cid, String title, String body, String payload) {
        GtApiConfiguration apiConfiguration = new GtApiConfiguration();
        //填写应用配置
        apiConfiguration.setAppId(AppID);
        apiConfiguration.setAppKey(appKey);
        apiConfiguration.setMasterSecret(masterSecret);
        apiConfiguration.setDomain(domain);
        // 实例化ApiHelper对象，用于创建接口对象
        ApiHelper apiHelper = ApiHelper.build(apiConfiguration);
        // 创建对象，目前有PushApi、StatisticApi、UserApi
        PushApi pushApi = apiHelper.creatApi(PushApi.class);
        //根据cid进行单推
        PushDTO<Audience> pushDTO = new PushDTO<>();
        // 请求唯一标识号，10-32位之间；如果request_id重复，会导致消息丢失
        pushDTO.setRequestId(IdGenerator.getUUID());
        /*推送目标用户*/
        Audience audience = new Audience();
        audience.addCid(cid);
        pushDTO.setAudience(audience);
        /*推送条件设置*/
        Settings settings = new Settings();
        settings.setTtl(3600000);//消息有效期，走厂商消息需要设置该值
        Strategy strategy = new Strategy();
        // 1: 表示该消息在用户在线时推送个推通道，用户离线时推送厂商通道;
        // 2: 表示该消息只通过厂商通道策略下发，不考虑用户是否在线;
        // 3: 表示该消息只通过个推通道下发，不考虑用户是否在线；
        // 4: 表示该消息优先从厂商通道下发，若消息内容在厂商通道代发失败后会从个推通道下发。
        strategy.setDef(4);
        settings.setStrategy(strategy);
        pushDTO.setSettings(settings);
        /*个推推送消息参数*/
        PushMessage pushMessage = new PushMessage();
        JSONObject param = new JSONObject();
        param.put("title", title);
        param.put("content", body);
        param.put("payload", payload);
        pushMessage.setTransmission(param.toJSONString());
        pushDTO.setPushMessage(pushMessage);
        /*厂商推送消息参数，包含ios消息参数，android厂商消息参数*/
        PushChannel pushChannel = new PushChannel();
        /*苹果推送参数*/
        IosDTO iosDTO = new IosDTO();
        iosDTO.setType("notify");//voip：voip语音推送，notify：apns通知消息
        /*推送通知消息内容*/
        Aps aps = new Aps();
        aps.setContentAvailable(0);
        aps.setSound("default");
        /*推送苹果离线通知标题内容*/
        Alert alert = new Alert();
        alert.setTitle(title+"苹果的标题");
        alert.setBody(body+"苹果的body");
        aps.setAlert(alert);
        iosDTO.setAps(aps);
        iosDTO.setAutoBadge("+1");
        iosDTO.setPayload(payload);//   苹果自定义数据内容
        iosDTO.setApnsCollapseId(IdGenerator.getUUID());//使用相同的apns-collapse-id可以覆盖之前的消息
        pushChannel.setIos(iosDTO);

        /*安卓推送参数*/
        AndroidDTO androidDTO = new AndroidDTO();
        /*android厂商通道推送消息内容*/
        Ups ups = new Ups();
        /*安卓离线厂商通道推送透传消息体*/
//        ups.setTransmission(payload);
        /*安卓离线厂商通道推送通知消息体*/
        ThirdNotification notification = new ThirdNotification();
        notification.setTitle(title);
        notification.setBody(body);
        notification.setClickType("intent");
        notification.setIntent("intent:#Intent;action=android.intent.action.oppopush;launchFlags=0x14000000;component=com.itvita.norisk.company/io.dcloud.PandoraEntry;S.UP-OL-SU=true;S.title=" + title + ";S.content=" + body + ";S.payload="+payload+";end");
        ups.setNotification(notification);
        //各厂商自有功能单项设置
        //各厂商自有功能单项设置
        ups.addOption("HW", "/message/android/notification/badge/class", "io.dcloud.PandoraEntry");
        ups.addOption("HW", "/message/android/notification/badge/add_num", 1);
        ups.addOption("HW", "/message/android/notification/importance", "HIGH");
        ups.addOption("VV","classification",1);
        androidDTO.setUps(ups);
        pushChannel.setAndroid(androidDTO);
        pushDTO.setPushChannel(pushChannel);

        // 进行cid单推
        ApiResult<Map<String, Map<String, String>>> apiResult = pushApi.pushToSingleByCid(pushDTO);
        if (apiResult.isSuccess()) {
            // success
            log.info("推送成功：{}", apiResult.getData());
        } else {
            // failed
            log.error("推送失败：cid:{},code:{}, msg:{}" ,cid, apiResult.getCode() , apiResult.getMsg());
        }
    }

    public static void main(String[] args) {
        JSONObject param = new JSONObject();
        param.put("id", "111");
        param.put("type", "native");
        toSingleCid("bb94fce97ee07c59fce32544ef7b9521", "推送测试", "推送内容", param.toJSONString());
    }
}

```