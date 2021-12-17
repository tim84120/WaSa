<template>
  <div class="app" :class="themeStyle === 'dark' ? 'dark' : ''">
    <div class="header">
      <h1>Wasa Demo</h1>
      <div class="themeBlock">
        <a>{{ mode + ":" }}</a>
        <button @click="themeStyle = 'dark'">Dark</button>
        <button @click="themeStyle = ''">Light</button>
      </div>
    </div>
    <div class="main">
      <button
        v-for="(tab, index) in tabs"
        :key="index"
        :class="['tab_button', { active: currentTab === tab.header }]"
        @click="currentTab = tab.header"
      >
        {{ tab.header }}
      </button>
      <keep-alive>
        <ComponentTransfer :type="currentType" :theme="themeStyle" />
      </keep-alive>
    </div>
  </div>
</template>

<script>
import ComponentTransfer from "./components/ComponentTransfer.vue";
import { ref, computed } from "vue";
import Global from "./Global.vue";

export default {
  name: "App",
  components: {
    ComponentTransfer,
  },
  setup() {
    const currentTab = ref("Text");
    const mode = Global.mode;
    const themeStyle = ref("dark");
    const tabs = [
      {
        header: "Text",
      },
      {
        header: "Radio",
      },
      {
        header: "Select",
      },
    ];
    const currentType = computed(() => currentTab.value.toLowerCase());

    return {
      currentTab,
      mode,
      themeStyle,
      tabs,
      currentType,
    };
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
  height: 800px;
}

.app {
  background: #a6dbaf;
  
  .main {
    margin: 20px;
    height: 700px;

    .tab_button {
      padding: 6px 10px;
      border-top-left-radius: 3px;
      border-top-right-radius: 3px;
      border: 1px solid #ccc;
      cursor: pointer;
      background: #f0f0f0;
      margin-bottom: -1px;
      margin-right: -1px;
    }
    .tab_button:hover {
      background: #418f4e;
    }
    .tab_button.active {
      background: #418f4e;
    }
    .tab {
      border: 1px solid #ccc;
      padding: 10px;
    }
  }
}

.dark {
  background: rgb(3, 66, 12);
  .header {
    background: #2c3e50;
    color: white;
  }
  .main {
    margin: 20px;

    .tab_button {
      padding: 6px 10px;
      border-top-left-radius: 3px;
      border-top-right-radius: 3px;
      border: 1px solid #ccc;
      cursor: pointer;
      background: #f0f0f0;
      margin-bottom: -1px;
      margin-right: -1px;
    }
    .tab_button:hover {
      background: #a6dbaf;
    }
    .tab_button.active {
      background: #a6dbaf;
    }
    .tab {
      border: 1px solid #ccc;
      padding: 10px;
    }
  }
}
.header {
  background: cornsilk;
  color: #2c3e50;
  height: 100px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  font-family: cursive, Helvetica, Arial, sans-serif;

  .themeBlock {
    margin: 10px;
    width: 100%;
    display: flex;
    flex-direction: row;
    justify-content: flex-end;

    button {
      margin: 5px;
    }
    a {
      display: flex;
      align-items: center;
    }
  }
}
</style>
