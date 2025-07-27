<template>
  <div class="set" @mouseenter="closeShow = true" @mouseleave="closeShow = false" @click.stop>
    <transition name="el-fade-in-linear">
      <close-one
        class="close"
        theme="filled"
        size="28"
        fill="#ffffff60"
        v-show="closeShow"
        @click="store.setOpenState = false"
      />
    </transition>
    <el-row :gutter="40" class="content-row">
      <el-col :span="12" class="left">
        <div class="logo text-hidden">
          <span class="bg">{{ siteBgName }}</span>
          <span class="sm">{{ siteSmName }}</span>
        </div>
        <div class="version">
          <div class="num">v&nbsp;{{ config.version }}</div>
          <el-tooltip content="主页使用的 Github 源代码仓库" placement="right" :show-arrow="false">
            <github-one class="github" theme="outline" size="24" @click="jumpTo(config.github)" />
          </el-tooltip>
        </div>
        <el-card class="update">
          <template #header>
            <div class="card-header">
              <span>更新日志</span>
            </div>
          </template>
          <div class="upnote">
            <div v-for="item in upData.new" :key="item" class="uptext">
              <add-one theme="outline" size="22" />
              {{ item }}
            </div>
            <div v-for="item in upData.fix" :key="item" class="uptext">
              <bug theme="outline" size="22" />
              {{ item }}
            </div>
          </div>
        </el-card>
      </el-col>
      <el-col :span="12" class="right">
        <div class="title">
          <setting-two theme="filled" size="28" fill="#ffffff60" />
          <span class="name">全局设置</span>
        </div>
        <Set />
      </el-col>
    </el-row>
  </div>
</template>

<script setup>
import { CloseOne, SettingTwo, GithubOne, AddOne, Bug } from "@icon-park/vue-next";
import { mainStore } from "@/store";
import Set from "@/components/Set.vue";
import config from "@/../package.json";

const store = mainStore();
const closeShow = ref(false);

// 站点名称
const siteBgName = import.meta.env.VITE_SIDE_BGNAME || "喵锵";
const siteSmName = import.meta.env.VITE_SIDE_SMNAME || "MiaowCham";

// 更新日志
const upData = reactive({
  new: [
    "采用 Vue 进行重构",
    "音乐歌单支持快速自定义",
    "壁纸支持个性化设置",
    "音乐播放器支持音量控制",
  ],
  fix: ["修复天气 API", "时光胶囊显示错误", "移动端动画及细节", "图标更换为 IconPark"],
});

// 跳转源代码仓库
const jumpTo = (url) => {
  window.open(url);
};
</script>

<style lang="scss" scoped>
.set {
  position: absolute;
  top: 50%;
  left: 50%;
  -webkit-transform: translate(-50%, -50%);
  transform: translate(-50%, -50%);
  width: 80%;
  height: 80%;
  background: rgb(255 255 255 / 40%);
  border-radius: 6px;
  padding: 40px;

  // 移动端全屏滚动布局
  @media (max-width: 720px) {
    position: fixed;
    top: 20px;
    left: 20px;
    right: 20px;
    bottom: 20px;
    transform: none;
    width: calc(100% - 40px);
    height: calc(100% - 40px);
    border-radius: 12px;
    padding: 20px;
    overflow-y: auto;
    background: rgb(255 255 255 / 40%);
    backdrop-filter: blur(10px);
  }

  .close {
    position: absolute;
    top: 14px;
    right: 14px;
    width: 32px;
    height: 32px;
    z-index: 1000;
    cursor: pointer;
    background: rgba(0, 0, 0, 0.3);
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: all 0.3s ease;

    &:hover {
      transform: scale(1.1);
      background: rgba(0, 0, 0, 0.5);
    }

    &:active {
      transform: scale(0.95);
    }
  }

  .content-row {
    height: 100%;
    flex-wrap: nowrap;

    // 移动端上下排布
    @media (max-width: 720px) {
      display: block;
      height: auto;
      
      .el-col {
        width: 100% !important;
        max-width: 100% !important;
        flex: none !important;
        padding-left: 20px !important;
        padding-right: 20px !important;
      }
    }
  }

  .el-row {
    height: 100%;
    flex-wrap: nowrap;

    .left {
      height: 100%;
      padding-left: 40px !important;
      padding-bottom: 20px;
      display: flex;
      flex-direction: column;
      justify-content: space-between;

      // 移动端样式调整
      @media (max-width: 720px) {
        height: auto;
        padding-left: 20px !important;
        padding-right: 20px !important;
        padding-bottom: 30px;
        margin-bottom: 20px;
        border-bottom: 1px solid rgba(255, 255, 255, 0.2);
      }

      .logo {
        transform: translateY(-8%);
        font-family: "Pacifico-Regular";
        padding-left: 22px;
        width: 100%;
        height: 260px;
        min-height: 140px;

        // 移动端样式调整
        @media (max-width: 720px) {
          transform: none;
          padding-left: 0;
          height: auto;
          min-height: auto;
          margin-bottom: 20px;
        }
        .bg {
          font-size: 5rem;
          font-family: "HarmonyOS-Black", "Pacifico-Regular", sans-serif;
        }

        .sm {
          margin-left: 6px;
          font-size: 2rem;
          font-family: "HarmonyOS-Black", "Pacifico-Regular", sans-serif;
        }

        @media (max-width: 990px) {
          .bg {
            font-size: 4.5rem;
          }
          .sm {
            font-size: 1.7rem;
          }
        }
        @media (max-width: 825px) {
          .bg {
            font-size: 3.8rem;
          }
          .sm {
            font-size: 1.3rem;
          }
        }
      }

      .version {
        display: flex;
        flex-direction: row;
        align-items: center;

        .num {
          font-size: 2rem;
          font-family: "Pacifico-Regular";
        }

        .github {
          width: 24px;
          height: 24px;
          margin-left: 12px;
          margin-top: 6px;

          &:hover {
            transform: scale(1.2);
          }
        }
      }

      .update {
        margin-top: 30px;
        height: 100%;

        // 移动端高度调整
        @media (max-width: 720px) {
          height: auto;
          max-height: 300px;
        }

        :deep(.el-card__body) {
          height: 100%;

          // 移动端高度调整
          @media (max-width: 720px) {
            height: auto;
            max-height: 240px;
          }

          .upnote {
            padding: 20px;
            height: calc(100% - 56px);
            overflow-y: auto;

            // 移动端高度调整
            @media (max-width: 720px) {
              height: auto;
              max-height: 180px;
            }

            .uptext {
              display: flex;
              flex-direction: row;
              align-items: center;
              padding-bottom: 16px;

              &:nth-last-of-type(1) {
                padding: 0;
              }

              .i-icon {
                width: 22px;
                height: 22px;
                margin-right: 8px;
              }
            }
          }
        }
      }
    }

    .right {
      height: 100%;
      padding-right: 40px !important;
      display: flex;
      flex-direction: column;
      justify-content: center;

      // 移动端样式调整
      @media (max-width: 720px) {
        height: auto;
        padding-left: 20px !important;
        padding-right: 20px !important;
        justify-content: flex-start;
        padding-top: 20px;
      }

      .title {
        display: flex;
        align-items: center;
        flex-direction: row;
        font-size: 18px;
        margin-bottom: 16px;

        .i-icon {
          width: 28px;
          height: 28px;
          margin-right: 6px;
        }
      }
    }
  }
}
</style>
