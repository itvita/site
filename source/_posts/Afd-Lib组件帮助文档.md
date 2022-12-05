---
html:
  toc: true
  print_background: true
toc:
  depth_from: 1
  depth_to: 6
  ordered: true
title: Afd-Lib组件帮助文档
categories:
  - vue
  - Afd-Lib
tags:
  - vue
mp3: /music/C400000ztSoN2Od4mh.m4a
cover: /img/005035-1667839835482e.jpg
date: 2022-11-12 18:30:07
---
<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=true} -->

<!-- code_chunk_output -->

1. [视频预览列表](#视频预览列表)
    1. [示例](#示例)
    2. [属性说明](#属性说明)
2. [基础上传按钮](#基础上传按钮)
    1. [示例](#示例-1)
    2. [属性](#属性)
    3. [事件](#事件)
    4. [values说明](#values说明)
3. [文件上传](#文件上传)
    1. [示例](#示例-2)
    2. [属性](#属性-1)
    3. [step说明](#step说明)
    4. [事件](#事件-1)
    5. [values举例](#values举例)
4. [树形下拉](#树形下拉)
    1. [示例](#示例-3)
    2. [属性](#属性-2)
    3. [asyncLoad说明](#asyncload说明)
    4. [方法](#方法)
    5. [事件](#事件-2)
5. [树形](#树形)
    1. [示例](#示例-4)
    2. [属性](#属性-3)
    3. [事件](#事件-3)
    4. [方法](#方法-1)
6. [时间选择器](#时间选择器)
    1. [示例](#示例-5)
    2. [属性](#属性-4)
    3. [事件](#事件-4)
7. [文本显示](#文本显示)
    1. [示例](#示例-6)
    2. [属性](#属性-5)
    3. [事件](#事件-5)
8. [table表格](#table表格)
    1. [示例](#示例-7)
    2. [属性](#属性-6)
    3. [columns](#columns)
    4. [columns列配置示例](#columns列配置示例)
        1. [基本配置](#基本配置)
        2. [格式化文本](#格式化文本)
        3. [格式化显示图片](#格式化显示图片)
        4. [格式化为图文](#格式化为图文)
        5. [格式化为开关按钮](#格式化为开关按钮)
        6. [格式化为徽章](#格式化为徽章)
    5. [operate](#operate)
        1. [items](#items)
    6. [operate配置示例](#operate配置示例)
    7. [方法](#方法-2)
9. [搜索条](#搜索条)
    1. [示例](#示例-8)
    2. [属性](#属性-7)
    3. [items示例](#items示例)
    4. [事件](#事件-6)
    5. [方法](#方法-3)
10. [报表](#报表)
    1. [示例](#示例-9)
    2. [属性](#属性-8)
    3. [方法](#方法-4)
11. [报表导出](#报表导出)
    1. [示例](#示例-10)
    2. [属性](#属性-9)
    3. [方法](#方法-5)
12. [日期选择器](#日期选择器)
    1. [示例](#示例-11)
    2. [属性](#属性-10)
    3. [事件](#事件-7)
13. [日期范围选择器](#日期范围选择器)
    1. [示例](#示例-12)
    2. [属性](#属性-11)
    3. [事件](#事件-8)
14. [单选选择器](#单选选择器)
    1. [示例](#示例-13)
    2. [属性](#属性-12)
    3. [事件](#事件-9)
15. [多选选择器](#多选选择器)
    1. [示例](#示例-14)
    2. [属性](#属性-13)
    3. [事件](#事件-10)
16. [月选择](#月选择)
    1. [示例](#示例-15)
    2. [属性](#属性-14)
    3. [事件](#事件-11)
17. [图片列表](#图片列表)
    1. [示例](#示例-16)
    2. [属性](#属性-15)
18. [高德地图坐标拾取](#高德地图坐标拾取)
    1. [示例](#示例-17)
    2. [属性](#属性-16)
    3. [事件](#事件-12)
19. [树形](#树形-1)
    1. [效果](#效果)
    2. [示例](#示例-18)
    3. [属性](#属性-17)
    4. [事件](#事件-13)

<!-- /code_chunk_output -->


##  视频预览列表

> 点击播放

### 示例

```vue
<template>
  <div>
    <lz-video url="path" :data-list="videoDataList" />
  </div>
</template>
<script>
export default {
  data () {
    return {
      videoDataList: [
        {
          path: 'http://127.0.0.1:8080/1.mp4'
        },
        {
          path: 'http://127.0.0.1:8080/3.mp4'
        }
      ]
    }
  },
  created () {},
  mounted () {},
  methods: {}
}
</script>
<style></style>

```

### 属性说明

| 属性     | 说明                       | 类型   | 默认值 |
| -------- | -------------------------- | ------ | ------ |
| url      | dataList 中视频访问地址key | String | path   |
| dataList | 视频列表                   | Array  |        |
| baseUrl  | url跟地址                  | String | ''     |

##  基础上传按钮

> 一般用于工具条，不回显上传结果。

### 示例

```vue
<template>
  <div>
    <lz-btn-upload
      @beforeUpload="beforeUpload"
      @doneUpload="doneUpload"
      label="导入"
      accept=".xlsx,.xls"
      action="http://localhost:8102/base/common/upload/image"
    />
  </div>
</template>
<script>
  export default {
    data () {
      return {}
    },
  created () {},
  mounted () {},
  methods: {
    beforeUpload (values) {
      console.log('导入前', values)
    },
    doneUpload (values) {
      console.log('导入后', values)
    }
  }
  }
</script>
<style></style>

```

### 属性

| 属性   | 说明                    | 类型   | 默认值 |
| ------ | ----------------------- | ------ | ------ |
| label  | 组件名称                | String | 导入   |
| size   | 允许上传文件大小 单位MB | Number | 2      |
| accept | 允许上传文件类型        | String |        |
| action | 文件上传路径            | String |        |

### 事件

| 事件名称     | 说明               | 回调参数         |
| ------------ | ------------------ | ---------------- |
| beforeUpload | 文件开始上传前调用 | function(values) |
| doneUpload   | 文件上传完成后调用 | function(values) |

### values说明

```json
{
		file:File,
		id: "1qgc04h0lsclr7bhtcby"
    name: "文件名.xlsx"
    original: "源文件路径"
    path: "压缩文件路径"
    state: 2 //状态，1开始上传，2上传成功，3上传失败
	}
```

## 文件上传

> 常用于表单，可以预览，下载。

### 示例

```vue
<template>
  <div>
    <lz-upload
      v-model="uploadList"
      :max-num="5"
      :size="5"
      @change="change"
      @beforeUpload="beforeUpload"
      @doneUpload="doneUpload"
      accept=".jpg,.png,.xlsx,.doc,.docx"
      :disabled="false"
      basePath="https://echftp.yqzhfw.com/"
      action="https://jmy.yqzhfw.com/train/api/base-server/base/common/upload/image"
      :replaceFields="{
        name: 'name',
        path: 'path',
        original: 'original',
        size: 'size',
        suffix: 'suffix',
      }"
      :showDownload="true"
    />
    <!-- :step="{ size: 2048 }" -->

  </div>
</template>
<script>
export default {
  data () {
    return {
      uploadList: [
        // {
        //   name: "音频服务.png",
        //   path: "/basis/2020/7/10/13acde2b08e84fc7bae4e9c0195facfc.png",
        // },
      ]
    }
  },
  methods: {
    change (param) {
      console.log('change', param)
    },
    beforeUpload (param) {
      console.log('beforeUpload', param)
    },
    doneUpload (param) {
      console.log('doneUpload', param)
    }
  }
}
</script>

```

### 属性

| 属性           | 说明               | 类型    | 默认值                                                       |
| -------------- | ------------------ | ------- | ------------------------------------------------------------ |
| value(v-model) | 设置上传文件默认值 | Array   | []                                                           |
| max-num        | 允许最大文件数     | Number  | 0                                                            |
| size           | 单位MB             | Number  | 2                                                            |
| accept         | 允许上传文件类型   | String  | 几乎所有文件                                                 |
| disabled       | 是否禁用           | boolean | false                                                        |
| imgBasePath    | 文件访问跟路径     | String  |                                                              |
| action         | 文件上传路径       | String  |                                                              |
| replaceFields  | 结果 key替换       | Object  | {<br/>          name: 'name',<br/>          path: 'path',<br/>          original: 'original',<br/>          size: 'size',<br/>          suffix: 'suffix',<br/>  } |
| step           | 开启分片上传       | Object  | false                                                        |

### step说明

| 属性 | 说明             | 类型   | 默认值 |
| ---- | ---------------- | ------ | ------ |
| size | 分片大小，单位kb | Number | 无     |

### 事件

| 事件名称     | 说明               | 回调参数 |
| ------------ | ------------------ | -------- |
| change       | 文件发生改变后调用 | values   |
| beforeUpload | 文件上传前回调     | values   |
| doneUpload   | 文件上传结束回调   | values   |

### values举例

```
[{
   name: "音频服务.png",
   path: "/basis/2020/7/10/13acde2b08e84fc7bae4e9c0195facfc.png",
}]
```

## 树形下拉

### 示例

```vue
<template>
  <div>
    <lz-tree-select
      ref="dTreeSelect"
      :replaceFields="{
        key: 'id',
        value: 'value',
        title: 'title',
        children: 'children',
      }"
      v-model="treeSelect"
      @change="change"
      :multiple="false"
    />
  </div>
</template>
<script>
export default {
  data () {
    return {
      treeSelect: ['0-0', '0-0-1']
    }
  },
  created () {},
  mounted () {
    this.$refs.dTreeSelect.init([
        {
          title: 'Node1',
          value: '0-0',
          id: '0-0',
          children: [
            {
              value: '0-0-1',
              id: '0-0-1',
              title: 'title'
            },
            {
              title: 'Child Node2',
              value: '0-0-2',
              id: '0-0-2'
            }
          ]
        },
        {
          title: 'Node2',
          value: '0-1',
          id: '0-1'
        }
      ])
  },
  methods: {
    change (val) {
      console.log(val)
    }
  }
}
</script>
<style></style>
```

### 属性

| 属性           | 说明                                             | 类型             | 默认值                                                       |
| -------------- | ------------------------------------------------ | ---------------- | ------------------------------------------------------------ |
| replaceFields  | 替换结果集中key，value,title，children为对应字段 | Object           | {<br/>       key: 'key',<br/>        value:'value',<br>         title: 'title',<br/>         children: 'children'<br/>   } |
| v-model(value) | 绑定值单选时String ，多选时 Array                | String/Array     |                                                              |
| multiple       | 是否开启多选                                     | Boolean          | false                                                        |
| asyncLoad      | 异步加载数据                                     | function（node） | -                                                            |

### asyncLoad说明

```js
asyncLoad ({ id }) {
  return new Promise((resolve) => {
    this.$axios({
      url: 'http://localhost:7001/api/xxx/getTree',
      params: { pid: id }
      }).then((res) => {
      	resolve(res.data)
    })
  })
}
```

### 方法

| 属性 | 说明       | 举例                                               |
| ---- | ---------- | -------------------------------------------------- |
| init | 数据初始化 | this.$refs.dTreeSelect.init([]) //初始化一个空数组 |

### 事件

| 事件名称 | 说明           | 回调参数        |
| -------- | -------------- | --------------- |
| change   | 选中值改变触发 | function(value) |

## 树形

### 示例

```vue
<template>
  <div>
    <lz-tree
      ref="dTree"
      :replaceFields="{
        key: 'key',
        title: 'title',
        children: 'children',
      }"
      @click="nodeClick"
      :asyncLoad="false"
    >
    </d-tree>
  </div>
</template>
<script>
export default {
  data () {
    return {
      treeData: [
        {
          title: 'Node1',
          value: '0-0',
          key: '0-0',
          children: [
            {
              value: '0-0-1',
              key: '0-0-1',
              title: 'title'
            },
            {
              title: 'Child Node2',
              value: '0-0-2',
              key: '0-0-2'
            }
          ]
        },
        {
          title: 'Node2',
          value: '0-1',
          key: '0-1'
        }
      ]
    }
  },
  created () {},
  mounted () {
    this.$refs.dTree.init(this.treeData)
  },
  methods: {
    nodeClick (param) {
      console.log(param)
    },
    asyncLoad ({ id }) {
      return new Promise((resolve) => {
        this.$axios({
          url: 'http://localhost:7001/api/xxx/getTree',
          params: { pid: id }
        }).then((res) => {
          resolve(res.data) // 子节点数据 []
        })
      })
    },
    refresh () {
      this.$refs.dTree.refreshByPid(0, function () {
        console.log('刷新完成')
      })
    }
  }
}
</script>
<style></style>

```

### 属性

| 属性          | 说明                                       | 类型             | 默认值                                                       |
| ------------- | ------------------------------------------ | ---------------- | ------------------------------------------------------------ |
| replaceFields | 替换结果集中key，title，children为对应字段 | Object           | {<br/>       key: 'key',<br/>        title: 'title',<br/>         children: 'children'<br/>   } |
| asyncLoad     | 异步加载数据 （不需要异步可不配置）        | function（node） | -                                                            |

### 事件

| 事件名称 | 说明         | 回调参数        |
| -------- | ------------ | --------------- |
| click    | 节点点击事件 | function(value) |

### 方法

| 方法名称     | 参数        | 说明                             |
| ------------ | ----------- | -------------------------------- |
| init         | 树形数组    | 初始化数据，异步时可以传空数组[] |
| refreshByPid | id,callback | 要刷新的节点ID，刷新完成回调     |

## 时间选择器

### 示例

```vue
<template>
  <div>
    <lz-time-picker v-model="timePicker" @change="change"></d-time-picker>
  </div>
</template>
<script>
  export default {
    data () {
      return {
        timePicker: ''
      }
    },
  created () {},
  mounted () {},
  methods: {
    change (value) {
      console.log(value)
    }
  }
  }
</script>
<style></style>

```

### 属性

| 属性           | 说明                                            | 类型    | 默认值   |
| -------------- | ----------------------------------------------- | ------- | -------- |
| v-model(value) | 绑定值                                          | String  | ''       |
| allowClear     | 是否显示清空按钮                                | Boolean | false    |
| disabled       | 是否禁用                                        | Boolean | false    |
| format         | 日期格式                                        | String  | HH:mm:ss |
| hourStep       | 小时选项间隔                                    | Number  | 1        |
| minuteStep     | 分钟选项间隔                                    | Number  | 1        |
| secondStep     | 秒选项间隔                                      | Number  | 1        |
| placeholder    | 没有值的时候显示的内容                          | String  | ''       |
| size           | 文本框大小[large,default,small]                 | String  | default  |
| inputReadOnly  | 设置输入框为只读（避免在移动设备上打开虚拟键盘) | Boolean | true     |

### 事件

| 事件名称 | 说明       | 回调参数        |
| -------- | ---------- | --------------- |
| change   | 值改变事件 | function(value) |

## 文本显示

### 示例

```vue
<template>
  <div>
    <lz-text value="测试" color="primary" @click="handelClick" />
  </div>
</template>
<script>
export default {
  components: {},
  data () {
    return {}
  },
  created () {},
  mounted () {},
  methods: {
    handelClick (value) {
      console.log(value)
    }
  }
}
</script>
<style></style>

```

### 属性

| 属性  | 说明                                      | 类型   | 默认值  |
| ----- | ----------------------------------------- | ------ | ------- |
| value | 显示值                                    | String | ''      |
| color | 显示颜色【primary,success,warning,error】 | String | default |

### 事件

| 事件名称 | 说明     | 回调参数        |
| -------- | -------- | --------------- |
| click    | 点击事件 | function(value) |

## table表格

### 示例

```vue
<template>
  <div>
    <lz-table ref="myTable">
      <div slot="tools">
        <a-button icon="plus" @click="getSelect" type="primary">获取选中项id</a-button>
      </div>
    </d-table>
  </div>
</template>
<script>
export default {
  data () {
    return {}
  },
  created () {},
  mounted () {
    this.tableInit()
  },
  methods: {
    search (param) {
      this.$refs.myTable.search(param)
    },
    tableInit () {
      this.$refs.myTable.init(
        {
          url: 'http://localhost:9001/xxxx/getList',
          columns: [
            {
              field: 'title',
              title: '名称',
              sorter: 'true',
              align: 'left',
              width: 150
            },
            {
              field: 'path',
              title: '路由/权限',
              align: 'left',
              width: 150
            },
            {
              field: 'icons',
              title: '图标',
              align: 'left',
              width: 100,
              hidden: true
            },
            {
              field: 'menuType',
              title: '类型',
              sorter: 'true',
              align: 'center',
              width: 80,
              formatter: {
                type: 'text',
                format: (row) => {
                  if (row.menuType === 0) {
                    return {
                      value: '目录'
                    }
                  } else if (row.menuType === 1) {
                    return {
                      value: '菜单'
                    }
                  } else if (row.menuType === 2) {
                    return {
                      value: '按钮'
                    }
                  } else {
                    return {
                      value: '-'
                    }
                  }
                }
              }
            },
            {
              field: 'seq',
              title: '顺序号',
              sorter: 'true',
              align: 'right',
              width: 120
            }
          ],
          operate: {
            items: [
              {
                label: '编辑',
                color: 'primary',
                event: (row) => {
                  console.log(row)
                }
              },
              {
                label: '删除',
                color: 'danger',
                event: (row) => {
                  this.$confirm({
                    title: '确认删除？',
                    content: '删除后将无法恢复！',
                    onOk: () => {
                      console.log(row)
                    }
                  })
                }
              }
            ]
          }
        },
        () => {
          this.search()
        }
      )
    },
    getSelect () {
      console.log(this.$refs.myTable.getSelected())
    }
  }
}
</script>
<style></style>

```

### 属性

| 属性         | 说明                                                         | 是否必填 | 类型     | 默认值            |
| ------------ | ------------------------------------------------------------ | -------- | -------- | ----------------- |
| url          | 请求链接                                                     | 是       | String   |                   |
| method       | 请求方式                                                     | 否       | post/get | get               |
| pagination   | 是否显示分页                                                 | 否       | boolean  | true              |
| queryParams  | 默认参数                                                     | 否       | Object   | {}                |
| pageNumber   | 初始化加载第一页，默认第一页                                 | 否       | Number   | 1                 |
| pageSize     | 每页的记录行数（*）                                          | 否       | Number   | 10                |
| pageList     | 可供选择的每页的行数                                         | 否       | Array    | [10, 25, 50, 100] |
| showColumns  | 是否显示所有的列                                             | 否       | boolean  | true              |
| showRefresh  | 是否显示刷新按钮                                             | 否       | boolean  | true              |
| changeSize   | 允许改变列大小                                               | 否       | boolean  | true              |
| showCheckBox | 显示复选框                                                   | 否       | boolean  | false             |
| showIndex    | 显示序号                                                     | 否       | boolean  | true              |
| height       | 行高，如果没有设置height属性，表格自动根据记录条数设置表格高度 | 否       | Number   | 500               |
| columns      | 定义列                                                       | 是       | Array    |                   |
| operate      | 定义操作                                                     | 否       | Object   |                   |

### columns

| 属性      | 说明                             | 是否必填 | 类型    | 默认值 |
| --------- | -------------------------------- | -------- | ------- | ------ |
| field     | 字段名                           | 是       | String  | -      |
| title     | 显示名                           | 是       | String  | -      |
| sorter    | 是否可以排序                     | 否       | Boolean | false  |
| width     | 宽度 ，不配置则自适应宽度        | 否       | Integer | 自适应 |
| align     | 对齐方式 可选：left center right | 否       | String  | left   |
| hidden    | 是否隐藏                         | 否       | Boolean | false  |
| formatter | 如下示例 ：                      | 否       | Object  | -      |

### columns列配置示例

#### 基本配置

```js
[
  {
    field: 'title', //字段名
    title: '标签名称', //显示名
    sorter: true, //是否可以排序
    width:200,//宽度 ，不配置则自适应宽度
    align: 'left',//对齐方式 可选：left center right
    hidden: false
  },
  。。。
]
```

#### 格式化文本

> 多用于标题，可通过点击事件查看详情

```js
{
  field: 'title',
  title: '名称',
  sorter: 'true',
  align: 'left',
  width: 100,
  formatter: {
    type: 'text', //格式化方式
    format: row => {
    return {
      value: row.title, //显示文本（必填）
      color: 'primary', // 显示颜色 'primary','danger','success','warning','info','default'
      event:()=>{ // 点击触发事件
        	// ...
        }
      }
    }
  }
}
```

#### 格式化显示图片

> 可用于头像等需要显示图片的列

```js
{
  field: 'headImage',
  title: '状态',
  sorter: 'true',
  align: 'center',
  width: 100,
  formatter: {
   type: 'image', //格式化方式
   format: row => {
     return {
      name:'',// 名称
      url:''  // 图片路径
     }
   }
  }
}
```

#### 格式化为图文

> 同上，但图片右侧可配置显示的文字

```js
{
  field: 'name',
  title: '状态',
  sorter: 'true',
  align: 'center',
  width: 100,
  formatter: {
   type: 'image-text', //格式化方式
   format: row => {
     return {
      name:'',// 名称
      url:''  // 图片路径
      text:[ //显示文本内容， 建议一行或两行
         {
           content:'显示文本'
         },
         {
           content:'显示文本'
         }
      ]
     }
   }
  }
}
```

#### 格式化为开关按钮

> 不建议使用

```js
{
  field: 'state',
  title: '状态',
  sorter: 'true',
  align: 'center',
  width: 100,
  formatter: {
   type: 'switch', //格式化方式
   format: row => {
     return {
      value:true,// 是否选中  true | false
      change:()=>{// change事件回调
         const v = !row.state
         // ...
       }
     }
   }
  }
}
```

#### 格式化为徽章

> 常用于展示各种状态

```js
{
  field: 'state',
  title: '状态',
  sorter: 'true',
  align: 'center',
  width: 100,
  formatter: {
   type: 'badge', //格式化方式
   format: row => {
     return {
      value:'审核通过',
      color:'blue'//徽章颜色'blue','green','gray','orange','yellow','red' 等支持16进制
     }
   }
  }
}
```

### operate

| 属性  | 说明       | 是否必填 | 类型    | 默认值 |
| ----- | ---------- | -------- | ------- | ------ |
| width | 操作列宽度 | 否       | Integer | 自适应 |
| items | 操作配置   | 是       | Array   | -      |

#### items

| 属性       | 说明                                         | 是否必填 | 类型          | 默认值 |
| ---------- | -------------------------------------------- | -------- | ------------- | ------ |
| label      | 显示名称                                     | 是       | String        | -      |
| permission | 权限标识                                     | 否       | String        | -      |
| color      | 显示颜色【primary,success,danger,warning..】 | 是       | String        | -      |
| event      | 点击事件                                     | 是       | Function(row) |        |
| hidden     | 隐藏条件                                     | 是       | Function(row) |        |

### operate配置示例

```js
operate: {
          width: 200,
          items: [
            {
              label: '编辑',
              color: 'primary',
              event: row => {
                this.$refs.edit.showModal(row.id)
              },
              hidden: row => {
                return row.roleType === 1
              }
            },
            {
              label: '置顶',
              color: 'success',
              event: row => {
                update({
                  id: row.id,
                  isTop: 1
                }).then(res => {
                  if (res.code === 1) {
                    this.$message.success('置顶成功')
                    this.search()
                  }
                })
              },
              hidden: row => {
                return row.isTop === 1
              }
            },
            {
              label: '取消置顶',
              color: 'danger',
              event: row => {
                update({
                  id: row.id,
                  isTop: 0
                }).then(res => {
                  if (res.code === 1) {
                    this.$message.success('取消成功')
                    this.search()
                  }
                })
              },
              hidden: row => {
                return row.isTop !== 1
              }
            },
            {
              label: '删除',
              color: 'danger',
              event: row => {
                this.$confirm({
                  title: '确认删除？',
                  content: '删除后将无法恢复！',
                  onOk: () => {
                    dels([row.id]).then(res => {
                      if (res.code === 1) {
                        this.$message.success('删除成功')
                        this.$refs.myTable.selectedRowKeys = []
                        this.search()
                      }
                    })
                  }
                })
              }
            }
          ]
        }
```



### 方法

| 方法名称        | 参数                         | 返回结果                       | 说明                              |
| --------------- | ---------------------------- | ------------------------------ | --------------------------------- |
| selectedRowKeys | -                            | [id,id,id]                     | 获取选中的key                     |
| selectedRows    | -                            | [{row},{row},{row}]            | 获取选中的行                      |
| search          | JSON                         | -                              | 执行搜索{pageNumber:1}=搜索第一页 |
| getSelected     | -                            | {selectedRowKeys,selectedRows} | 获取选中的行与选中的key           |
| setSelected     | selectedRowKeys,selectedRows | -                              | 设置选中项                        |

> 关于列表多选，需要保留结果的，建议使用多选选择器

## 搜索条

> 常配合table表格使用位于table上方的搜索条件

### 示例

```vue
<template>
  <div>
    <lz-search ref="searchBar" :column="3" :items="items" @search="search" @reset="reset"></d-search>
    <a-button @click="getSearchValues">获取搜索参数</a-button>
    <a-button style="margin-left:10px;" @click="setSearchValues">设置搜索值</a-button>
    <div>{{ searchValue }}</div>
  </div>
</template>
<script>
import items from './items'
export default {
  data () {
    return {
      items,
      searchValue: {}
    }
  },
  created () {},
  mounted () {},
  methods: {
    reset () {
      console.log('重置搜索条件')
    },
    search (param) {
      this.searchValue = param
    },
    getSearchValues () {
      this.searchValue = this.$refs.searchBar.getValues()
    },
    setSearchValues () {
      this.$refs.searchBar.setValues({
        title: '测试标题',
        state: 0,
        dates: ['2020-10-10', '2020-11-11']
      })
    }
  }
}
</script>
<style></style>

```

### 属性

| 属性   | 说明           | 类型   | 默认值 |
| ------ | -------------- | ------ | ------ |
| items  | 搜索条件配置   | Array  | []     |
| column | 每行显示多少列 | Number | 3      |

### items示例

```json
export default [
//文本
  {
    type: 'text', //组件类型
    dataIndex: 'name', //组件key
    label: '名称', //组件显示名称
  },
  //下拉静态数据
  {
    type: 'select',
    dataIndex: 'state',
    label: '状态',
    options: [ //选项配置
      {
        label: '启用',//名称
        value: '1' //值
      },
      {
        label: '禁用',
        value: '0'
      }
    ]
  },
  //下拉动态数据
   {
    type: 'select',
    dataIndex: 'state',
    label: '状态',
    options: [],
    optionsConfig: { //动态数据配置
       url:'http://localhost:8102/base/classify/getAll',//数据请求地址result:{code:1,content:[]}
       label: 'title',// label对应key  不设置默认label
       value: 'id' //value 对应key  不设置默认value
    }
  },
    //树形下拉
   {
    type: 'tree-select',
    dataIndex: 'dept',
    label: '树形下拉',
    defaultValue: '',
    allowLv: '>=0',//允许选择层级的条件===n,!==n ,>=n ,<=n,>n,<n,false 不使用条件(不使用条件时，可通过返回结果内增加disabled=[true|false]控制是否可选)
    asyncLoad:false,//是否开启数据懒加载（开启后会在请求url上增加参数?pid=value）
    optionsConfig: {
       url:'http://localhost:8102/base/classify/getAll',//数据请求地址result:{code:1,content:[{label,value,lv,[disabled]}]}
       label: 'title',// label对应key  不设置默认title
       value: 'id', //value 对应key  不设置默认value
       lv: 'lv'//层级 不设置 默认 lv
    }
  },
  //日期范围
  {
    type: 'range-picker',
    dataIndex: 'dates',
    label: '日期范围',
  },
  //月选择框
  {
    type: 'month-picker',
    dataIndex: 'month',
    label: '月份选择',
  }
]
```

### 事件

| 事件名称 | 说明     | 回调参数         |
| -------- | -------- | ---------------- |
| search   | 点击搜索 | function(values) |
| reset    | 点击重置 | function()       |

### 方法

| 方法名称        | 参数   | 返回结果 | 说明             |
| --------------- | ------ | -------- | ---------------- |
| getValues       | -      | Object   | 获取当前搜索条件 |
| setSearchValues | Object | -        | 设置当前搜索条件 |

## 报表

> 需结合报表服务

### 示例

```vue
<template>
  <div>
    <lz-report
      ref="dReport"
      :domain="domain"
      reportId="ff80808174d28d1b0174d2b88a730000"
      reportName="验收单"
    >
      <a-button @click="hideModal">关闭</a-button>
    </d-report>
  </div>
</template>
<script>
export default {
  data () {
    return {
      domain: 'http://xxxxxx' // 报表服务的跟地址
    }
  },
  created () {},
  mounted () {
    this.$refs.dReport.init({ orderId: 1, brandId: 123 }, () => {})
  },
  methods: {}
}
</script>
<style></style>

```

### 属性

| 属性       | 说明                 | 类型   | 默认值 |
| ---------- | -------------------- | ------ | ------ |
| domain     | 报表服务跟域名       | Array  | 必填   |
| reportId   | 报表配置ID           | String | 必填   |
| reportName | 报表名称             | String | 报表   |
| solt       | 插槽，可插入操作按钮 | -      | -      |

### 方法

| 方法名称 | 参数 | 返回结果 | 说明                                 |
| -------- | ---- | -------- | ------------------------------------ |
| init     | JSON | -        | 初始化报表，参数为配置报表时所需参数 |

## 报表导出

> 依赖报表服务

### 示例

```vue
<template>
  <div>
    <lz-export-tools
      ref="lzExportTools"
      domain="http://localhost:7001"
      reportId="ff80808174d28d1b0174d43fb7e40001"
      reportName="测试导出"
      @click="exportClick"
    />
  </div>
</template>
<script>
export default {
  data () {
    return {}
  },
  created () {},
  mounted () {},
  methods: {
    exportClick () {
      this.$refs.dExportTools.exportExcel({ keyword: 'ceshi' })
    }
  }
}
</script>
<style></style>

```

### 属性

| 属性       | 说明           | 类型   | 默认值 |
| ---------- | -------------- | ------ | ------ |
| domain     | 报表服务跟域名 | Array  | 必填   |
| reportId   | 报表配置ID     | String | 必填   |
| reportName | 报表名称       | String | 报表   |

### 方法

| 方法名称    | 参数 | 返回结果 | 说明      |
| ----------- | ---- | -------- | --------- |
| exportWord  | JSON | -        | 导出word  |
| exportExcel | JSON | -        | 导出excel |
| exportPdf   | JSON | -        | 导出pdf   |

## 日期选择器

### 示例

```vue
<template>
  <div>
    <lz-date-picker
      v-model="datePicker"
      :show-time="{
        format: 'HH:mm',
      }"
      :show-today="false"
      @change="dateChange"
      :disabledDate="disabledDate"
    />
  </div>
</template>
<script>
import moment from 'moment'
export default {
  data () {
    return {
      datePicker: '2020-10-10'
    }
  },
  created () {},
  mounted () {},
  methods: {
    dateChange (values) {
      console.log(values)
    },
    disabledDate (current) {
      // 只能选择今天之前
      return current && current > moment().endOf('day')
    }
  }
}
</script>
<style></style>

```

### 属性

| 属性           | 说明                                               | 类型                | 默认值     |
| -------------- | -------------------------------------------------- | ------------------- | ---------- |
| v-model(value) | 绑定值                                             | Array               | []         |
| allowClear     | *是否展示清除按钮*                                 | Boolean             | false      |
| disabled       | *禁用全部操作*                                     | Boolean             | false      |
| format         | *展示的时间格式*                                   | String              | YYYY-MM-DD |
| placeholder    | *没有值的时候显示的内容*                           | Array               | []         |
| size           | 文本框大小[large,default,small]                    | String              | default    |
| inputReadOnly  | *设置输入框为只读（避免在移动设备上打开虚拟键盘）* | Boolean             | true       |
| showToday      | *是否展示“今天”按钮*                               | Boolean             | true       |
| showTime       | *显示时间选择器*                                   | [Object, Boolean]   | false      |
| disabledDate   | *禁用日期*                                         | [Function, Boolean] | false      |
| disabledTime   | *禁用时间*                                         | [Function, Boolean] | false      |

### 事件

| 事件名称 | 说明       | 回调参数         |
| -------- | ---------- | ---------------- |
| change   | 选择值改变 | function(values) |

## 日期范围选择器

### 示例

```vue
<template>
  <div>
    <lz-range-picker
      v-model="rangePicker"
      format="YYYY-MM-DD HH:mm"
      :showTime="{
        format: 'HH:mm',
      }"
      :disabled-date="disabledDate"
      :placeholder="['开始日期','结束日期']"
    ></d-range-picker>
  </div>
</template>
<script>
import moment from 'moment'
export default {
  data () {
    return {
      rangePicker: ['', '']
    }
  },
  created () {},
  mounted () {},
  methods: {
    disabledDate (current) {
      // 禁止点击今天与今天之前的日志
      return current && current < moment().endOf('day')
    }
  }
}
</script>
<style></style>

```

### 属性

| 属性           | 说明                                               | 类型                | 默认值     |
| -------------- | -------------------------------------------------- | ------------------- | ---------- |
| v-model(value) | 绑定值                                             | Array               | []         |
| allowClear     | *是否展示清除按钮*                                 | Boolean             | false      |
| disabled       | *禁用全部操作*                                     | Boolean             | false      |
| format         | *展示的时间格式*                                   | String              | YYYY-MM-DD |
| placeholder    | *没有值的时候显示的内容*                           | Array               | []         |
| size           | 文本框大小[large,default,small]                    | String              | default    |
| inputReadOnly  | *设置输入框为只读（避免在移动设备上打开虚拟键盘）* | Boolean             | true       |
| showTime       | *显示时间选择器*                                   | [Object, Boolean]   | false      |
| disabledDate   | *禁用日期*                                         | [Function, Boolean] | false      |
| disabledTime   | *禁用时间*                                         | [Function, Boolean] | false      |
| showRanges     | *显示扩展按钮*                                     | Boolean             | true       |

### 事件

| 事件名称 | 说明       | 回调参数         |
| -------- | ---------- | ---------------- |
| change   | 选择值改变 | function(values) |

## 单选选择器

### 示例

```vue
<template>
  <div>
    <lz-one-selector
      :action="action"
      :replaceFields="{
        title: 'cateName,cateCode',
        description: 'createTime',
      }"
      v-model="selector"
      @change="handelChange"
      :show-description="true"
    />
  </div>
</template>
<script>
export default {
  data () {
    return {
      selector: null,
      action: 'http://xxx'
    }
  },
  created () {},
  mounted () {},
  methods: {
    handelChange (values) {
      console.log(values)
    }
  }
}
</script>
<style></style>

```

### 属性

| 属性            | 说明                                                         | 类型    | 默认值                                                       |
| --------------- | ------------------------------------------------------------ | ------- | ------------------------------------------------------------ |
| v-model(value)  | 绑定值                                                       | Object  | null                                                         |
| action          | 左侧数据请求url<br/>（自动附加请求参数：pageSize，pageNumber，keyword） | String  | ''                                                           |
| replaceFields   | 显示的内容可以用(,)分割在一行展示多列                        | Object  | {<br/>	title: 'title,code',<br/>	description: 'createTime',<br/>} |
| showDescription | 是否显示描述行                                               | Boolean | true                                                         |

### 事件

| 事件名称 | 说明               | 回调参数         |
| -------- | ------------------ | ---------------- |
| change   | 结果发生改变时调用 | function(values) |

## 多选选择器

### 示例

```vue
<template>
  <div>
    <lz-multiple-selector
      :action="action"
      :replaceFields="{
        title: 'title,code',
        description: 'note',
      }"
      v-model="selector"
      :show-description="false"
      @change="handelChange"
    />
  </div>
</template>
<script>
  export default {
    data () {
      return {
        selector: [],
        action: 'http://xxx'
      }
    },
  created () {},
  mounted () {},
  methods: {
    handelChange (values) {
        console.log(values)
    }
  }
  }
</script>
<style></style>

```

### 属性

| 属性            | 说明                                                         | 类型    | 默认值                                                       |
| --------------- | ------------------------------------------------------------ | ------- | ------------------------------------------------------------ |
| v-model(value)  | 绑定值                                                       | Object  | null                                                         |
| action          | 左侧数据请求url<br/>（自动附加请求参数：pageSize，pageNumber，keyword） | String  | ''                                                           |
| replaceFields   | 显示的内容可以用(,)分割在一行展示多列                        | Object  | {<br/>	title: 'title,code',<br/>	description: 'createTime',<br/>} |
| showDescription | 是否显示描述行                                               | Boolean | true                                                         |

### 事件

| 事件名称 | 说明               | 回调参数         |
| -------- | ------------------ | ---------------- |
| change   | 结果发生改变时调用 | function(values) |

## 月选择

### 示例

```vue
<template>
  <div>
    <lz-month-picker v-model="month" :disabledDate="disabledDate" />
  </div>
</template>
<script>
import moment from 'moment'
export default {
  data () {
    return {
      month: null
    }
  },
  created () {},
  mounted () {},
  methods: {
    disabledDate (current) {
      // 只能选择今天及以前的月
      return current && current > moment().endOf('day')
    }
  }
}
</script>
<style></style>

```

### 属性

| 属性           | 说明                                               | 类型                | 默认值  |
| -------------- | -------------------------------------------------- | ------------------- | ------- |
| v-model(value) | 绑定值                                             | String              | null    |
| allowClear     | *是否展示清除按钮*                                 | Boolean             | false   |
| disabled       | *禁用全部操作*                                     | Boolean             | false   |
| format         | *展示格式*                                         | String              | YYYY-MM |
| placeholder    | *没有值的时候显示的内容*                           | String              | ''      |
| size           | 文本框大小[large,default,small]                    | String              | default |
| inputReadOnly  | *设置输入框为只读（避免在移动设备上打开虚拟键盘）* | Boolean             | true    |
| disabledDate   | *禁用日期*                                         | [Function, Boolean] | false   |

### 事件

| 事件名称 | 说明               | 回调参数         |
| -------- | ------------------ | ---------------- |
| change   | 结果发生改变时调用 | function(values) |

## 图片列表

### 示例

```vue
<template>
  <div>
    <lz-image
      url="path"
      :data-list="dataList"
      width="100px"
      height="100px"
    >

    </d-image></div>
</template>
<script>
  export default {
    data () {
      return {
        dataList: [
          {
            path:
              'https://ss0.bdstatic.com/94oJfD_bAAcT8t7mm9GUKT-xh_/timg?image&quality=100&size=b4000_4000&sec=1595555863&di=170ed927a6ae5b36f478e5b222d05816&src=http://a3.att.hudong.com/14/75/01300000164186121366756803686.jpg'
          },
          {
            path:
              'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1595565947814&di=88ad5be9f62cf469215501c5abe970a0&imgtype=0&src=http%3A%2F%2Fa4.att.hudong.com%2F22%2F59%2F19300001325156131228593878903.jpg'
          },
          {
            path:
              'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1595565947814&di=88ad5be9f62cf469215501c5abe970a0&imgtype=0&src=http%3A%2F%2Fa4.att.hudong.com%2F22%2F59%2F19300001325156131228593878903.jpg'
          },
          {
            path:
              'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1595565947814&di=88ad5be9f62cf469215501c5abe970a0&imgtype=0&src=http%3A%2F%2Fa4.att.hudong.com%2F22%2F59%2F19300001325156131228593878903.jpg'
          },
          {
            path:
              'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1595565947814&di=88ad5be9f62cf469215501c5abe970a0&imgtype=0&src=http%3A%2F%2Fa4.att.hudong.com%2F22%2F59%2F19300001325156131228593878903.jpg'
          },
          {
            path:
              'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1595565947814&di=88ad5be9f62cf469215501c5abe970a0&imgtype=0&src=http%3A%2F%2Fa4.att.hudong.com%2F22%2F59%2F19300001325156131228593878903.jpg'
          }
        ]
      }
    },
  created () {},
  mounted () {},
  methods: {}
  }
</script>
<style></style>

```

### 属性

| 属性      | 说明                             | 类型   | 默认值 |
| --------- | -------------------------------- | ------ | ------ |
| data-list | 图片列表数据                     | Array  | []     |
| url       | 图片列表中对应url的地址dataIndex | String | url    |
| baseUrl   | 图片访问跟地址                   | String | ''     |
| width     | 图片宽                           | String | 100px  |
| height    | 图片高                           | String | 100px  |

## 高德地图坐标拾取

### 示例

```vue
<template>
  <div>
    <lz-map-choose-address
      map-key="87ff1e887140aa980a075c096a434940"
      placeholder="请设置地址"
      v-model="chooseArddr"
      @change="chooseArddrChange"
    />
    选择结果：{{ chooseArddr }}

  </div>
</template>
<script>
export default {
  data () {
    return {
      chooseArddr: null
      // {
      //   addr: '河南省郑州市金水区文化路街道河南省农业科学院1',
      //   lat: '34.788996',
      //   lng: '113.679317'
      // }
    }
  },
  created () {},
  mounted () {},
  methods: {
    chooseArddrChange (val) {
      console.log(val)
    }
  }
}
</script>
<style></style>

```

### 属性

| 属性           | 说明              | 类型   | 默认值 |
| -------------- | ----------------- | ------ | ------ |
| v-model(value) | 绑定数据          | Object | null   |
| placeholder    | 数据空时提示      | String | ''     |
| mapKey         | 高德地图申请的key | String | 必填   |

### 事件

| 事件名称 | 说明               | 回调参数         |
| -------- | ------------------ | ---------------- |
| change   | 结果发生改变时调用 | function(values) |

## 树形

> 适用于授权等，层级不限，最后一级横排。

### 效果

![lzAuthTree.jpg](https://cdn.jsdelivr.net/gh/itvita/liuqiang@master/md/lzAuthTree.jpg)

### 示例

```vue
<template>
  <div>
    <lz-auth-tree v-model="checkedKeys" :items="treeData" @change="change" />
  </div>
</template>
<script>
export default {
  components: {},
  data () {
    return {
      checkedKeys: ['1323994360672419840'],
      treeData: [
        {
          children: [
            {
              pid: '1323994360672419840',
              menuType: 2,
              id: '1323995046420152320',
              title: '分类管理'
            },
            {
              pid: '1323994360672419840',
              menuType: 2,
              id: '1323997514642227200',
              title: '文章管理'
            },
            {
              pid: '1323994360672419840',
              menuType: 2,
              id: '1335853728959299584',
              title: '用户管理'
            }
          ],
          pid: '0',
          menuType: 1,
          id: '1323994360672419840',
          title: 'IT生活'
        },
        {
          children: [
            {
              pid: '1322770188088639488',
              menuType: 2,
              id: '1322803882748805120',
              title: '用户管理'
            },
            {
              pid: '1322770188088639488',
              menuType: 2,
              id: '1322774696441151488',
              title: '菜单管理'
            },
            {
              pid: '1322770188088639488',
              menuType: 2,
              id: '1322803959471013888',
              title: '角色管理'
            }
          ],
          pid: '0',
          menuType: 1,
          id: '1322770188088639488',
          title: '系统管理'
        }
      ]
    }
  },
  created () {},
  mounted () {},
  methods: {
    change (e) {
      console.log(e)
    }
  }
}
</script>
<style></style>		
```

### 属性

| 属性           | 说明     | 类型                          | 默认值 |
| -------------- | -------- | ----------------------------- | ------ |
| v-model(value) | 绑定数据 | Array                         | []     |
| items          | 渲染数据 | Array(树形)[{id:xx,title:xx}] | []     |

### 事件

| 事件名称 | 说明               | 回调参数         |
| -------- | ------------------ | ---------------- |
| change   | 结果发生改变时调用 | function(values) |

