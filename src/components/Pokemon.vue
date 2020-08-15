<template>
  <div>
    <div class="card">
      <div class="card-image">
        <figure>
          <img :src="currentImg" alt="Placeholder image" />
        </figure>
      </div>
      <div class="card-content">
        <div class="media">
          <div class="media-content">
            <p class="title is-4">{{ num }} - {{ name | upper }}</p>
            <p class="subtitle is-6">{{ type }}</p>
          </div>
        </div>

        <div class="content">
          <a @click="mudarSprite" class="button is-primary">Mudar sprite</a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  created: async function() {
    const response = await axios.get(this.url);
    this.front = response.data.sprites.front_default;
    this.back = response.data.sprites.back_default;
    this.type = response.data.types[0].type.name;
    this.currentImg = this.front;
  },
  data() {
    return {
      front: "",
      type: "",
      back: "",
      isFront: true,
      currentImg: "",
    };
  },
  props: {
    num: Number,
    name: String,
    url: String,
  },
  filters: {
    upper: function(value) {
      return value[0].toUpperCase() + value.slice(1);
    },
  },
  methods: {
    mudarSprite: function() {
      if (this.isFront) {
        this.isFront = false;
        this.currentImg = this.back;
      } else {
        this.isFront = true;
        this.currentImg = this.front;
      }
    },
  },
};
</script>

<style></style>
