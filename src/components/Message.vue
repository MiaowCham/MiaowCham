<template>
  <!-- 基本信息 -->
  <div class="message">
    <!-- Logo -->
    <div class="logo">
      <img class="logo-img" :src="siteLogo" alt="logo" />
      <div :class="{ name: true, long: siteBgName.length >= 6 }">
        <span class="bg">{{ siteBgName }}</span>
        <span class="sm">{{ siteSmName }}</span>
      </div>
    </div>
    <!-- 简介 -->
    <div class="description cards" @click="changeBox">
      <div class="content">
        <Icon size="16">
          <QuoteLeft />
        </Icon>
        <Transition name="fade" mode="out-in">
          <div :key="hitokotoData.text + hitokotoData.from" class="text">
            <p>{{ hitokotoData.text }}</p>
            <div class="from">—— {{ hitokotoData.from }}</div>
          </div>
        </Transition>
        <Icon size="16">
          <QuoteRight />
        </Icon>
      </div>
    </div>
  </div>
</template>

<script setup>
import { Icon } from "@vicons/utils";
import { QuoteLeft, QuoteRight } from "@vicons/fa";
import { Error } from "@icon-park/vue-next";
import { getHitokoto } from "@/api";
import { mainStore } from "@/store";
const store = mainStore();

// 组件挂载时获取一言数据
onMounted(() => {
  getHitokotoData();
});

// 主页站点logo
const siteLogo = import.meta.env.VITE_SITE_MAIN_LOGO;
// 站点名称
const siteBgName = import.meta.env.VITE_SIDE_BGNAME || "喵锵";
const siteSmName = import.meta.env.VITE_SIDE_SMNAME || "MiaowCham";

// 一言数据
const hitokotoData = reactive({
  text: "这里应该显示一句话",
  from: "無名",
});

// 简介区域文字
const descriptionText = reactive({
  hello: import.meta.env.VITE_DESC_HELLO,
  text: import.meta.env.VITE_DESC_TEXT,
});

// 获取一言数据
const getHitokotoData = async () => {
  try {
    const result = await getHitokoto();
    hitokotoData.text = result.hitokoto;
    hitokotoData.from = result.from;
  } catch (error) {
    ElMessage({
      message: "一言获取失败",
      icon: h(Error, {
        theme: "filled",
        fill: "#efefef",
      }),
    });
    hitokotoData.text = "奋力的奔跑吧，让自己成为明日的朝阳";
    hitokotoData.from = "曜辰";
  }
};

// 切换右侧功能区
const changeBox = () => {
  if (store.getInnerWidth >= 721) {
    store.boxOpenState = !store.boxOpenState;
  } else {
    // 移动端：关闭移动端菜单，打开盒子作为独立页面
    store.mobileOpenState = false;
    store.boxOpenState = true;
  }
};

// 监听状态变化
watch(
  () => store.boxOpenState,
  (value) => {
    if (value) {
      descriptionText.hello = import.meta.env.VITE_DESC_HELLO_OTHER;
      descriptionText.text = import.meta.env.VITE_DESC_TEXT_OTHER;
    } else {
      descriptionText.hello = import.meta.env.VITE_DESC_HELLO;
      descriptionText.text = import.meta.env.VITE_DESC_TEXT;
    }
  },
);
</script>

<style lang="scss" scoped>
.message {
  .logo {
    display: flex;
    flex-direction: row;
    align-items: center;
    animation: fade 0.5s;
    max-width: 460px;
    .logo-img {
      border-radius: 70%;
      width: 140px;
    }
    .name {
      width: 100%;
      padding-left: 22px;
      transform: translateY(-8px);
      font-family: "Pacifico-Regular";

      .bg {
        font-size: 5rem;
        font-family: "HarmonyOS-Black", "Pacifico-Regular", sans-serif;
      }

      .sm {
        margin-left: 6px;
        margin-right: 20px;
        font-size: 2rem;
        font-family: "HarmonyOS-Black", "Pacifico-Regular", sans-serif;
        @media (min-width: 721px) and (max-width: 750px) {
          display: none;
        }
      }
    }
    @media (max-width: 768px) {
      .logo-img {
        width: 120px;
      }
      .name {
        height: 128px;
        .bg {
          font-size: 4.5rem;
          font-family: "HarmonyOS-Black", "Pacifico-Regular", sans-serif;
        }
      }
    }

    @media (max-width: 720px) {
      max-width: 100%;
    }
  }

  .description {
    padding: 1rem;
    margin-top: 3.5rem;
    max-width: 460px;
    animation: fade 0.5s;

    .content {
      display: flex;
      align-items: flex-start;

      .text {
        margin: 0.75rem 1rem;
        line-height: 2rem;
        flex: 1;
        transition: opacity 0.2s;

        p {
          &:nth-of-type(1) {
            font-family: "Pacifico-Regular";
          }
        }
        
        .from {
          font-size: 0.9rem;
          opacity: 0.8;
          margin-top: 0.5rem;
          text-align: right;
          width: 100%;
          display: block;
        }
      }

      .xicon:nth-of-type(2) {
        align-self: flex-end;
      }
    }
    @media (max-width: 720px) {
      max-width: 100%;
    }
  }
  @media (max-width: 400px) {
    .logo {
      flex-direction: column;
      align-items: center;
      text-align: center;
      .logo-img {
         width: 150px;
         margin-bottom: 1rem;
       }
      .name {
         padding-left: 0;
         height: auto;
         transform: none;
         text-align: center;
         width: 100%;
         display: flex;
         flex-direction: column;
         align-items: center;
         .bg {
           font-size: 3.5rem;
         }
         .sm {
           font-size: 1.4rem;
           margin-left: 0;
           margin-right: 0;
         }
       }
    }
    .description {
      margin-top: 1rem;
    }
  }
  @media (max-width: 390px) {
    .logo {
      .name {
         .bg {
           font-size: 3rem;
         }
         .sm {
           font-size: 1.2rem;
         }
       }
    }
  }
}
</style>
