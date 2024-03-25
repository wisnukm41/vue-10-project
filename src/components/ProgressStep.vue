<template>
    <div class="progress-container">
        <div class="progress-bar">
            <div v-for="(step, index) in steps" :key="index" :class="{'step-active': current === index}">
                {{ step }}
            </div>
        </div>
        <div class="controls">
            <button @click="prevStep" :disabled="current === 0" class="btn">Previous</button>
            <button @click="nextStep" :disabled="current === steps.length - 1" class="btn">
                Next
            </button>
        </div>
    </div>
</template>

<script setup>
import { ref } from "vue";


const steps = ref(['First', 'Second', 'Third'])

const current = ref(0)

const nextStep = () => {
    if(current.value < steps.value.length - 1){
        current.value += 1
    }
}

const prevStep = () => {
    if(current.value > 0){
        current.value -= 1
    }
}

</script>


<style scoped>
.progress-container {
  max-width: 400px;
  margin: 50px auto;
}

.progress-bar {
  display: flex;
  background-color: #eee;
  border-radius: 8px;
  overflow: hidden;
}

.progress-bar div {
  flex: 1;
  text-align: center;
  padding: 15px;
  color: #fff;
  position: relative;
  z-index: 1;
}

.progress-bar div:not(:last-child) {
  border-right: 2px solid #fff;
}

.step-active {
  background-color: #af514c; /* Green for active step */
}

.controls {
  margin-top: 20px;
  text-align: center;
  display: flex;
  justify-content: space-around;
}

.btn {
  padding: 10px 20px;
  font-size: 16px;
  cursor: pointer;
  background-color: #673ab7; /* Purple for button */
  color: #fff;
  border: none;
  border-radius: 5px;
  margin: 0 5px;
}

.btn:disabled {
  background-color: #ccc;
  cursor: not-allowed;
}
</style>