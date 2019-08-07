<template>
  <div class="labelComp">
    <div :style="container_style">
      <div class="labelComp_headerBox" v-if="heading" :style="header_style">{{heading}}</div>
      <div class="labelComp_valueBox">{{computed_value}}</div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'LabelComp',
    props: {
      heading: {
        type: String,
        default: null
      },
      value: {
        default: null
      },
      header_position: {
        type: String,
        default: 'left'
      },
      css_variables: {
        type: Object,
        default: () => {
          return null;
        }
      }
    },
    computed: {
      computed_value: function(){
        this.$emit('label_comp_value_changed',this.value);
        if(this.value !== null) {
          return this.value.toString();
        }else {
          return '';
        }
      },
      container_style: function(){
        if(this.header_position === 'left'){
          return 'display: flex; flex-direction: row;';
        }else if(this.header_position === 'below'){
          return 'display: flex; flex-direction: column-reverse;';
        }else if(this.header_position === 'above'){
          return 'display: flex; flex-direction: column;';
        }
      },
      header_style: function(){
        if(this.header_position === 'left') {
          return 'margin-right: 5px;';
        }
      }
    },
    mounted(){
      if(this.css_variables !== null){
        for(let key of Object.keys(this.css_variables)){
          this.$el.style.setProperty(`--${key}`, this.css_variables[key]);
        }
      }
    }
  }
</script>

<style lang="less">
  :root {
    --label_comp_font_family: Verdana, serif;

    --label_comp_heading_color: black;
    --label_comp_heading_font_size: 1rem;
    --label_comp_heading_font_weight: bold;

    --label_comp_value_width: 8rem;
    --label_comp_value_font_size: 1rem;
    --label_comp_value_font_weight: normal;
    --label_comp_value_color: black;
    --label_comp_value_background: transparent;

    --label_comp_scrollbar_color: #D62929;
  }
  .labelComp {
    display: inherit;
    font-family: var(--label_comp_font_family);

    &_headerBox {
      align-self: center;
      color: var(--label_comp_heading_color);
      font-size: var(--label_comp_heading_font_size);
      font-weight: var(--label_comp_heading_font_weight);
    }

    &_valueBox {
      align-self: center;
      color: var(--label_comp_value_color);
      background: var(--label_comp_value_background);
      border: none;
      font-size: var(--label_comp_value_font_size);
      font-weight: var(--label_comp_value_font_weight);
      padding: 2px;
      white-space: nowrap;

      width: var(--label_comp_value_width);
      overflow-x: auto;
      &::-webkit-scrollbar-track {
        -webkit-box-shadow: inset 0 0 6px rgba(0,0,0,0.3);
        border-radius: 10px;
        background-color: #F5F5F5;
      }
      &::-webkit-scrollbar {
        height: 8px;
        width: 8px;
        background-color: transparent;
      }
      &::-webkit-scrollbar-thumb {
        border-radius: 10px;
        -webkit-box-shadow: inset 0 0 6px rgba(0, 0, 0, .3);
        background-color: var(--label_comp_scrollbar_color);
      }
    }
  }
</style>