---
title: uniapp在线更新
categories:
  - uniapp
tags:
  - uniapp
mp3: /music/滚滚红尘.mp3
cover: /img/230359-16521950393a5a.jpg
date: 2022-10-29 19:56:36
---
### 说在前面
1. 每次打开app检查版本
2. 此处为强制更新，其他非强制更新，热更新等同理。
### 上代码

```javascript
/* APP版本更新
 res = {
 	code: 1,
 	data: {
 		version: 200, //版本号
 		iosLink: '',
 		androidLink: 'http://192.168.1.49:8080/20210913110002.apk',
 		content: '1版本更新内容\n2版本更新内容\n3版本更新内容'
 	}
 }
 */
export function checkUpdate() {
	$api({
		url: $config.baseURL + '/v1/appInfo',
		method: 'GET',
		data: {}
	}).then(res => {
		if (res.code === 1) {
			const appinfo = res.data
			plus.runtime.getProperty(plus.runtime.appid, widgetInfo => {
				const versionCode = widgetInfo.versionCode;
				if (versionCode < appinfo.version) {
					uni.showModal({
						title: '发现新版本',
						showCancel: false,
						confirmText: '立即更新',
						content: appinfo.content,
						success: (res) => {
							if (res.confirm) {
								if (uni.getSystemInfoSync().platform == 'android') {
									var w = plus.nativeUI.showWaiting("下载中...");
									const downloadTask = uni.downloadFile({
										url: appinfo.androidLink,
										success: downloadResult => {
											if (downloadResult.statusCode ===
												200) {
												plus.runtime.install(
													downloadResult
													.tempFilePath, {
														force: false
													},
													d => {
														console.log(
															'install success...'
														);
														plus.runtime
															.restart();
													},
													e => {
														console.error(
															'install fail...'
														);
													}
												);
											}
										}
									});
									downloadTask.onProgressUpdate((res) => {
										w.setTitle("  正在下载" + res.progress + "%  ");
										if(res.progress>=100){
											w.close();
										}
										//  console.log('下载进度' + res.progress);
                    //   console.log('已经下载的数据长度' + res.totalBytesWritten);
                    //   console.log('预期需要下载的数据总长度' + res.totalBytesExpectedToWrite);
									});
								}
								if (uni.getSystemInfoSync().platform == 'ios') {
									plus.runtime.openURL(appinfo.iosLink, function(res) {});
								}
							}
						}
					})

				}
			})
		}
	})
}

```