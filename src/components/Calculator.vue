<template lang="pug">
  .container
    .row
      .col-6-md
        .card.m-2
          .row.m-1
            .col-12
              b-form-input(type="number" v-model="input")
          .row.m-1
            .col-3
              b-button(@click="addInput('7')") 7
            .col-3
              b-button(@click="addInput('8')") 8
            .col-3
              b-button(@click="addInput('9')") 9
            .col-3
              b-button(variant="danger" @click="cls") CLS
          .row.m-1
            .col-3
              b-button(@click="addInput('4')") 4
            .col-3
              b-button(@click="addInput('5')") 5
            .col-3
              b-button(@click="addInput('6')") 6
            .col-3
              b-button(@click="addAction('-')") -
          .row.m-1
            .col-3
              b-button(@click="addInput('1')") 1
            .col-3
              b-button(@click="addInput('2')") 2
            .col-3
              b-button(@click="addInput('3')") 3
            .col-3
              b-button(@click="addAction('+')") +
          .row.m-1
            .col-9
              | {{total}}
            .col-3
              b-button(variant="success" @click="calculate") =

</template>

<script>
export default {
  data() {
    return {
      input: 0,
      total: null,
      steps: [{ value: 0, action: "" }],
    };
  },
  methods: {
    addInput(newInput) {
      if (this.input === 0) {
        this.input = newInput;
      } else {
        this.input += newInput;
      }
    },
    addAction(action) {
      if (this.input != 0) {
        this.addStep(this.input, action);
      } else if (this.total) {
        this.addStep(this.total, action);
      }
    },
    addStep(value, action) {
      this.steps[this.steps.length - 1].value = value;
      this.steps.push({ value: 0, action: action });
      this.total = null;
      this.input = 0;
    },
    cls() {
      this.clear();
      this.total = null;
    },
    clear() {
      this.input = 0;
      this.steps = [{ value: 0, action: "" }];
    },
    calculate() {
      this.steps[this.steps.length - 1].value = this.input;
      this.steps.forEach(step => {
        switch (step.action) {
          case "+":
            this.total = parseFloat(this.total) + parseFloat(step.value);
            break;
          case "-":
            this.total = parseFloat(this.total) - parseFloat(step.value);
            break;
          default:
            this.total = parseFloat(step.value);
        }
      });
      this.clear();
    }
  }
};
</script>
