<template>
  <div class='demo_container'>
    <button v-on:click="change_name">Set Name Content to 'Roy Stevens'; Age: 69</button>
    <label-comp
      heading="Your Name:"
      :value="current_name"
      :css_variables="css_variables_short"
      v-on:label_comp_value_changed="value_changed">
    </label-comp>

    <label-comp
      heading="Your Job:"
      value="Plumber"
      :css_variables="css_variables_short"
      v-on:label_comp_value_changed="value_changed">
    </label-comp>

    <label-comp
      heading="Your Address"
      value="102 Spencer Ave, Chicago, Ill. 40044 US"
      header_position="below"
      :css_variables="css_variables_long"
      v-on:label_comp_value_changed="value_changed">
    </label-comp>

    <label-comp
      heading="Your Age"
      :value="current_age"
      header_position="below"
      :css_variables="css_variables_short"
      v-on:label_comp_value_changed="value_changed">
    </label-comp>

    <label-comp
      heading="Favorite Activities"
      :value="current_activities"
      header_position="above"
      :css_variables="css_variables_short">
    </label-comp>
  </div>
</template>

<script>
  import LabelComp from 'labelcomp';
  export default {
    name: 'App',
    data: function() {
      return {
        current_name: 'Jim Jones',
        current_age: null,
        current_activities: 'basketball,football,chess,homework,volleyball, dating',
        css_variables_long: {
          label_comp_heading_color: 'white',
          label_comp_value_color: 'gold',
          label_comp_value_width: '240px'
        },
        css_variables_short: {
          label_comp_heading_color: 'white',
          label_comp_value_color: 'gold',
          label_comp_value_width: '120px'
        }
      };
    },
    components: {
      LabelComp
    },
    methods: {
      change_name: function(){
        this.current_name = 'Roy Stevens';
        this.current_age = 69;
      },
      value_changed: function(value){
        console.log(`Value Changed: ${value}`);
      }
    }
  }
</script>

<style>
  .demo_container {
    width: 100%;
    height: 100%;
    max-width: 50rem;
    min-height: 38rem;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    color: white;
    background-color: black;
    padding: 2rem;
  }
  button {
    width: 220px;
  }
</style>