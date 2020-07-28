<template>
  <div class="bg-matrix text-white container-fluid">
    <div class="row my-4">
      <div class="col-4" v-for="target in targets" :key="target">
        <img :src="target.img" alt />
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
          @click="attackEnemy(target,attack.damage)"
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
    // name: "App";
    return {
      targets: [
        {
          health: 100,
          name: "Bob",
          hits: 0,
          img: "./assests/guy-idle.png",
        },
        {
          health: 100,
          name: "Sam",
          hits: 0,
          img: "./assests/guy-idle.png",
        },
        {
          health: 100,
          name: "Jake",
          hits: 0,
          img: "./assests/guy-idle.png",
        },
      ],
      attacks: [
        {
          name: "slap",
          damage: 1,
          img: "./assets/guy-slap.png",
        },
        {
          name: "punch",
          damage: 5,
          img: "./assests/guy-punch.png",
        },
        {
          name: "kick",
          damage: 10,
          img: "./assests/guy-kick.png",
        },
        // {
        //   name: "dead",
        //   damage: 100,
        //   img: "./assests/guy-dead.png",
        // },
      ],
    };
  },
  methods: {
    attackEnemy(target, dmg) {
      target.health -= dmg;
      target.hits++;
    },
    reset(target) {
      (target.health = 100), (target.hits = 0);
    },
  },
};
</script>

