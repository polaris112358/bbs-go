<template>
  <div class="right-container">
    <post-btns v-if="isOwner" />

    <div class="widget">
      <div class="widget-header">
        个人资料
      </div>
      <div class="widget-content">
        <img :src="user.avatar" class="img-avatar" />
        <div class="nickname">
          <a :href="'/user/' + user.id">{{ user.nickname }}</a>
        </div>
        <div v-if="user.description" class="description">
          <p>{{ user.description }}</p>
        </div>
        <div v-if="user.type === 1">
          <img
            :src="
              'https://open.weixin.qq.com/qr/code?username=' + user.username
            "
          />
        </div>
        <ul v-if="isOwner" class="operations">
          <li>
            <i class="iconfont icon-edit" />
            <a href="/user/settings">&nbsp;编辑资料</a>
          </li>
          <li>
            <i class="iconfont icon-message" />
            <a href="/user/messages">&nbsp;消息</a>
          </li>
          <li>
            <i class="iconfont icon-favorites" />
            <a href="/user/favorites">&nbsp;收藏</a>
          </li>
        </ul>
      </div>
    </div>

    <div class="ad">
      <!-- 展示广告 -->
      <adsbygoogle ad-slot="1742173616" />
    </div>
  </div>
</template>

<script>
import PostBtns from '~/components/PostBtns'
export default {
  components: { PostBtns },
  props: {
    user: {
      type: Object,
      required: true
    },
    currentUser: {
      type: Object,
      required: false,
      default: null
    }
  },
  computed: {
    isOwner() {
      return (
        this.user && this.currentUser && this.user.id === this.currentUser.id
      )
    }
  }
}
</script>

<style lang="scss" scoped>
.nickname {
  font-size: 18px;
  font-weight: bold;
  a {
    color: #3273dc;
  }
}
.img-avatar {
  margin-top: 5px;
  border: 1px dotted #eeeeee;
  border-radius: 5%;
  width: 190px;
  height: 190px;
}
.description {
  font-size: 14px;
  padding: 10px 15px;
  border: 1px dotted #eeeeee;
  border-left: 3px solid #eeeeee;
  background-color: #fbfbfb;
}
.operations {
  list-style: none;
  margin-top: 8px;
  margin-left: 0px;

  li {
    padding-left: 3px;

    font-size: 13px;
    &:hover {
      cursor: pointer;
      background-color: #fcf8e3;
      color: #8a6d3b;
      font-weight: bold;
    }

    a {
      color: #3273dc;
    }
  }
}
</style>
