---
title: xTools帮助文档
categories:
  - xtools-antd
  - vue
tags:
  - vue
mp3: /music/C400001oUtvi02vFfr.m4a
cover: /img/010213-1669395733b8e1.jpg
date: 2022-10-09 19:44:53
---

1. [图片上传](#图片上传)
   1. [示例](#示例)
   2. [代码](#代码)
   3. [属性](#属性)
   4. [事件](#事件)
2. [ztree树形展示](#ztree树形展示)
   1. [示例](#示例-1)
   2. [代码](#代码-1)
   3. [属性](#属性-1)
   4. [事件](#事件-1)
   5. [方法](#方法)
3. [多选](#多选)
   1. [示例](#示例-2)
   2. [代码](#代码-2)
   3. [属性](#属性-2)
   4. [事件](#事件-2)
   5. [方法](#方法-1)
4. [描述列表](#描述列表)
   1. [示例](#示例-3)
   2. [代码](#代码-3)
   3. [属性](#属性-3)
5. [图片预览](#图片预览)
   1. [示例](#示例-4)
   2. [代码](#代码-4)
   3. [属性](#属性-4)
   4. [事件](#事件-3)
6. [富文本](#富文本)
   1. [示例](#示例-5)
   2. [代码](#代码-5)
   3. [属性](#属性-5)
   4. [事件](#事件-4)
7. [简易上传组件](#简易上传组件)
   1. [示例](#示例-6)
   2. [代码](#代码-6)
   3. [属性](#属性-6)
   4. [事件](#事件-5)
8. [图片预览v2](#图片预览v2)
   1. [示例](#示例-7)
   2. [代码](#代码-7)
   3. [属性](#属性-7)
   4. [事件](#事件-6)
## 图片上传
### 示例
![](https://cdn.jsdelivr.net/gh/itvita/resources@master/images/20210910175339.png)
### 代码
```html
<template>
  <div>
    <xui-image-upload
      baseUrl="https://norisk-dev-1305901002.cos.ap-chengdu.myqcloud.com/"
      action="http://192.168.1.59:9001/app/company/h5/v1/common/ant/upload"
      :headers="headers"
      v-model="images"
      :maxNum="3"
      ></xui-image-upload
    >
  </div>
</template>
<script>
export default {
  data () {
    return {
      headers: {
        xxx: 'xxxxxxx'
      },
      images: [
        {
          name: '测试1',
          original:
            '20210910/3ec7557b2a0d40a69b58b9f16a7cf2b1.png?imageMogr2/format/tpg',
          path: '20210910/3ec7557b2a0d40a69b58b9f16a7cf2b1.png'
        }
      ]
    }
  },
  mounted () {},
  methods: {}
}
</script>
<style scoped lang="less"></style>

```

### 属性
| 属性    | 说明             | 类型   | 默认值                  |
| ------- | ---------------- | ------ | ----------------------- |
| baseUrl | 图片访问跟地址   | String |                         |
| action  | 文件上传地址     | String |                         |
| headers | 上传header       | Object | {}                      |
| v-model | 绑定数据         | Array  | []                      |
| maxNum  | 最大上传数量     | Number | 5                       |
| size    | 大小限制，单位MB | Number | 2                       |
| accept  | 限制格式         | String | .png, .jpg, .jpeg, .gif |

### 事件
| 事件名称 | 说明         | 回调参数         |
| -------- | ------------ | ---------------- |
| done     | 上传完成调用 | function(values) |

## ztree树形展示
### 示例
![](https://cdn.jsdelivr.net/gh/itvita/resources@master/images/202202171710336.png)
### 代码
```html
<template>
  <div>
    <xui-ztree
      ref="ztree"
      @click="handelClick"
      allowDrag
      @onDrop="handelOnDrop"
      allowRight
      @add="handelAdd"
      @edit="handelEdit"
      @delete="handelDelete"/>
  </div>
</template>
<script>
export default {
  components: {},
  data () {
    return {}
  },
  mounted () {
    var zNodes = [{
      id: '1471031561859104768',
      accountId: null,
      name: '技术部',
      orgCode: '120',
      orgType: '2',
      fullName: '技术部',
      pid: '0',
      drag: false, // 禁止拖动
      childOuter: false, // 禁止子节点拖走
      dropInner: false, // 禁止拖入内部
      noR: true// 禁止右键
    }, {
      id: '1446660854618521600',
      accountId: null,
      name: '测试1',
      orgCode: '102',
      orgType: '2',
      fullName: '测试1',
      pid: '0'
    }, {
      id: '1433634300481241088',
      accountId: null,
      name: '总经办',
      orgCode: '100',
      orgType: '2',
      fullName: '总经办',
      pid: '0'
    }, {
      id: '1449920876383305728',
      accountId: null,
      name: '技术研发部',
      orgCode: '111',
      orgType: '2',
      fullName: '技术研发部',
      pid: '0'
    }, {
      id: '1449920877176029184',
      accountId: null,
      name: '质量管理部',
      orgCode: '114',
      orgType: '2',
      fullName: '质量管理部',
      pid: '0'
    }, {
      id: '1448897871297380352',
      accountId: null,
      name: '公司所有部门',
      orgCode: '109',
      orgType: '2',
      fullName: '公司所有部门',
      pid: '0'
    }, {
      id: '1446310621657169920',
      accountId: null,
      name: '生产处',
      orgCode: '101',
      orgType: '2',
      fullName: '生产处',
      pid: '0'
    }, {
      id: '1449920877016645633',
      accountId: null,
      name: '印刷车间',
      orgCode: '113',
      orgType: '2',
      fullName: '印刷车间',
      pid: '0'
    }, {
      id: '1446714319529050113',
      accountId: null,
      name: 'EHS部',
      orgCode: '103',
      orgType: '2',
      fullName: 'EHS部',
      pid: '0'
    }, {
      id: '1447462514932580353',
      accountId: null,
      name: '后勤处',
      orgCode: '106',
      orgType: '2',
      fullName: '后勤处',
      pid: '0'
    }, {
      id: '1447462510973157377',
      accountId: null,
      name: '行政部',
      orgCode: '105',
      orgType: '2',
      fullName: '行政部',
      pid: '0'
    }, {
      id: '1447825233716183041',
      accountId: null,
      name: '生产运行部',
      orgCode: '108',
      orgType: '2',
      fullName: '生产运行部',
      pid: '0'
    }, {
      id: '1447462507491885057',
      accountId: null,
      name: '危化部',
      orgCode: '104',
      orgType: '2',
      fullName: '危化部',
      pid: '0'
    }, {
      id: '1467797017227952130',
      accountId: null,
      name: '生产部',
      orgCode: '115',
      orgType: '2',
      fullName: '生产部',
      pid: '0'
    }, {
      id: '1467797032931426306',
      accountId: null,
      name: '安环部',
      orgCode: '118',
      orgType: '2',
      fullName: '安环部',
      pid: '0'
    }, {
      id: '1447824551772684290',
      accountId: null,
      name: '财务部',
      orgCode: '107',
      orgType: '2',
      fullName: '财务部',
      pid: '0'
    }, {
      id: '1467797026493169666',
      accountId: null,
      name: '仓库部',
      orgCode: '116',
      orgType: '2',
      fullName: '仓库部',
      pid: '0'
    }, {
      id: '1467797030205128706',
      accountId: null,
      name: '设备部',
      orgCode: '117',
      orgType: '2',
      fullName: '设备部',
      pid: '0'
    }, {
      id: '1467797034667868162',
      accountId: null,
      name: '副总经理',
      orgCode: '119',
      orgType: '2',
      fullName: '副总经理',
      pid: '0'
    }, {
      id: '1449920876475580418',
      accountId: null,
      name: '模切车间',
      orgCode: '112',
      orgType: '2',
      fullName: '模切车间',
      pid: '0'
    }, {
      id: '1448897871381266435',
      accountId: null,
      name: '综合管理部',
      orgCode: '110',
      orgType: '2',
      fullName: '综合管理部',
      pid: '0'
    }, {
      id: '1433634472804220928',
      accountId: null,
      name: '安全技术部',
      orgCode: '100101',
      orgType: '2',
      fullName: '总经办>安全技术部',
      pid: '1433634300481241088'
    }, {
      id: '1437968767303811072',
      accountId: null,
      name: '综合财务部',
      orgCode: '100102',
      orgType: '2',
      fullName: '总经办>综合财务部',
      pid: '1433634300481241088'
    }, {
      id: '1433634437257494528',
      accountId: null,
      name: '智慧研发部',
      orgCode: '100100',
      orgType: '2',
      fullName: '总经办>智慧研发部',
      pid: '1433634300481241088'
    }, {
      id: '1433634708930953216',
      accountId: null,
      name: '研发一组',
      orgCode: '100100100',
      orgType: '3',
      fullName: '总经办>智慧研发部>研发一组',
      pid: '1433634437257494528'
    }, {
      id: '1433634770872434688',
      accountId: null,
      name: '研发2组',
      orgCode: '100100101',
      orgType: '3',
      fullName: '总经办>智慧研发部>研发2组',
      pid: '1433634437257494528'
    }, {
      id: '1436160986611449856',
      accountId: null,
      name: '技术一组',
      orgCode: '100101100',
      orgType: '3',
      fullName: '总经办>安全技术部>技术一组',
      pid: '1433634472804220928'
    }, {
      id: '1446714319843622912',
      accountId: null,
      name: 'ehs检查科',
      orgCode: '103100',
      orgType: '2',
      fullName: 'EHS部>ehs检查科',
      pid: '1446714319529050113'
    }, {
      id: '1466650607812083712',
      accountId: null,
      name: '0',
      orgCode: '103100101',
      orgType: '2',
      fullName: 'EHS部>ehs检查科>0',
      pid: '1446714319843622912'
    }, {
      id: '1446714320263053312',
      accountId: null,
      name: 'LED班',
      orgCode: '103100100',
      orgType: '3',
      fullName: 'EHS部>ehs检查科>LED班',
      pid: '1446714319843622912'
    }, {
      id: '1447462507835817987',
      accountId: null,
      name: '劳动防护用具',
      orgCode: '104100',
      orgType: '3',
      fullName: '危化部>劳动防护用具',
      pid: '1447462507491885057'
    }, {
      id: '1447462511283535875',
      accountId: null,
      name: '池内外脱落',
      orgCode: '105100',
      orgType: '3',
      fullName: '行政部>池内外脱落',
      pid: '1447462510973157377'
    }, {
      id: '1447462513175166980',
      accountId: null,
      name: '警示标识',
      orgCode: '105101',
      orgType: '3',
      fullName: '行政部>警示标识',
      pid: '1447462510973157377'
    }, {
      id: '1447462515242958851',
      accountId: null,
      name: '有落石',
      orgCode: '106100',
      orgType: '3',
      fullName: '后勤处>有落石',
      pid: '1447462514932580353'
    }, {
      id: '1447825234022367232',
      accountId: null,
      name: 'eh检查科',
      orgCode: '108100',
      orgType: '2',
      fullName: '生产运行部>eh检查科',
      pid: '1447825233716183041'
    }]
    var root = {
      open: true,
      id: '0',
      pId: '-1',
      name: '跟节点',
      // icon: 'https://cdn.jsdelivr.net/gh/itvita/liuqiang@master/nage/gongsi.png' //自定义图标
      drag: false, // 禁止拖动
    }
    zNodes.forEach(d => {
      d.pId = d.pid
      delete d.pid
      // d.icon = 'https://cdn.jsdelivr.net/gh/itvita/liuqiang@master/nage/gongsi.png'
      // drag: false, // 禁止拖动
      // childOuter: false, // 禁止子节点拖走
      // dropInner: false, // 禁止拖入内部
      // noR: true// 禁止右键
    })
    zNodes.push(root)
    this.$refs.ztree.init(zNodes)
  },
  methods: {
    handelClick (treeNode) {
      console.log(treeNode)
    },
    handelOnDrop (treeNodes, targetNode, moveType) {
      console.log(treeNodes, targetNode, moveType)
    },
    handelAdd (treeNode) {
      console.log(treeNode)
    },
    handelEdit (treeNode) {
      console.log(treeNode)
    },
    handelDelete (treeNode) {
      console.log(treeNode)
    }
  }
}
</script>
<style scoped lang="less"></style>


```

### 属性
| 属性       | 说明         | 类型    | 默认值 |
| ---------- | ------------ | ------- | ------ |
| allowDrag  | 允许拖动     | Boolean | false  |
| allowRight | 允许右键菜单 | Boolean | false  |

### 事件
| 事件名称 | 回调参数                                  | 说明                                                                                                         |
| -------- | ----------------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| click    | function(treeNode)                        | 点击事件，选中项的数据                                                                                       |
| onDrop   | function(treeNodes, targetNode, moveType) | 拖动结束事件，treeNodes：拖动节点数组，targetNode目标节点，moveType移动方式（inner拖入，prev拖上，next拖下） |
| add      | function(treeNode)                        | 新增事件，选中项的数据                                                                                       |
| edit     | function(treeNode)                        | 编辑事件，选中项的数据                                                                                       |
| delete   | function(treeNode)                        | 删除事件，选中项的数据                                                                                       |

### 方法
| 方法名称 | 参数                        | 说明       |
| -------- | --------------------------- | ---------- |
| init     | 树形简单数据[{id,name,pId}] | 树形初始化 |
| select   | id                          | 设置选中   |



## 多选
### 示例
![](https://cdn.jsdelivr.net/gh/itvita/resources@master/images/20210910180900.png)
### 代码
```html
<template>
  <div>
    <xui-multiple-choice
      ref="xMultipleChoice"
      :multiple="true"
      @change="handelChange"
      :dataSource="data"
    />
    <a @click="done">获取选择结果</a>
  </div>
</template>
<script>
export default {
  data () {
    const data = [
      {
        name: '现场管理',
        children: []
      },
      {
        name: '基础管理',
        children: []
      }
    ]
    for (var i = 0; i < data.length; i++) {
      for (var x = 0; x < 10; x++) {
        data[i].children.push({
          id: i + '' + x,
          name: i + '-测试数据' + x
        })
      }
    }
    return {
      data: data
    }
  },
  mounted () {},
  methods: {
    /**
     * @Time: 2021-07-23 23:05:02
     * @author: liu.q [916000612@qq.com]
     * @des:  item 当前操作项, type【'selected'选择，'unselected'取消选择】, selectIds 最终结果id数组
     * */
    handelChange ({ item, type, selectIds }) {
      console.log(item, type, selectIds)
    },
    /**
     * @Time: 2021-07-23 23:06:14
     * @author: liu.q [916000612@qq.com]
     * @des:  获取最终选择结果
     * */
    done () {
      /* 获取选中ID */
      const selectIds = this.$refs.xMultipleChoice.getSelectIds()
      console.log(selectIds)
      /* 获取选中对象 */
      const selectObjects = this.$refs.xMultipleChoice.getSelectObjects()
      console.log(selectObjects)
    }
  }
}
</script>
<style scoped lang="less"></style>
```

### 属性
| 属性       | 说明                                 | 类型    | 默认值 |
| ---------- | ------------------------------------ | ------- | ------ |
| multiple   | 是否多选                             | Boolean | false  |
| dataSource | 数据源，两级数组[{id,name,children}] | Array   |        |

### 事件
| 事件名称 | 回调参数                            | 说明                                                                                              |
| -------- | ----------------------------------- | ------------------------------------------------------------------------------------------------- |
| change   | function({ item, type, selectIds }) | 选项改变，item 当前操作项, type【'selected'选择，'unselected'取消选择】, selectIds 最终结果id数组 |


### 方法
| 方法名称         | 参数 | 说明         |
| ---------------- | ---- | ------------ |
| getSelectIds     |      | 获取选中ID   |
| getSelectObjects |      | 获取选中对象 |

## 描述列表
### 示例
![](https://cdn.jsdelivr.net/gh/itvita/resources@master/images/20210917094248.png)
### 代码
```html
<template>
<div>
  <xui-descriptions label-width="200px" label="测试标题" >
    斐济电视剧覅哦啊江东四杰佛i啊惊世毒妃
  </xui-descriptions>
  <xui-descriptions label="测试标题" label-width="200px">
    斐济电视剧覅
  </xui-descriptions>
   <xui-descriptions label="测试标题" label-width="200px">
    <div><img src="fidjsif"/></div>
  </xui-descriptions>
</div>
</template>
<script>
export default {
data () {
return {}
},
mounted () {},
methods: {}
}
</script>
<style scoped lang="less"></style>

```


### 属性
| 属性        | 说明             | 类型   | 默认值 |
| ----------- | ---------------- | ------ | ------ |
| label       | 标题             | String |        |
| label-width | 标题宽度，单位px | String | 0px    |

## 图片预览
### 示例
![](https://cdn.jsdelivr.net/gh/itvita/resources@master/images/20211021113519.png)

![](https://cdn.jsdelivr.net/gh/itvita/resources@master/images/20211021113828.png)

![](https://cdn.jsdelivr.net/gh/itvita/resources@master/images/20211021113549.png)

### 代码

```html
<template>
  <div>
    <xui-image-preview
      :showBtn="true"
      :showName="false"
      width="100px"
      height="100px"
      :baseUrl="baseUrl"
      url="path"
      v-model="ImgList"
    />
  </div>
</template>
<script>
export default {
  data () {
    return {
      baseUrl: 'https://norisk-prod-1305901002.cos.ap-chengdu.myqcloud.com/',
      ImgList: [
        {
          name: '测试',
          path: '20211015/f9cec9d0e43d4edb91c69d5d2b9389b0.jpg'
        },
        {
          name: '测试',
          path: '20211015/f9cec9d0e43d4edb91c69d5d2b9389b0.jpg'
        },
        {
          name: '测试',
          path: '20211015/f9cec9d0e43d4edb91c69d5d2b9389b0.jpg'
        },
        {
          name: '测试',
          path: '20211015/f9cec9d0e43d4edb91c69d5d2b9389b0.jpg'
        },
        {
          name: '测试',
          path: '20211015/f9cec9d0e43d4edb91c69d5d2b9389b0.jpg'
        }
      ]
    }
  },
  mounted () {},
  methods: {}
}
</script>
<style scoped lang="less"></style>

```
### 属性
| 属性           | 说明                   | 类型    | 默认值 |
| -------------- | ---------------------- | ------- | ------ |
| v-model(value) | 数据[{name:xx,url:xx}] | Array   | []     |
| url            | url 键名               | String  | url    |
| baseUrl        | 图片访问跟域名         | String  | ''     |
| width          | 宽                     | String  | 100px  |
| height         | 高                     | String  | 100px  |
| showBtn        | 是否显示预览 删除按钮  | Boolean | false  |
| showName       | 是否显示图片名称       | Boolean | false  |

### 事件
| 事件名称 | 回调参数                  | 说明                                           |
| -------- | ------------------------- | ---------------------------------------------- |
| change   | function(newData)         | 图片列表改变后的数组                           |
| delete   | function(newData,delData) | 删除事件，newData删除后的结果，delData删除数据 |

## 富文本
### 示例
![](https://cdn.jsdelivr.net/gh/itvita/resources@master/images/20211028105103.png)
### 代码
```html
<template>
  <div>
    <xui-editor
      v-model="values"
      @change="handelChange"
      placeholder="输入内容提示文字。。。"
      :action="action"
      :basePath="basePath"
      :height="300"
      :headers="headers"
    />
  </div>
</template>
<script>
export default {
  data () {
    return {
      action: 'https://apis.norisk.com.cn/app/company/v1/common/ant/upload', // 文件上传地址
      basePath: 'https://norisk-prod-1305901002.cos.ap-chengdu.myqcloud.com/', // 文件预览跟地址
      values: '<p>我是默认内容</p>',
      headers: {
        'token':'111111'
      }
    }
  },
  mounted () {},
  methods: {
    handelChange () {
      console.log(this.values)
    }
  }
}
</script>
<style scoped lang="less"></style>
```
### 属性
| 属性           | 说明             | 类型   | 默认值        |
| -------------- | ---------------- | ------ | ------------- |
| v-model(value) | 数据(html内容)   | String | ''            |
| action         | 文件上传地址     | String | ''            |
| basePath       | 图片访问跟路径   | String | ''            |
| placeholder    | 空内容提示性文字 | String | 请输入内容... |
| height         | 高(单位px)       | Number | 300           |
| headers        | 自定义header     | Object | {}            |

### 事件
| 事件名称 | 回调参数           | 说明         |
| -------- | ------------------ | ------------ |
| change   | function(newValue) | 内容改变触发 |

## 简易上传组件
### 示例
![](https://cdn.jsdelivr.net/gh/itvita/resources@master/images/202112311136516.png)
### 代码
```html
<template>
  <div>
    <x-upload
      accept=".doc,.docx,.pdf,.xls,.xlsx"
      :size="1"
      :action="url"
      @beforeUpload="beforeUpload"
      @uploadSuccess="uploadSuccess"
      @uploadError="uploadError"
    >
      <div>
        简易上传，自定义按钮
      </div>
    </x-upload>
  </div>
</template>

<script>
export default {
  data () {
    return {
      url: 'https://xxx.com/v1/upload'
    }
  },
  methods: {
    beforeUpload (param) {
      console.log(param)
    },
    uploadSuccess (param) {
      console.log(param)
    },
    uploadError (error) {
      console.log(error)
    }
  }
}
</script>

<style scoped>

</style>
```
### 属性
| 属性    | 说明                       | 类型   | 默认值 |
| ------- | -------------------------- | ------ | ------ |
| action  | 文件上传地址               | String | ''     |
| size    | 文件限制大小，单位MB       | Number | 2      |
| accept  | 格式限制（.jpg,.png,.xls） | String | 各种   |
| headers | 自定义header               | Object | {}     |
| params  | 自定义额外参数             | Object | {}     |

### 事件
| 事件名称      | 回调参数                                   | 说明         |
| ------------- | ------------------------------------------ | ------------ |
| beforeUpload  | function({ id,file,name,size,suffix})      | 上传前调用   |
| uploadSuccess | function({name,path,original,suffix,size}) | 上传成功调用 |
| uploadError   | function({message})                        | 上传失败调用 |

## 图片预览v2
### 示例
![](https://cdn.jsdelivr.net/gh/itvita/resources@master/images/202202151155088.png)
### 代码
```html
<template>
  <div>
    <x-image-preview
      width="100px"
      height="100px"
      :baseUrl="baseUrl"
      url="path"
      :showDel="true"
      :draggable="true"
      v-model="ImgList"
      @change="handelChange"
    >
    </x-image-preview>
  </div>
</template>

<script>
export default {
  data () {
    return {
      baseUrl: 'https://norisk-prod-1305901002.cos.ap-chengdu.myqcloud.com/',
      ImgList: [
        {
          id: 1,
          path: '20220119/014026340563464bb7ee74d653325825.png'
        },
        {
          id: 2,
          path: '20211015/f9cec9d0e43d4edb91c69d5d2b9389b0.jpg'
        }
      ]
    }
  },
  mounted () {
    setTimeout(() => {
      this.ImgList.push(
        {
          id: 3,
          path: '20211015/f9cec9d0e43d4edb91c69d5d2b9389b0.jpg'
        }
      )
    }, 3000)
  },
  methods: {
    handelChange (v) {
    console.log(JSON.stringify(v))
      console.log(JSON.stringify(this.ImgList))
    }
  }
}
</script>

<style scoped>

</style>

```
### 属性
| 属性           | 说明                 | 类型    | 默认值  |
| -------------- | -------------------- | ------- | ------- |
| v-model(value) | 绑定数据[{path:xxx}] | Array   | ''      |
| width          | 宽                   | String  | '100px' |
| height         | 高                   | String  | '100px' |
| baseUrl        | 图片跟地址           | String  |         |
| url            | list对应url路径key   | String  |         |
| showDel        | 是否显示删除按钮     | Boolean | true    |
| draggable      | 是否允许拖动         | Boolean | true    |

### 事件
| 事件名称 | 回调参数           | 说明         |
| -------- | ------------------ | ------------ |
| change   | function(newValue) | 内容改变触发 |
| delete   | function(delValue) | 删除项       |

