<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <h1 class="inline">ue Slap</h1>
    <h2 class="bg-dark"
      :class="{'green': target.health >= 75, 'yellow': target.health >= 40 && target.health < 75, 'red': target.health < 40}">
      Health:
      {{target.health}}</h2>
    <h2 class="red" v-if="target.health == 0">It's dead jim.</h2>
    <h2 class="bg-dark" :class="statusColor()">Hits: {{target.hits}}</h2>
    <!-- attacks directly references data and attack can be anything like "banana" -->
    <button class="btn btn-danger btn-lg" @click="dealDamage(attackIndex)" v-for="(attack, attackIndex) in attacks"
      :disabled="target.health == 0">{{attack.name}}</button>
    <button class="btn btn-primary" @click="reset">Reset</button>
  </div>
</template>

<script>
  export default {
    name: 'Home',
    data() {
      return {
        target: {
          health: 100,
          hits: 0
        },
        attacks: [
          {
            name: "Slap",
            dmg: 1
          },
          {
            name: "Punch",
            dmg: 5
          },
          {
            name: "Kick",
            dmg: 10
          }
        ]
      }
    },
    methods: {
      statusColor() {
        let className = 'green'
        if (this.target.health < 75) {
          className = 'yellow'
        }
        if (this.target.health < 40) {
          className = 'red'
        }
        return className
      },
      slap(event) {
        event.target.disabled = true
        setTimeout(() => {
          event.target.disabled = false
        }, 3000)
        this.target.health--
        this.target.hits++
      },
      dealDamage(attackIndex) {
        this.target.health -= this.attacks[attackIndex].dmg
        if (this.target.health < 0) {
          this.target.health = 0
        }
        this.target.hits++
      },
      reset() {
        this.target.health = 100
        this.target.hits = 0
      }
    },
    components: {
    }
  }
</script>

<style>
  .inline {
    display: inline;
  }

  img {
    height: 3rem;
  }

  .green {
    color: green;
  }

  .yellow {
    color: yellow;
  }

  .red {
    color: red;
  }
</style>