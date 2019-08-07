## label-comp

**label-comp** is a simple web component (Vue.js >= 2.5) that provides a label (either left or bottom) along with a non-editable content line.  

 **label-comp** can be installed via with the included `package.json` file for a local installation via the [npm install](https://docs.npmjs.com/cli/install.html "npm install") command.  **label-comp** depends on the [vue.js](https://vuejs.org/ "Vue.js") framework.  A demo folder is provided that used [Parcel](https://parceljs.org/) together with its associated `package.json` file to bundle together  **label-comp** along with its [vue.js](https://vuejs.org/ "Vue.js") dependency for a simple application.  Further details are provided below for running the demo.

## Props

A prop in Vue.js is a custom attribute for passing information from a parent component hosting **label-comp** instance(s) to a **label-comp** as a child component. 

**label-comp**  has the following props for a parent to bind and send information to:

`heading` -- a heading for the component that can be positioned below, or to the left of the content box (string, default: `null`)  

`value` -- property for setting the current value for the label (string or number, default: null)      

`header_postion` -- determines the position of the above `heading`as 'below', or 'left' (string, default: 'left')

 `css_variables` -- defines the css variables for this instance (object, default: null)

## Styling

The **css_variables** prop is a javascript object that contains any combination of css variable names as keys and associated values for quick, limited styling of **label-comp**.  The following list is the css variable names along with their default values:

```
  {
  	label_comp_font_family: Verdana, serif,

    label_comp_heading_color: black,
    label_comp_heading_font_size: 1rem,
    label_comp_heading_font_weight: bold,

    label_comp_value_width: 8rem,
    label_comp_value_font_size: 1rem,
    label_comp_value_font_weight: normal,
    label_comp_value_color: black,
    label_comp_value_background: transparent,

    label_comp_scrollbar_color: #D62929
  }
```

## Events

**label-comp** has one event that notifies the parent component of the current content value.

**label-comp** emits the following single named event to its parent:

```
'label_comp_value_changed' -- returns the current value for a label component
```

## Demonstration

A demonstration of **label-comp** is provided in the repository by hosting the `index.html` file under the `dist` folder.  The demo was templated from its `App.vue` file.

As a suggestion, install [http-server](https://www.npmjs.com/package/http-server "http-server") locally/globally via [npm](https://www.npmjs.com/ "npm") then enter the command `http-server`in the **label-comp** `dist` directory.  From a browser enter the url: `localhost:8080/` to view the demo.

Here is some example code for using **label-comp** taken from its template file `App.vue`:

```
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
```

And the supporting data references:

```
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
  methods: {
    change_name: function(){
      this.current_name = 'Roy Stevens';
    },
    value_changed: function(value){
      console.log(`Value Changed: ${value}`);
    }
  }
```

