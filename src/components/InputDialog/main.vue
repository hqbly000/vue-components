<template>
  <div v-if="dialogVisible">
    <el-dialog
      :title="title"
      :visible.sync="dialogVisible"
      :width="width"
      top="5vh"
      :close-on-click-modal="false"
      append-to-body
    >
      <div :style="{ height: height }" class="i-dialog-div">
        <slot> </slot>
      </div>
      <div slot="footer" class="dialog-footer">
        <slot name="footer-btn-group">
          <el-button @click="dialogVisible = false">取 消</el-button>
          <el-button type="primary" @click="handleConfirm">保 存</el-button>
        </slot>
      </div>
    </el-dialog>
  </div>
</template>

<script>
import { debounce } from 'throttle-debounce'

export default {
  name: 'InputDialog',
  props: {
    visible: {
      required: true,
      type: Boolean,
      default: false
    },
    title: {
      required: false,
      type: String,
      default: '标题'
    },
    width: {
      type: String,
      default: '600px'
    },
    height: {
      type: String,
      default: 'auto'
    }
  },
  computed: {
    dialogVisible: {
      get() {
        return this.visible
      },
      set(val) {
        this.$emit('update:visible', val)
      }
    }
  },
  methods: {
    handleConfirm: debounce(function() {
      this.$emit('confirm')
    }, 300)
  }
}
</script>
<style scope>
.el-dialog__header {
  text-align: left;
  border-bottom: 1px solid #efefef;
}

.el-dialog__footer {
  border-top: 1px solid #efefef;
}
.i-dialog-div {
  max-height: 65vh;
  overflow-y: auto;
  overflow-x: hidden;
}

.dialog-footer > span {
  margin-left: 10px;
  margin-right: 10px;
}
</style>
