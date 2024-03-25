<template>
    <div class="demo">
      <h1>Vue Projects</h1>
      <button
        v-for="(_, tab) in tabs"
        :key="tab"
        :class="['tab-button', { active: currentTab === tab }]"
        @click="currentTab = tab"
      >
        {{ tab }}
      </button>
      <component :is="tabs[currentTab]" class="tab"></component>
    </div>
</template>

<script setup>
  import TodoList from '@/components/TodoList.vue'
  import RandomQuoteGenerator from '@/components/RandomQuoteGenerator.vue'
  import Calculator from '@/components/Calculator.vue'
  import Accordion from '@/components/Accordion.vue'
  import FormValidation from '@/components/FormValidation.vue'
  import PasswordGenerator from '@/components/PasswordGenerator.vue'
  import ProgressStep from '@/components/ProgressStep.vue'
  import DadJoke from '@/components/DadJoke.vue'
  import GithubSearch from '@/components/GithubSearch.vue'
  import WikiClone from '@/components/WikiClone.vue'
  import { ref } from 'vue'

  const tabs = {
    TodoList, RandomQuoteGenerator, Calculator, Accordion, FormValidation, PasswordGenerator, ProgressStep, DadJoke, GithubSearch, WikiClone
  };

  const currentTab = ref('TodoList')

</script>

<style scoped>
.demo {
  font-family: sans-serif;
  border: 1px solid #eee;
  border-radius: 2px;
  padding: 20px 30px;
  margin-top: 1em;
  margin-bottom: 40px;
  user-select: none;
  overflow-x: auto;
}

.tab-button {
  display: inline;
  padding: 6px 10px;
  border-top-left-radius: 3px;
  border-top-right-radius: 3px;
  border: 1px solid #ccc;
  cursor: pointer;
  background: #f0f0f0;
  margin-bottom: -1px;
  margin-right: -1px;
  width: fit-content;
}
.tab-button:hover {
  background: #e0e0e0;
}
.tab-button.active {
  background: #e0e0e0;
}
.tab {
  border: 1px solid #ccc;
  padding: 10px;
}
</style>
