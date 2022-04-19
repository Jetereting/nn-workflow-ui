<template>
  <div
    :class="[
      node.type === 'start'
        ? 'node-wrap-box node_sid-startevent start-node'
        : 'node-wrap-box',
    ]"
  >
    <div>
      <div
        class="title newTitle"
        data-spm-anchor-id="0.0.0.i2.2f244490ZxXSWD"
        :style="titlebg"
      >
        <span class="iconfont">
          <svg
            class=""
            viewBox="64 64 896 896"
            fill="currentColor"
            aria-hidden="true"
            width="1em"
            height="1em"
          >
            <path :d="icon" />
          </svg>
        </span>
        <span
          class="editable-title"
          style="margin-left:5px"
          data-spm-anchor-id="0.0.0.i53.2f244490UdKR44"
        >{{ nodetype }}</span>
        <i
          aria-label="icon: close"
          tabindex="-1"
          class="anticon anticon-close close newClose"
          @click="delNode"
        ><svg
          viewBox="64 64 896 896"
          focusable="false"
          class=""
          data-icon="close"
          width="1em"
          height="1em"
          fill="currentColor"
        >
          <path
            d="M563.8 512l262.5-312.9c4.4-5.2.7-13.1-6.1-13.1h-79.8c-4.7 0-9.2 2.1-12.3 5.7L511.6 449.8 295.1 191.7c-3-3.6-7.5-5.7-12.3-5.7H203c-6.8 0-10.5 7.9-6.1 13.1L459.4 512 196.9 824.9A7.95 7.95 0 0 0 203 838h79.8c4.7 0 9.2-2.1 12.3-5.7l216.5-258.1 216.5 258.1c3 3.6 7.5 5.7 12.3 5.7h79.8c6.8 0 10.5-7.9 6.1-13.1L563.8 512z"
          /></svg></i>
      </div>
      <div
        class="content"
        @click="isShowDialog()"
      >
        <template v-if="content == '所有人' || content == '选择审批人'">
          {{ content }}
        </template>
        <template v-else>
          <div
            v-for="(item, index) in content"
            :key="index"
            class="text"
          >
            <div class="">
              <p>
                <span v-show="item.needSameDept == 1">同部门下的</span>{{ item.labelNames }}
              </p>
            </div>
          </div>
        </template>

        <i
          v-show="!(this.node.type == 'start')"
          aria-label="icon: right"
          class="anticon anticon-right arrow"
        ><svg
          viewBox="64 64 896 896"
          focusable="false"
          class=""
          data-icon="right"
          width="1em"
          height="1em"
          fill="currentColor"
          aria-hidden="true"
        >
          <path
            d="M765.7 486.8L314.9 134.7A7.97 7.97 0 0 0 302 141v77.3c0 4.9 2.3 9.6 6.1 12.6l360 281.1-360 281.1c-3.9 3-6.1 7.7-6.1 12.6V883c0 6.7 7.7 10.4 12.9 6.3l450.8-352.1a31.96 31.96 0 0 0 0-50.4z"
          /></svg></i>
      </div>
    </div>
    <AddNodeApprover
      :dialog.sync="dialog"
      :properties="node.properties"
      @setProperties="setProperties"
    />
  </div>
</template>
<script>
import AddNodeApprover from './add-node-approver'
export default {
  name: 'NodeWrapBox',
  components: {
    AddNodeApprover
  },
  props: {
    node: {
      type: Object,
      default: Object
    }
  },
  data: () => ({
    newList: [],
    isClick: false,
    dialog: false,
    text: '请选择',
    titlebg: 'background: rgb(87, 106, 149);',
    nodetype: '发起人',
    content: '选择审批人',
    icon:
      'M857.38719 501.122873l32.092376 55.372292-462.704913 268.054249-32.092376-55.372292 462.704913-268.054249zM214.687739 272.628103a74.666667 74.666667 0 0 1 56.108377-10.59344l349.700121 72.962378 25.42413-16.550783a256 256 0 0 1 200.607216-34.234109l7.340895 1.920136 33.304979 9.173915a62.784 62.784 0 0 1 17.808365 112.93566l-3.142878 1.93771-565.500618 326.294865a64 64 0 0 1-62.81291 0.644848l-3.608286-2.153736-116.500307-74.381783a51.178667 51.178667 0 0 1-5.80794-81.95298l2.726317-2.189881 40.021527-29.880682a64 64 0 0 1 38.67169-12.720002l4.636771 0.180458L306.447943 539.764106l63.58375-41.464382-183.853702-86.16662a66.282667 66.282667 0 0 1-33.502513-84.438721l1.602898-3.709032a66.282667 66.282667 0 0 1 23.743377-27.355265zM228.654476 597.832534l-25.165422 18.790878 100.878414 64.433205 562.921897-324.830673-30.46755-8.398012a192 192 0 0 0-155.943322 24.212909L323.148023 605.254826l-94.493547-7.422292zM249.719766 326.18002l-36.695129 23.994174a2.282667 2.282667 0 0 0 0.277033 3.978501l219.777991 102.991981 111.431983-72.636812-286.786137-59.821493a10.666667 10.666667 0 0 0-6.543342 0.698599L249.719766 326.18002z'
  }),
  mounted () {
    this.setText()
  },
  methods: {
    // 初始禁止点击
    isShowDialog () {
      if (this.node.type === 'start') {
        this.dialog = false
      } else {
        this.dialog = true
      }
    },
    delNode () {
      this.$emit('delNode')
    },
    addApprover () {
      this.dialog = true
    },
    setProperties (properties) {
      this.content = properties.actionerRules
      this.node.properties = properties
      this.setText()
    },
    setText () {
      switch (this.node.type) {
        case 'start':
          this.content = '所有人'
          break
        case 'approver':
          this.nodetype = '审批人'
          this.titlebg = 'background: rgb(255, 148, 62);'
          this.icon =
            'M644.8 581.568l160.64 187.456A64 64 0 0 1 756.842667 874.666667H267.157333a64 64 0 0 1-48.597333-105.642667l160.661333-187.434667c18.922667 11.52 39.466667 20.629333 61.205334 26.944L267.157333 810.666667H480v-128h64v128h212.842667l-173.269334-202.133334a254.613333 254.613333 0 0 0 61.226667-26.965333zM512 149.333333c117.824 0 213.333333 95.509333 213.333333 213.333334s-95.509333 213.333333-213.333333 213.333333-213.333333-95.509333-213.333333-213.333333S394.176 149.333333 512 149.333333z m0 64a149.333333 149.333333 0 1 0 0 298.666667 149.333333 149.333333 0 0 0 0-298.666667z'
          break
        case 'notifier':
          this.nodetype = '抄送人'
          this.titlebg = 'background: rgb(50, 150, 250)'
          this.icon =
            'M309.461333 205.994667a68.778667 68.778667 0 0 1 34.965334 18.837333l153.813333 153.813333 0.042667-0.085333 45.248 45.248-0.064 0.085333 161.557333 161.557334 0.064-0.085334 45.269333 45.290667-168.490666 168.533333c-48.597333 48.576-129.792 46.208-181.333334-5.333333L88.021333 481.28c-25.792-25.770667-26.986667-66.346667-2.688-90.666667a59.818667 59.818667 0 0 1 33.92-16.810666l102.912-14.805334 14.784-102.912c4.992-34.709333 37.461333-57.130667 72.533334-50.090666z m-11.690666 62.698666l-19.413334 146.496-146.538666 19.413334L446.848 749.653333c25.962667 25.962667 66.432 27.626667 90.368 3.690667l122.581333-122.602667-362.026666-362.026666z m525.44-3.84l101.205333 101.248a64 64 0 0 1 0 90.517334l-143.872 143.872-45.290667-45.290667 143.914667-143.850667-101.226667-101.226666a85.333333 85.333333 0 0 0-120.682666 0l-83.562667 83.52-45.226667-45.248 83.541334-83.52a149.333333 149.333333 0 0 1 211.2 0z'
          break
        default:
      }
      if (this.node.properties && this.node.properties.actionerRules) {
        this.content = this.node.properties.actionerRules
      }
    }
  }
}
</script>
