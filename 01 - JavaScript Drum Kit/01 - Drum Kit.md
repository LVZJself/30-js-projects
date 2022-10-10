## 01 - Drum Kit

将实现功能分为两部分

1. 页面监听到 keydown 事件，触发 playSound 函数

   playSound 函数通过 监听到的 keyCode 来绑定实际按下的按钮

   完成 对应图片的样式改变 和 对应音频的播放

   ```javascript
   function playSound(e) {
       const audio = document.querySelector(`audio[data-key="${e.keyCode}"]`);//模板字符串
       const key = document.querySelector(`div[data-key="${e.keyCode}"]`);
       //无关按键及时退出
       if (!audio) return;
       if (!key) return;
       key.classList.add('playing');
       audio.currentTime = 0;//保证连续按键的声音
       audio.play();
   }
   
   // 监听页面的keydown事件，触发playAudio函数。
   window.addEventListener('keydown', playSound);
   ```

2. 监听到 transitionend 事件，动画结束后会触发 removeTransition 函数

   解绑添加的样式

   ```javascript
   function removeTransition(e) {
       //一次按键多个样式属性发生transition，但我们只需要清除一次样式。eg：box-shadow, transform, border-color
       if (e.propertyName !== 'transform') return;
       e.target.classList.remove('playing');
   }
     
   const keys = Array.from(document.querySelectorAll('.key'));
   keys.forEach(key => key.addEventListener('transitionend',removeTransition));  
   ```

   

