<!--Created by suti(https://github.com/suti), modified by Chuanfeng(https://github.com/ChuanfengZhang)-->
<template>
  <div class="drop-down"
       :class="{poped: currentVisible}"
       @click="handleClick"
       @mouseenter="handleMouseenter"
       @mouseleave="handleMouseleave"
  >
    <div class="drop-down-sel">
      <i v-if="hasFolderIcon" class="icon-folder" :class="curFolder"></i>
      <span :title="da.sel">{{da.sel}}</span>
    </div>

    <div class="drop-down-drop"
         v-show="currentVisible"
    >
      <div
          class="drop-down-drop-option"
          v-for="(item, index) in da.opt"
          :key="index"
          :class="{disabled:item.dis, selected:item.sel}"
          @click.stop="handleItemClick(item, index)"
      >
        <i v-if="hasFolderIcon" class="icon-folder" :class="folderColorClass(item.color)"></i>
        <span class="option-title" :title="item.des">{{item.des}}</span>
      </div>
    </div>
  </div>
</template>
<script>
  export default {
    name: 'drop-down',
    data() {
      return {
        da: { // 处理后的数据
          sel: '',
          opt: []
        },
        curFolder: '', // 当前文件夹颜色
        currentVisible: false // 是否显示列表
      }
    },
    props: {
      dData: {
        type: Array,
        required: true,
        default: () => {
          return []
        }
      },
      trigger: { // 显示列表的触发方式
        type: String,
        default: 'hover'
      },
      hasFolderIcon: { // 是否有文件夹图标
        type: Boolean,
        default: false
      }
    },
    mounted() {
      this.dealData();
    },
    watch: {
      dData() {
        this.dealData();
      }
    },
    methods: {
      // 处理传入数据
      dealData() {
        this.da.opt = this.dData;
        for (let i = 0; i < this.dData.length; i++) {
          if (i === 0) {
            this.da.sel = this.dData[0].des;
          }
          this.da.opt[i].des = this.dData[i].des ? this.dData[i].des : '未命名';
        }
      },
      handleClick() {
        if (this.trigger !== 'click') {
          return false
        }
        this.currentVisible = !this.currentVisible
      },
      handleMouseenter() {
        if (this.trigger !== 'hover') {
          return false
        }
        this.currentVisible = true
      },
      handleMouseleave() {
        if (this.trigger !== 'hover') {
          return false
        }
        this.currentVisible = false
      },
      // 处理列表项点击
      handleItemClick(item, index) {
        if (item.dis) return
        let arr = []
        for (let i = 0; i < this.da.opt.length; i++) {
          arr[i] = this.da.opt[i]
          arr[i].sel = i === index
        }
        this.currentVisible = false
        this.$emit('select', this.da.opt[index])
        this.$set(this.da, 'opt', arr)
        this.$set(this.da, 'sel', arr[index].des)
        if (this.hasFolderIcon) {
          this.curFolder = this.folderColorClass(item.color)
        }
      },
      folderColorClass(color) {
        switch (color) {
          case 0:
            // 0 (默认浅灰色)
            return {
              'grey-folder': true
            };
            break;
          case 1:
            // 1浅蓝色
            return {
              'blue-folder': true
            };
            break;
          case 2:
            // 2紫色
            return {
              'royalBlue-folder': true
            };
            break;
          case 3:
            // 3洋红色
            return {
              'pink-folder': true
            };
            break;
          case 4:
            // 4橙色
            return {
              'orange-folder': true
            };
            break;
          case 5:
            // 5金黄色
            return {
              'yellow-folder': true
            };
            break;
          case 6:
            // 6浅绿色
            return {
              'green-folder': true
            };
            break;
        }
      }
    }
  }
</script>
<style lang="less" scoped>
  @import './dropDown';
</style>