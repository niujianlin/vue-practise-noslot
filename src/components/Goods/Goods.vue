<template>
  <div class="goods-container">
    <!-- 左侧图片 -->
    <div class="thumb">
      <div class="custom-control custom-checkbox">
        <!-- 复选框 -->
        <input type="checkbox" class="custom-control-input" :id="'sel' + id" :checked="state" 
        @change="stateChange"/>
        <!-- 上面的:id,这里的:for绑定什么字符都行的，只要动态绑定即可 -->
        <label class="custom-control-label" :for="'sel' + id">
          <!-- 商品的缩略图 -->
          <img :src="pic" alt="" />
        </label>
      </div>
    </div>
    <!-- 右侧信息区域 -->
    <div class="goods-info">
      <!-- 商品标题 -->
      <h6 class="goods-title">{{ title }}</h6>
      <div class="goods-info-bottom">
        <!-- 商品价格 -->
        <span class="goods-price">￥{{ price }}</span>
        <!-- 商品的数量 -->
        <Counter :cnt="count" :id="id"></Counter>
      </div>
    </div>
  </div>
</template>

<script>
import Counter from '@/components/Counter/Counter.vue'

export default {
  props: {
    id: {
      required: true,
      type: Number
    },
    // 要渲染的商品标题
    title: {
      default: '',
      type: String
    },
    pic: {
      default: '',
      type: String
    },
    price: {
      default: 0,
      type: Number
    },
    state: {
      default: true,
      type: Boolean
    },
    count: {
      default: 0,
      type: Number
    }
  },
  methods: {
    //复选框状态变化时，子向父传值，e是触发的事件，里面记录了当前复选框id对应的各种属性
    stateChange(e) {
      console.log(e)
      const newState = e.target.checked
      // console.log(newState)
      this.$emit('state-change', {id: this.id, value: newState})
    }
  },
  components: {
    Counter,
  }
}
</script>

<style lang="less" scoped>
.goods-container {
  + .goods-container {
    border-top: 1px solid #efefef;
  }
  padding: 10px;
  display: flex;
  .thumb {
    display: flex;
    align-items: center;
    img {
      width: 100px;
      height: 100px;
      margin: 0 10px;
    }
  }

  .goods-info {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    flex: 1;
    .goods-title {
      font-weight: bold;
      font-size: 12px;
    }
    .goods-info-bottom {
      display: flex;
      justify-content: space-between;
      .goods-price {
        font-weight: bold;
        color: red;
        font-size: 13px;
      }
    }
  }
}
</style>
