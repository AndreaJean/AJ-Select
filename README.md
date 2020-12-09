# AJ-Select

基于js，jquery的下拉框插件。

支持功能：

  1、基础单选；

  2、可清空单选；

  3、基础多选；

  4、设置默认选中项
  
  5、树形结构单、多选

  6、设置前置文字

  7、可过滤选项


## 引用
```html
<link rel="stylesheet" type="text/css" href="css/select.css">
<script type="text/javascript" src="js/jquery.min.js"></script>
<script type="text/javascript" src="js/tree.js"></script>
<script type="text/javascript" src="js/select.js"></script>
```
- 选项为列表形式时可不引用tree.js

## 调用

```JavaScript
var mySelect = new AjSelect(opt) //创建对象
mySelect.init(data) //初始化
```

## 参数

#### opt的默认设置

```JavaScript
{
  id: '', // 生成下拉框的父级DOM元素id
  preText: '', // 前置文字，放置于下拉框前的说明文字
  preStyle: '', // 前置文字样式
  placeholder: '', // 下拉框内的提示文字
  isMultiple: false, // 是否多选
  showTree: false, // 选项是否为树结构
  showClear: false, // 是否显示清空按钮
  showSearch: false, // 是否开启选项过滤功能
  // 下拉框的样式
  inputStyle: {
    width: '', // 宽度
    height: '', // 高度
    bgColor: '', // 背景色
    color: '', // 文字颜色
    fontSize: '', // 文字字号
    borderRadius: '', // 边框圆角
    borderwith: '', // 边框粗细
    borderColor: '', // 边框颜色
    arrowColor: ''// 下拉框右侧尖角图标颜色
  },
  // 选项面板样式
  panelStyle: {
    bgColor: '', // 背景色
    borderRadius: '', // 边框圆角
    borderwith: '', // 边框粗细
    borderColor: '', // 边框颜色
    color: '', // 选项文字颜色
    fontSize: '', // 选项文字字号
    lineHeight: '', // 选项文字行高
    colorSel: '', // 选中选项文字颜色
    fontSizeSel: '', // 选中选项文字字号
    bgColorSel: '' // 选中选项背景色
  },
  // 回调函数
  callback: {
    clearOver: null, // 清空事件
    selectOver: null, // 选中项改变
    dataOver: null, // 选项加载完毕
    setData: null // 调用$_setData后
  }
}
```

#### 列表形式选项data

结构为对象数组，示例：
```JavaScript
var data = [
  {pid:'0', label: '中国', value: '中国', selected: true},
  {pid:'1', label: '美国', value: '美国', selected: false, disable: true},
  {pid:'2', label: '日本', value: '日本', selected: false},
  {pid:'3', label: '英国', value: '英国', selected: false, disable: true},
  {pid:'4', label: '意大利', value: '意大利', selected: false},
  {pid:'5', label: '韩国', value: '韩国', selected: false},
  {pid:'6', label: '西班牙', value: '西班牙', selected: false},
  {pid:'7', label: '越南', value: '越南', selected: false},
  {pid:'8', label: '泰国', value: '泰国', selected: false}
]
```
- label：{String}，必含属性，选项文字
- value：{String}，必含属性，选项值
- selected：{Boolean}，非必含属性，值为true该选项初始选中
- disable：{Boolean}，非必含属性，值为true该选项禁选
- pid：{---}，自定义属性、隐藏属性，不限个数和类型

#### 树结构选项data

结构为多层级对象数组，示例：
```JavaScript
var data = [
  {
    id: '010',
    label: '北京',
    level: 1,
    children: [
      {
        id: '010-CY',
        label: '朝阳区',
        level: 2,
        children: [
          { id: '010-CY-AYC', label: '奥运村街道', level: 3, children: [] },
          { id: '010-CY-YYC', label: '亚运村街道', level: 3, children: [] }
        ]
      },
      {
        id: '010-CP',
        label: '昌平区',
        level: 2,
        children: [
          {
            id: '010-CP-TTYB',
            label: '天通苑北街道',
            level: 3,
            children: []
          }
        ]
      }
    ]
  },
  { id: '020', label: '上海', level: 1, children: [] },
  { id: '0371', label: '郑州', level: 1, children: [] },
  { id: '0391', label: '焦作', level: 1, children: [] }
]
```
- id：{String}，必含属性，选项唯一标识，选项值
- label：{String}，必含属性，选项文字
- children：{Boolean}，必含属性，子节点信息
- level：{---}，自定义属性、隐藏属性，不限个数和类型

#### 方法

| 方法名 | 说明 | 参数 | 返回值 |
| --- | --- | --- | --- |
|$_getData|获取当前选中项数据|---|选中项数据JSON字符串，单选为对象，多选为数组|
|$_setData|加载表格数据|selectedVal：{String}，选项value，多个value用逗号隔开|---|
|$_addCheck|显示/隐藏校验文字|flag：{Boolean}，true可用，false不可用；msg：{String}，校验不通过时的提示文字；type：{String}，提示文字出现的位置，'right'或者'bottom'|---|
|$_disabled|设置下拉框可用不可用|flag：{Boolean}，true可用，false不可用|---|
|onClear|清空选中项或是恢复默认选中项|---|---|
