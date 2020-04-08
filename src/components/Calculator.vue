<template lang="pug">
  .container
    .row
      .col-6-md
        .card.m-1
          .row.m-1
            .col-12
              b-form-input(type="number" v-model="value")
          .row.m-1
            .col-3
              b-button(@click="valueAdd('7')") 7
            .col-3
              b-button(@click="valueAdd('8')") 8
            .col-3
              b-button(@click="valueAdd('9')") 9
            .col-3
              b-button(@click="step('-')") -
          .row.m-1
            .col-3
              b-button(@click="valueAdd('4')") 4
            .col-3
              b-button(@click="valueAdd('5')") 5
            .col-3
              b-button(@click="valueAdd('6')") 6
            .col-3
              b-button(@click="step('+')") +
          .row.m-1
            .col-3
              b-button(@click="valueAdd('1')") 1
            .col-3
              b-button(@click="valueAdd('2')") 2
            .col-3
              b-button(@click="valueAdd('3')") 3
            .col-3
              b-button(variant="success" @click="calculate") =
          .row.m-1
            .col-9
              | {{total}}
            .col-3
              b-button(variant="danger" @click="clear") cls

</template>

<script>
export default {
  data() {
    return {
      value: 0,
      total: null,
      steps: []
    };
  },
  methods: {
    step(action) {
      this.steps.push(this.value);
      this.steps.push(action);
      this.value = 0;
    },
    clear() {
      this.value = 0;
      this.total = null;
      this.steps = [];
    },
    valueAdd(value) {
      if (this.value === 0) {
        this.value = value;
      } else {
        this.value = this.value + value;
      }
    },
    calculate() {
      this.steps.push(this.value);
      let subtotal = 0;
      let lastStep = null;
      this.steps.forEach(step => {
        if (step === "+") {
          lastStep = step;
        } else if (step === "-") {
          lastStep = step;
        } else {
          if (lastStep === null) {
            subtotal = step;
          } else {
            if (lastStep === "+") {
              subtotal = parseFloat(subtotal) + parseFloat(step);
            } else if (lastStep === "-") {
              subtotal = parseFloat(subtotal) - parseFloat(step);
            }
          }
        }
      });

      this.clear();
      this.total = subtotal;
    }
  }
};
</script>
