<template>
  <main>
    <h1>{{title}}</h1>
    <button @click="send('TOGGLE')">
      {{
        state.value === 'inactive'
          ? 'Click to activate'
          : 'Active! Click to deactivate'
      }}
    </button>
  </main>
</template>

<script>
import { useMachine } from '@xstate/vue';
import { Machine } from 'xstate';

const toggleMachine = Machine({
  id: 'toggle',
  initial: 'inactive',
  states: {
    inactive: {
      on: { TOGGLE: 'active' }
    },
    active: {
      on: { TOGGLE: 'inactive' }
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
    const { state, send } = useMachine(toggleMachine);
    return {
      state,
      send
    };
  }
};
</script>
