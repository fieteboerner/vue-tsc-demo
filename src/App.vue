<script setup lang="ts">
import {ref} from 'vue'
import HelloWorld from './components/HelloWorld.vue'

const response = ref<{ data: string[] }>()
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <!-- TS-Error with named slot -->
      <HelloWorld>
        <template v-if="response" #foo>
          <div v-for="line in response.data" :key="line">
            {{ line }}
          </div>
        </template>
      </HelloWorld>

        <!-- No Error with default slot -->
        <HelloWorld>
          <template v-if="response">
            <div v-for="line in response.data" :key="line">
              {{ line }}
            </div>
          </template>
        </HelloWorld>

        <!-- TS-Error with named default slot -->
        <HelloWorld>
          <template v-if="response" #default>
            <div v-for="line in response.data" :key="line">
              {{ line }}
            </div>
          </template>
        </HelloWorld>

        <!-- Nasty workaround -->
        <HelloWorld>
          <template #foo>
            <template v-if="response">
              <div v-for="line in response.data" :key="line">
                {{ line }}
              </div>
            </template>
          </template>
        </HelloWorld>
    </div>
  </header>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
