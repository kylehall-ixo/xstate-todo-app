<template>
  <main>
    <h1>{{title}}</h1>
    <button class="startBtn" @click="send('TIMER')">
      Step
    </button>
    <div class="traffic-light-container">
      <div class="light red-light" v-bind:class="{ 'red-active': state.value === 'red' }"></div>
      <div class="light yellow-light" v-bind:class="{ 'yellow-active': state.value === 'yellow' }"></div>
      <div class="light green-light" v-bind:class="{ 'green-active': state.value === 'green' }"></div>
    </div>
  </main>
</template>

<script>
import { useMachine } from '@xstate/vue';
import { Machine } from 'xstate';

const lightMachine = Machine({
  id: 'light',
  initial: 'green',
  states: {
    green: {
      on: {
        TIMER: 'yellow'
      }
    },
    yellow: {
      on: {
        TIMER: 'red'
      }
    },
    red: {
      on: {
        TIMER: 'green'
      }
    }
  }
});

export default {
  data() {
    return {
      title: 'HI XSTATE',
    }
  },
  setup() {
    const { state, send } = useMachine(lightMachine);
    return {
      state,
      send
    };
  }
};
</script>

<style>
  .traffic-light-container {
    width: 18%;
    padding-top: 16px;
    margin: 0 auto;

    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    background-color: #333;
    border-radius: 8px;
  }

  .light {
    width: 250px;
    height: 250px;
    border-radius: 100%;
    margin-bottom: 16px;
  }

  .red-light {
    background-color: hsla(360, 82%, 43%, 1);
  }

  .yellow-light {
    background-color: hsla(50, 100%, 42%, 1);
  }

  .green-light {
    background-color: green;
  }

  .startBtn {
    padding: 25px 45px;
    border-radius: 25%;
    margin-bottom: 48px;
  }

  .red-active {
    background-color: hsla(360, 100%, 53%, 1);
  }

  .yellow-active {
    background-color: hsla(50, 100%, 63%, 1);
  }

  .green-active {
    background-color: #52ff52;
  }

</style>
