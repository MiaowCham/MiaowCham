<template>
  <footer id="footer" :class="store.footerBlur ? 'blur' : null">
    <Transition name="fade" mode="out-in">
      <div v-if="!store.playerState || !store.playerLrcShow" class="power">
        <div class="copyright-line">
          <span>
            <span :class="startYear < fullYear ? 'c-hidden' : 'hidden'">Copyright&nbsp;</span>
            &copy;
            <span v-if="startYear < fullYear"
              class="site-start">
              {{ startYear }}
              -
            </span>
            {{ fullYear }}
            <a :href="siteUrl">{{ siteAuthor }}</a>
          </span>
          &
          <!-- 以下信息请不要修改哦 -->
          <span class="hidden">
            Made&nbsp;by
            <a :href="config.github" target="_blank">
              {{ config.author }}
            </a>
          </span>
        </div>
        <!-- 站点备案 -->
        <div v-if="siteIcp" class="icp-line">
          <span v-if="!siteIcpSide">
            {{ siteIcp }}
          </span>
          <a v-else :href="siteIcpSide" target="_blank">
            {{ siteIcp }}
          </a>
        </div>
      </div>
      <div v-else class="lrc">
        <Transition name="fade" mode="out-in">
          <div class="lrc-all" :key="displayLrc">
            <music-one theme="filled" size="18" fill="#efefef" />
            <span class="lrc-text" v-html="displayLrc" />
            <music-one theme="filled" size="18" fill="#efefef" />
          </div>
        </Transition>
      </div>
    </Transition>
  </footer>
</template>

<script setup>
import { MusicOne } from "@icon-park/vue-next";
import { mainStore } from "@/store";
import config from "@/../package.json";

const store = mainStore();
const fullYear = new Date().getFullYear();

// 歌词字符数限制
const maxLrcLength = ref(50); // 默认限制50个字符

// 根据屏幕宽度调整字符数限制
const updateMaxLength = () => {
  const width = window.innerWidth;
  if (width <= 480) {
    maxLrcLength.value = 20; // 小屏幕限制20个字符
  } else if (width <= 720) {
    maxLrcLength.value = 30; // 中等屏幕限制30个字符
  } else {
    maxLrcLength.value = 50; // 大屏幕限制50个字符
  }
};

// 处理歌词显示的计算属性
const displayLrc = computed(() => {
  const lrc = store.getPlayerLrc;
  if (!lrc || lrc.length <= maxLrcLength.value) {
    return lrc;
  }
  return lrc.substring(0, maxLrcLength.value) + '...';
});

// 监听窗口大小变化
onMounted(() => {
  updateMaxLength();
  window.addEventListener('resize', updateMaxLength);
});

onBeforeUnmount(() => {
  window.removeEventListener('resize', updateMaxLength);
});

// 加载配置数据
// const siteStartDate = ref(import.meta.env.VITE_SITE_START);
const startYear = ref(
  import.meta.env.VITE_SITE_START?.length >= 4 ? 
  import.meta.env.VITE_SITE_START.substring(0, 4) : null
);
const siteIcp = ref(import.meta.env.VITE_SITE_ICP);
const siteIcpSide = ref(import.meta.env.VITE_SITE_ICP_SIDE);
const siteAuthor = ref(import.meta.env.VITE_SITE_AUTHOR);
const siteUrl = computed(() => {
  const url = import.meta.env.VITE_SITE_LINK;
  if (!url) return "https://www.imsyy.top";
  // 判断协议前缀
  if (!url.startsWith("http://") && !url.startsWith("https://")) {
    return "//" + url;
  }
  return url;
});
</script>

<style lang="scss" scoped>
#footer {
  width: 100%;
  position: absolute;
  bottom: 0;
  left: 0;
  height: 60px;
  text-align: center;
  z-index: 0;
  font-size: 14px;
  // 文字不换行
  word-break: keep-all;
  white-space: nowrap;
  display: flex;
  align-items: center;
  justify-content: center;
  .power {
    animation: fade 0.3s;
    .copyright-line {
      line-height: 20px;
      margin-bottom: 4px;
    }
    .icp-line {
      line-height: 20px;
      font-size: 12px;
      opacity: 0.8;
    }
  }
  .lrc {
    padding: 0 20px;
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
    .lrc-all {
      width: 98%;
      display: flex;
      flex-direction: row;
      justify-content: center;
      align-items: center;
      .lrc-text {
        margin: 0 8px;
      }
      .i-icon {
        width: 18px;
        height: 18px;
        display: inherit;
      }
    }
  }
  &.blur {
    backdrop-filter: blur(10px);
    background: rgb(0 0 0 / 25%);
    font-size: 16px;
  }
  .fade-enter-active,
  .fade-leave-active {
    transition: opacity 0.15s ease-in-out;
  }
  @media (max-width: 720px) {
    font-size: 0.9rem;
    &.blur {
      font-size: 0.9rem;
    }
  }
  @media (max-width: 560px) {
    .c-hidden {
      display: none;
    }
  }
  @media (max-width: 480px) {
    .hidden {
      display: none;
    }
  }
}
</style>
