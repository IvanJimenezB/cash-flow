<script setup>
import { ref } from "vue";

const showMovements = ref(false);
    
</script>
<template>
    <div class="header">
        <slot name="header"></slot>
    </div>
    <div class="resume">
        <slot name="resume"></slot>
    </div>
    <div class="movements">
        <div class="head" @click="showMovements = !showMovements">
            <div class="grip"></div>
        </div>
        <transition  name="move">
            <div class="body" v-show="showMovements">
                <slot name="movements"></slot>
                aaaa
            </div>
        </transition>
    </div>
</template>
<style scoped>
.header,
.resume,
.movements {
  display: flex;
  justify-content: space-around;
  align-items: center;
  padding: 14px 0;
  box-sizing: border-box;
}

.header {
  position: fixed;
  width: 100vw;
}

.resume {
  min-height: 100vh;
}

.movements {
  z-index: 1;
  position: absolute;
  flex-direction: column;
  bottom: 0;
  width: 100vw;
  background-color: white;
  box-shadow: 0 -8px 16px #e5e5e5;
  border-radius: 24px;
}

.movements .head {
  display: grid;
  place-items: center;
  padding: 4px;
  width: 100%;
  box-sizing: border-box;
}

.movements .body {
  height: 75vh;
  width: 100%;
}

.movements .head .grip {
  width: 120px;
  height: 8px;
  background-color: #e5e5e5;
  border-radius: 4px;
}

/* .move-enter-active {
    transition: transform 1s ease-out;
}

.move-enter-from{
    transform: translateY(500px);
} */
.move-enter-active {
    animation-name: scroll;
    animation-duration: 0.5s;
    animation-fill-mode: forwards;
    animation-iteration-count: 1;
    animation-timing-function: ease;
}
.move-leave-active {
    animation-name: scroll;
    animation-duration: 0.5s;
    animation-fill-mode: forwards;
    animation-direction: reverse;
    animation-iteration-count: 1;
    animation-timing-function: ease;
}

@keyframes scroll {
    from {height: 0;}to{height: 75vh;}
}

</style>