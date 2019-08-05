## collapse-comp

**collapse-comp** is a simple Vue.js web component (>= 2.5) that can open/close content placed within its tags along with an open/close user interface icon and a header at the top of the content.  

 **collapse-comp** can be installed via with the included `package.json` file for a local installation via the [npm install](https://docs.npmjs.com/cli/install.html "npm install") command.  **collapse-comp** depends on the [vue.js](https://vuejs.org/ "Vue.js") framework.  A demo folder is provided that used [Parcel](https://parceljs.org/) together with its associated `package.json` file to bundle together  **collapse-comp** and its [vue.js](https://vuejs.org/ "Vue.js") dependency for a simple application.  Further details are provided below for running the demo.

## Props

A prop in Vue.js is a custom attribute for passing information from a parent component hosting **collapse-comp** instance(s) to an **collapse-comp** as a child component. 

**collapse-comp** has the following props for a parent to bind and send information to:

`heading` -- a heading to be displayed above the component's content (string,default: null)

`show_content` -- controls opening(true) and closing(false) content explicitly from the parent code (boolean, default: null) 

`blur_panel` -- if false, will not roll up item panel when component is out of focus (boolean, default: true)

`css_variables` -- defines the css variables for **collapse-comp** (object, default: null)

Note: if `show_content` retains it default value of `null` then an arrow icon appears for the user to control opening/closing content.

## Styling

The **css_variables** prop is a javascript object that contains any combination of css variable names as keys and associated values.  The following list are the css variable names along with their default values for a quick styling of **collapse-comp**:

```
  {
      collapse_comp_font_family: 'Verdana,serif',

      collapse_comp_heading_color: 'black',
      collapse_comp_heading_font_size: '1rem',
      collapse_comp_heading_font_weight: 'bold',
      
      collapse_comp_down_icon: '\21D3';
      collapse_comp_icon_color: 'black'
      
      collapse_comp_content_position: 'static';
  	  collapse_comp_content_z_index: 'auto';
  }
```

As an example you could bind from the parent the following object to the `css_variables` prop for setting the heading font size and the heading color of **collapse-comp**:

```
{collapse_comp_heading_font_size: '24px', collapse_comp_heading_color: 'purple'}
```

Note that multiple **collapse-comp** children of the parent can each be bound to a unique set of `css_variable` prop objects. To enforce the same styling across all **collapse-comp** children, simply  bind just one `css_variable` prop object to all the **collapse-comp** children.

## Events

**collapse-comp** has no events between the parent and child components

## Demonstration

One demonstration of  **collapse-comp**  is provided in the folder named `demo` and can be viewed by hosting the `index.html`file.  The demo (templated in the `App.vue` file)  defines a list of book titles that can be opened/closed.

As a suggestion, install [http-server](https://www.npmjs.com/package/http-server "http-server") locally/globally via [npm](https://www.npmjs.com/ "npm") then enter the command `http-server`in the **collapse-comp** `dist` directory.  From a browser enter the url: `localhost:8080/` to view the demo.

Here is some example code for using **collapse-comp** taken from the demo:

```
      <collapse-comp
        heading="My Favorite Book
        :show_content="show_content">
        <div class="books_content">
          <ul>
            <li> Doctor Strangelove </li>
            <li> I Love jQuery </li>
            <li> Python for Data Analysis </li>
            <li> Applied Calculus </li>
            <li> The Flower Farmer </li>
            <li> Artificial Intelligence </li>
            <li> Introduction to Numerical Methods</li>
            <li> The Audacity of Hope</li>
            <li> The Book of Gimp </li>
          </ul>
        </div>
      </collapse-comp>  
```



And the supporting data reference:

```
data() {
    return {
      show_content: false
    }
  },
  ...
  ...
  ...
  methods: {
    toggle_content: function(){
      this.show_content = !this.show_content;
    }
  }
```

