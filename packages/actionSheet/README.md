# 动作面板 ActionSheet

创建可交互的弹出动作面板，显示在屏幕下方，可填入分享、列表项、表单项的元素。

### 使用场景

常见用于分享网页、发送文件、弹出型选择、弹出型勾选框等。

### 引入

``` javascript
import Vue from 'vue'
import {ActionSheet} from 'yun-ui'
import 'yun-ui/dist/yun/ActionSheet/index.css'

Vue.component(ActionSheet.name, ActionSheet)
```

### 代码示例

``` javascript
<template>
    <!-- 创建一个用于分享的弹出面板 -->
    <y-action-sheet type="panel" panelTitle="分享到" :actionSheetItem="actionSheetPanelItem"
                @maskClicked="maskClicked" :show="showActionPanel" @cancel="maskClicked">
    </y-action-sheet>
    <!-- 创建一个列表型的弹出面板 -->
    <y-action-sheet type="list" @maskClicked="maskClicked" :show="showActionList"
                @cancel="maskClicked" :actionSheetItem="actionSheetPanelItem">
    </y-action-sheet>
    <!-- 创建一个含表单的弹出面板 -->
    <y-action-sheet type="checkbox" @maskClicked="maskClicked" @confirm="maskClicked" @change="actionSheetChange"
                @cancel="maskClicked" :show="showActionCheckbox" :actionSheetItem="actionSheetCheckboxItem">
    </y-action-sheet>
</template>
<script>
export default {
    props: {},
    data () {
        return {
            actionSheetPanelItem: [
                {
                    title: '同事圈',
                    icon: require('../assets/placeholder-figure.png'),
                    callback: this.actionItemClick
                },
                {
                    title: '收藏',
                    icon: require('../assets/placeholder-figure.png'),
                    callback: this.actionItemClick
                }
            ],
            actionSheetCheckboxItem: [
                {
                    title: '上传到电脑',
                    checked: true,
                    value: 'upload',
                    icon: require('../assets/placeholder-figure.png'),
                    callback: this.actionItemClick
                },
                {
                    title: '转发',
                    icon: require('../assets/placeholder-figure.png'),
                    callback: this.actionItemClick
                }
            ],
            showActionPanel: false,
            showActionList: false,
            showActionCheckbox: false
        }
    },
    methods: {
        maskClicked: function () {
            console.log('mask clicked')
            this.showActionList = false
            this.showActionCheckbox = false
            this.showActionPanel = false
            this.showPop = false
        },
        checkboxChange: function (value, status) {
            console.log(value)
            console.log(status)
        },
        actionItemClick: function () {
            console.log('action item clicked')
        },
        actionSheetChange: function (value, status) {
            console.log(value，status)
        }
    }
}
</script>
```

### API

|      参数      |    说明    |    类型    |       可选值    |      默认值   |
|     ----      |   ----     |   ----    |      ----      |     ----     |
|     type      | 弹出面板类型 |   String  |  panel,list,checkbox |       |
|   panelTitle  |   panel类型时的标题  |   String  |   |        |
|actionSheetItem|   传入的菜单项，每一项为一个对象  |   Array  |   |       |
|     show      |    此actionSheet是否显示    |   Boolean  |  true,false  |   false  |
|    change     |   面板为checkbox类型时，复选框变化时的回调函数，第一个参数为复选框变化后的值，第二个参数为复选框的label值|Function| | |
|  maskClicked  |    点击蒙层时的回调函数,用于控制切换actionSheet的显隐状态    |   Function  |  | |
|    cancel     |    点击X按钮或点击取消按钮时的回调函数    |   Function  |  | |
|    confirm    |    点击确定时的回调函数    |   Function  |  | |


### actionSheetItem

actionSheetItem内各个项需要传入的参数说明：

|      参数     |         说明        |    类型    |       可选值    |      默认值   |
|     ----     |         ----     |   ----    |      ----      |     ----     |
|     title    | 通用，菜单项的标题  |   String  |              |              |
|     icon     |  通用，菜单项的图标         |   String  |             |               |
|    callback  | 通用，菜单项点击后的事件回调，参数为当前菜单项    |   Function  |  |  |
|    value     | checkbox类型专用，用于区分不同菜单项  |   String |          |      |
|    checked   | checkbox类型专用，菜单项默认是否勾选 |   Boolean | true,false | false |
