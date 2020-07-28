<template>
  <div class="bg-matrix text-white container-fluid">
    <div class="row my-4">
      <div class="col-4" v-for="target in targets" :key="target">
        <img :src="target.img" class="img-fluid" alt />
        <h1 v-if="target.health >0">{{ target.name}}</h1>
        <h2 v-else>{{target.name}} is Dead</h2>
        <h1
          class="text-success"
          :class="{'text-warning' : target.health <= 75, 'text-danger' : target.health <= 50}"
        >Health: {{ target.health < 0 ? 0 : target.health }}</h1>
        <h2>Hit Count: {{target.hits}}</h2>
        <button
          class="btn btn-danger m-1"
          v-for="attack in attacks"
          :key="attack.name"
          :disabled="target.health == 0"
          @click="attackEnemy(target,attack.img, attack.damage)"
        >{{attack.name}}</button>
        <button
          class="btn btn-primary"
          @click="reset(target)"
          :disabled="target.health > 0"
        >Reset Game</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    name: "App";
    return {
      targets: [
        {
          health: 100,
          name: "Bob",
          hits: 0,
          img: require("@/assets/guy-idle.png"),
        },
        {
          health: 100,
          name: "Sam",
          hits: 0,
          img: require("@/assets/guy-idle.png"),
        },
        {
          health: 100,
          name: "Jake",
          hits: 0,
          img: require("@/assets/guy-idle.png"),
        },
      ],
      attacks: [
        {
          name: "slap",
          damage: 1,
          img: require("@/assets/guy-slap.png"),
        },
        {
          name: "punch",
          damage: 5,
          img: require("@/assets/guy-punch.png"),
        },
        {
          name: "kick",
          damage: 10,
          img: require("@/assets/guy-kick.png"),
        },
        // {
        //   name: "dead",
        //   damage: 100,
        //   img: "./assests/guy-dead.png",
        // },
      ],
      guyIdle: require("@/assets/guy-idle.png"),
    };
  },
  methods: {
    attackEnemy(target, img, dmg) {
      target.health -= dmg;
      target.hits++;
      target.img = img;
      setTimeout(() => this.resetGuy(target), 1000);
    },
    resetGuy(target) {
      target.img = this.guyIdle;
    },
    reset(target) {
      (target.health = 100), (target.hits = 0);
    },
  },
};
</script>


