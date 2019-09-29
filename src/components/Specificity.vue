<template>
  <div class="specificity">
    <header class="header">
      <h2>CSS 权重计算</h2>
      <button @click="sortSpecificity">权重排序</button>
    </header>
    <p style="fontSize:10px;color:lightblue; margin-bottom: 2vh; textAlign:left; display:none;">
      注意，因为这里的
      <i style="color: red">transition-group</i>
      使用的是字符串作为key值，所以为了保证页面的运行，希望使用过程，保证每个字符串不同</p>
    <div class="container">
      <ul>
        <transition-group
          name="fade"
          appear
          tag="ul"
        >
          <li
            v-for="(item, index) in exlist"
            :key="index"
          >
            <div class="item">
              <div class="input-wrapper">
                <textarea
                  class="input"
                  :rows="
                    exlist[index].str.match(/\n/g) ? exlist[index].str.match(/\n/g).length+1 : 1"
                  title="输入 CSS 选择器"
                  autocomplete="off"
                  autocorrect="off"
                  v-model="exlist[index].str"
                  @input="calculate(index)"
                ></textarea>
              </div>
              <div class="calculate">
                <dl class="id-select">
                  <dt style="background: #ff4351;">{{exlist[index].specificityArray[0] || 0}}</dt>
                  <dd>ID选择器</dd>
                </dl>
                <dl class="class-select">
                  <dt style="background: #7b72e9;">{{exlist[index].specificityArray[1] || 0}}</dt>
                  <dd>class 选择器、属性选择器(type="text") 伪类选择器(:hover)</dd>
                </dl>
                <dl class="element-select">
                  <dt style="background: #feae1b;">{{exlist[index].specificityArray[2] || 0}}</dt>
                  <dd>元素选择器（包括伪元素:before)</dd>
                </dl>
              </div>
              <div class="operator">
                <button
                  class="delelte"
                  v-if="index !== 0"
                  @click="deleteExlist(index)"
                >-</button>
                <button
                  class="add"
                  @click="addExlist(index)"
                >+</button>
              </div>
            </div>
          </li>
        </transition-group>
      </ul>
    </div>
    <footer class="footer">
      权重计算主要由<a style="color:red;" href="https://www.npmjs.com/package/specificity">https://www.npmjs.com/package/specificity</a>该包提供，可以使用<code style="color: white;">yarn add specificity</code>来安装
    </footer>
  </div>
</template>

<script>
import { calculate, compare } from 'specificity';

export default {
  name: 'Specificity',
  data() {
    return {
      exlist: [{
        str: '#div',
        specificityArray: [1, 0, 0],
      }],
    };
  },
  methods: {
    calculate(index) {
      const obj = calculate(this.exlist[index].str)[0];
      if (obj && obj.specificityArray) {
        this.exlist[index].specificityArray = [...obj.specificityArray.slice(1)];
      }
    },
    addExlist(index) {
      this.exlist.splice(index + 1, 0, {
        str: '#div',
        specificityArray: [1, 0, 0],
      });
    },
    deleteExlist(index) {
      this.exlist.splice(index, 1);
    },
    sortSpecificity() {
      this.exlist.sort((a, b) => compare(b.str, a.str));
    },
  },
};
</script>

<style scoped>
.specificity {
  width: 70vw;
  margin: 0 auto;
}

.specificity .header {
  box-sizing: border-box;
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 10vh;
  padding: 0 2vw;
  margin-bottom: 1vh;
  background: #229ffd;
}
.specificity .header h2 {
  letter-spacing: -1px;
  color: #fff;
  /* font-size: 40px; */
  text-shadow: 2px 3px 0px rgba(0, 0, 0, 0.15);
}

button {
  color: #1b9af7;
  font-size: 1vw;
  font-weight: 700;
  border: none;
  border-radius: 2%;
  padding: 1vh 1vw;
  outline: none;
  cursor: pointer;
}
.header button:hover {
  opacity: 0.9;
}

.input-wrapper {
  width: 100%;
  box-sizing: border-box;
  overflow: hidden;
}

li {
  opacity: 1;
}

.item {
  /* padding: 1vw 1vh; */
  position: relative;
  height: auto;
  background: #fff;
  padding: 2vw;
  box-shadow: 0 0 1.5vw 0 #d5cebb;
  overflow: hidden;
  position: relative;
  opacity: 1;
  overflow: hidden;
  margin-bottom: 2vh;
}

.input {
  display: block;
  width: 100%;
  top: 0;
  left: 0;
  margin: 0;
  border: none;
  padding: 1vw;
  background: #0d2a35;
  color: #fff;
  font-size: 30px;
  resize: none;
  outline: none;
  overflow: hidden;
}

dl {
  display: flex;
  flex-direction: row;
  align-items: center;
  margin-top: 2vh;
  color: #516269;
}

dl dt {
  display: block;
  width: 4vw;
  height: 4vw;
  line-height: 4vw;
  border-radius: 50%;
  color: #fff;
  font-weight: 700;
}

dl dd {
  margin-left: 1vw;
}

.operator {
  position: absolute;
  right: 0;
  bottom: 1vh;
}
.operator button {
  font-size: 2vw;
  font-weight: 400;
}

/* 动画区域 */
.fade-enter-active,
.fade-leave-active {
  transition: all 0.5s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}
</style>
