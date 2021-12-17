<template>
  <div class="content" :class="theme === 'dark' ? 'dark' : ''">
    <div class="text" v-show="type === 'text'">
      <input type="text" v-model="inputText" placeholder="Text something" />
    </div>
    <div class="radio" v-show="type === 'radio'">
      <label
        ><input
          type="radio"
          name="color"
          value="blue"
          v-model="radioSelect"
        /><a>藍色</a></label
      >
      <label
        ><input
          type="radio"
          name="color"
          value="yellow"
          v-model="radioSelect"
        /><a>黃色</a></label
      >
      <label
        ><input type="radio" name="color" value="red" v-model="radioSelect" /><a
          >紅色
        </a></label
      >
      <label
        ><input type="radio" name="color" value="green" v-model="radioSelect" />
        <a>綠色</a></label
      >
    </div>
    <div class="select" v-show="type === 'select'">
      <select v-model="selectedItems">
        <option value="" disabled selected>--Select your car--</option>
        <option value="Porsche">Porsche</option>
        <option value="BMW">BMW</option>
        <option value="Mercedes">Mercedes</option>
        <option value="Audi">Audi</option>
      </select>
    </div>
    <div class="showAll">
      {{ inputText }}
      {{ radioSelect }}
      {{ selectedItems }}
    </div>
    <div class="langList" v-if="list">
      <ul>
        <li v-for="(item, index) in list" :key="index">
          {{'No. ' + item.id + ' ==> ' + item.title }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import { ref, onMounted } from "vue";

export default {
  name: "componentTransfer",
  props: {
    msg: String,
    type: String,
    theme: String,
  },

  setup() {
    onMounted(() => {
      fetch("https://mocki.io/v1/5683c354-ef99-445d-a25f-bddf6d466987")
        .then((res) => res.json())
        .then((data) => (list.value = data.ProgramLanguage))
        .catch((err) => console.log(err.message));
    });
    const list = ref();
    const themeStyle = ref("dark");
    const inputText = ref();
    const radioSelect = ref();
    const selectedItems = ref("");

    return {
      list,
      themeStyle,
      inputText,
      radioSelect,
      selectedItems,
    };
  },
};
</script>

<style lang="scss">
.content {
  margin: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;

  .radio a {
    color: rgb(50, 50, 51);
  }
  .showAll {
    color: rgb(48, 80, 185);
    margin: 50px;
    font-size: 60px;
    height: 70px;
  }
  ul {
    text-align: left;

    list-style-type: none;
  }
  .langList {
    color: black
  }
}

.dark {
  .radio a {
    color: rgb(238, 231, 231);
  }
  .showAll {
    color: lightskyblue;
  }
  .langList {
    color: white
  }
}
</style>
