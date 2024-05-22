<script>
import { ref } from 'vue';

export default {
  setup() {
    const display = ref('');
    const buttons = [
      { value: 'AC', type: 'clear' },
      { value: 'DEL', type: 'delete' },
      { value: '.', type: 'operator' },
      { value: '/', type: 'operator' },

      { value: '7' },
      { value: '8' },
      { value: '9' },
      { value: '*', type: 'operator' },

      { value: '4' },
      { value: '5' },
      { value: '6' },
      { value: '-', type: 'operator' },

      { value: '1' },
      { value: '2' },
      { value: '3' },
      { value: '+', type: 'operator' },

      { value: '000' },
      { value: '00' },
      { value: '0' },
      { value: '=', type: 'equals' },
    ];

    function updateDisplay(value) {
      if (value === 'AC') {
        return display.value = '';
      }
      if (value === 'DEL') {
        return display.value = display.value.slice(0, -1);
      }
      if (value === '=') {
        return display.value = eval(display.value);
      }
      display.value += value;
    }

    return {
      display,
      buttons,
      updateDisplay,
    };
  },
};
</script>

<template>
  <div class="calculator">
    <input type="text" v-model="display" class="display" disabled />

    <div class="buttons">
      <button v-for="btn in buttons" :key="btn.value" @click="updateDisplay(btn.value)"
        :class="`button button_${btn.type || 'default'}`">
        {{ btn.value }}
      </button>
    </div>
  </div>
</template>

<style>
body{
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100hv;
  background: #35374B;
}

.calculator{
  max-width: 360px;
  border-radius: 10px;
  padding: 20px;
  background-color: #344955;
}

.display{
  width: 100%;
  height: 56px;
  font-size: 20px;
  text-align: right;
  margin-bottom: 10px;
  padding: 20px;
  border-radius: 5px;
  color: black;
  background-color: #35374B;
  border: none;
  box-sizing: border-box;
}

.buttons{
  display: flex;
  flex-wrap: wrap;
  width: 100%;
  justify-content: space-between;
}

.button{
  display: flex;
  align-items: center;
  justify-content: center;
  width: calc(100% / 5);
  height: 60px;
  margin: 8px 3px;
  border-radius: 10px;
  background-color: #344955;
  color: #78A083;
  font-size: 21px;
  border: none;
  cursor: pointer;
  box-shadow: 0px 1px 3px rgba(0, 0, 0, 0.2);
  transition: all .3s ease-in-out;
  }

  .button:hover{
    transform: translateY(-4px);
    box-shadow: 0px 2px 4px 2px rgba(0, 0, 0, 0.2);
  }

  .button:focus{
    outline: none;
  }

  .button_operator,
  .button_delete,
  .button_equals{
    color: #401F71;
  }

  .button_clear{
    color: #9B3922;
  }

  @media screen and (max-width: 426px) {
    button{
      font-size: 18px !important;
    }
    
    .calculator{
      max-width: 260px !important;
    }
  }
</style>
