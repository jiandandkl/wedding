<template>
  <div class="page">
    <img
      class="bg-img"
      src='/static/images/banner.jpg'
      background-size="cover"
    >
    <div v-if="num">
      <div class="name">{{name}}，您好！您的座位是:</div>
      <div class="num">{{num}}号桌</div>
    </div>
    <div v-else>
      <div class="welcome">&nbsp;贵宾，您好！</div>
      <input
        class="welcome-input"
        v-model="name"
        placeholder-style="color:#b60201;text-align:center"
        placeholder="请输入您的姓名">
      <button @click="search" :data="name" class="welcome-btn">查看座位</button>
    </div>
    <div v-if="num" class="table-map">
      <div class="table-title">座位示意图</div>
      <div class="stage-row">舞台</div>
      <div class="stage-column"></div>
      <div class="entrance">入口</div>
      <div class="tables tables-row table-one">
        <div v-for="(item, index) in [1,7,11]" :key="index" class="table-item {{}}" :class="[item === num ? 'table-select' : '']">{{item}}</div>
      </div>
      <div class="tables tables-row table-two">
        <div v-for="(item, index) in [2,8,12]" :key="index" class="table-item" :class="[item === num ? 'table-select' : '']">{{item}}</div>
      </div>
      <div class="tables tables-row table-three">
        <div v-for="(item, index) in [5,9,15]" :key="index" class="table-item" :class="[item === num ? 'table-select' : '']">{{item}}</div>
      </div>
      <div class="tables tables-row table-four">
        <div v-for="(item, index) in [6,10,16]" :key="index" class="table-item" :class="[item === num ? 'table-select' : '']">{{item}}</div>
      </div>
      <div class="tables tables-four table-five">
        <div v-for="(item, index) in [18,19,22,25]" :key="index" class="table-item" :class="[item === num ? 'table-select' : '']">{{item}}</div>
      </div>
      <div class="tables tables-four table-six">
        <div v-for="(item, index) in [20,21,26,27]" :key="index" class="table-item" :class="[item === num ? 'table-select' : '']">{{item}}</div>
      </div>
      <div class="tables table-item table-seven">17</div>
    </div>
  </div>
</template>

<script>
import guest from '../../../static/guest'

export default {
  data () {
    return {
      name: '',
      num: '',
      guest
    }
  },

  methods: {
    search () {
      const trimName = this.name.toString().trim()
      const tableNum = this.guest[trimName]
      if (tableNum) {
        this.num = tableNum
      } else {
        wx.showToast({
          title: `输入有误或未查到座位， 请联系夏友鱼`,
          icon: 'none',
          duration: 2000
        })
      }
    }
  },

  onShareAppMessage () {
    return {
      title: '对号入座',
      path: '/pages/index/index'
    }
  }
}
</script>

<style scoped>

.page {
  padding-bottom: 1.2rem;
}

.name {
  color: #b60201;
  text-align: center;
  font-size: 0.4rem;
  margin-top: .4rem;
}

.num {
  color: #b60201;
  text-align: center;
  font-size: 0.6rem;
  margin-top: 0.6rem;
  font-weight: 700;
}

.bg-img {
  width: 100%;
  height: 9.66rem;
}

.table-map {
  position: relative;
  margin: 0 auto;
  margin-top: 0.66rem;
  width: 7.1rem;
  height: 9.5rem;
  box-shadow:0px 2px 5px #aaa;
  padding-top: .34rem;
}

.table-title {
  font-size: 0.4rem;
  color: #b60201;
  text-align: center;
}

.stage-row {
  background-color: #ed8a8a;
  color: #fff;
  font-size: 0.3rem;
  width: 5rem;
  height: 0.6rem;
  line-height: 0.6rem;
  margin: 0 auto;
  margin-top: .45rem;
  text-align: center;
}

.stage-column {
  width: 0.65rem;
  height: 4.08rem;
  background-color: #ed8a8a;
  margin: 0 auto;
}

.entrance {
  border-top: 2px solid #b60201;
  border-bottom: 2px solid #b60201;
  color: #b60201;
  width: 0.6rem;
  margin-top: 0.5rem;
  font-size: .3rem;
  margin-left: .2rem;
  margin-bottom: .35rem;
}

.tables {
  position: absolute;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.tables-row {
  width: .86rem;
  height: 3.3rem;
}

.table-one {
  top: 2.56rem;
  left: .6rem;
}

.table-two {
  top: 2.16rem;
  left: 1.86rem;
}

.table-three {
  top: 2.16rem;
  left: 4.35rem;
}

.table-four {
  top: 2.56rem;
  right: .6rem;
}

.table-item {
  width: .85rem;
  height: .85rem;
  line-height: 0.85rem;
  text-align: center;
  border-radius: 50%;
  border: 1px solid #b60201;
}

.tables-four {
  width: 2.12rem;
  flex-wrap: wrap;
  flex-direction: row;
}

.tables-four .table-item {
  margin-bottom: .38rem;
}

.table-five {
  left: 0.6rem;
}

.table-six {
  right: .6rem;
}

.table-seven {
  right: 1.25rem;
  top: 6.15rem;
}

.table-select {
  color: #fff;
  background-color: #b60201;
}

.welcome {
  font-size: .46rem;
  color: #b60201;
  text-align: center;
  margin-bottom: .4rem;
  margin-top: .3rem;
}

.phcolor {
  color: #b60201;
}

input-placeholder {
  text-align: center;
}

.welcome-input {
  border-radius: .5rem;
  border: 2px solid #b60201;
  width: 3.6rem;
  height: .84rem;
  margin: 0 auto;
  margin-bottom: .45rem;
  padding: 0 0.2rem;
  color: #b60201;
}

.welcome-btn {
  width: 4rem;
  border-radius: .5rem;
  background-color: #b60201;
  color: #fff;
}

</style>
