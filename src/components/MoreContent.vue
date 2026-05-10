<template>
  <div class="more-content">
    <div class="content-wrapper">
      <div class="readme-link">
        <a href="https://github.com/MiaowCham/MiaowCham/blob/main/README.md" target="_blank">
          📄 README.md
        </a>
      </div>
      <h3 style="margin-top: 10px;">Hi there 👋 I'm 喵锵 (MiaowCham)</h3>
      
      <div class="note-box">
        <strong>Note</strong><br></br> My English isn't perfect—I use translation tools sometimes, But I will work hard to learn it.😄
      </div>
      
      <p>My name is 喵锵 (MiaowCham). In fact, I got this name from looking it up in the dictionary 💦</p>
      <p>I'm a passionate open-source enthusiast from Zhejiang, China. As a hobbyist developer, I hope my project can help some people.🙏</p>
      <p>However, in the latter half of the year, I'll be heading to Qingdao, Shandong, China to continue my education, so I may not be as active in the community as before 🥲 But don't worry—I'm sure I'll be back soon!</p>
      
      <h2>🥰 What I'm Into</h2>
      <ul>
        <li>📃 I'm using Markdown and a static site generator to build <a href="https://miaowcham.com/" rel="nofollow">My Personal Website</a>.</li>
        <li>🔭 I'm currently working on AI projects.</li>
        <li>⬇️ I like to use Markdown to create documents.</li>
        <li>🐍 I'm trying to self-learn Python through AI and complete some projects.</li>
        <li>📺 I might post some videos on <a href="https://space.bilibili.com/485769432" target="_blank">Bilibili</a>.</li>
      </ul>
      
      <h2>📫 How to reach me:</h2>
      <ul>
        <li>📧 Email: <a href="mailto:mcyyds1234@outlook.com" target="_blank">mcyyds1234@outlook.com</a></li>
        <li>📧 QQMail: <a href="mailto:qq@miaowcham.com" target="_blank">qq@miaowcham.com</a></li>
        <li>🐧 QQ: <a href="https://qm.qq.com/q/qjU8Nm72fe" target="_blank">2049669820</a></li>
        <li>✈️ Telegram: <a href="https://t.me/miaowcham" target="_blank">@MiaowCham</a></li>
      </ul>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.more-content {
  display: flex;
  align-items: flex-start;
  justify-content: center;
  margin-top: 20px;
  width: 100%;
  height: 100%;
  overflow: hidden;
}

.content-wrapper {
  max-width: 800px;
  width: 100%;
  height: 100%;
  overflow-y: auto;
  padding: 20px;
  box-sizing: border-box;
  background: rgba(0, 0, 0, 0.3);
  border-radius: 12px;
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  position: relative;
  
  /* 自定义滚动条样式 */
  &::-webkit-scrollbar {
    width: 8px;
  }
  
  &::-webkit-scrollbar-track {
    background: rgba(255, 255, 255, 0.1);
    border-radius: 4px;
  }
  
  &::-webkit-scrollbar-thumb {
    background: rgba(255, 255, 255, 0.3);
    border-radius: 4px;
    
    &:hover {
      background: rgba(255, 255, 255, 0.5);
    }
  }
  
  h2, h3 {
    color: #fff;
    margin: 20px 0 10px 0;
    
    &:first-child {
      margin-top: 0;
    }
  }
  
  h3 {
    font-size: 1.5em;
    border-bottom: 2px solid rgba(255, 255, 255, 0.3);
    padding-bottom: 10px;
  }
  
  h2 {
    font-size: 1.3em;
  }
  
  p {
    color: rgba(255, 255, 255, 0.9);
    line-height: 1.6;
    margin: 15px 0;
  }
  
  ul {
    color: rgba(255, 255, 255, 0.9);
    padding-left: 20px;
    
    li {
      margin: 8px 0;
      line-height: 1.5;
    }
  }
  
  a {
    color: #64b5f6;
    text-decoration: none;
    transition: color 0.3s ease;
    
    &:hover {
      color: #90caf9;
      text-decoration: underline;
    }
  }
  
  .note-box {
     background: rgba(33, 150, 243, 0.2);
     border: 1px solid rgba(33, 150, 243, 0.4);
     border-radius: 8px;
     padding: 15px;
     margin: 15px 0;
     color: rgba(255, 255, 255, 0.9);
     
     strong {
       color: #64b5f6;
     }
   }
   
   .readme-link {
     position: absolute;
     top: 0;
     left: 0;
     z-index: 10;
     
     a {
       display: inline-block;
       color: rgba(255, 255, 255, 0.6);
       text-decoration: none;
       font-size: 0.75em;
       font-family: 'Courier New', monospace;
       padding: 4px 8px;
       background: rgba(0, 0, 0, 0.2);
       border-radius: 0 0 6px 0;
       transition: color 0.2s ease;
       
       &:hover {
         color: rgba(255, 255, 255, 0.9);
       }
     }
   }
}
</style>
