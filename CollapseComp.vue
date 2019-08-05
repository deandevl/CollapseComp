<template>
  <div class="collapseComp" tabindex="0" v-on:blur="blur_it">
    <section class="collapseComp_headerSec">
      <div
          v-show="show_content == null"
          :class="is_open ? 'collapseComp_arrowIcon__open' : 'collapseComp_arrowIcon__closed'"
          v-on:click="icon_click">
      </div>
      <span v-show="heading">{{heading}}</span>
    </section>
    <section class="collapseComp_contentSec" :style="content_style">
      <slot></slot>
    </section>
  </div>
</template>

<script>
  export default {
    name: 'CollapseComp',
    data(){
      return {
        show_it: false,
        drop_panel_height: null,
        drop_panel_width: null,
        content_style: 'width: 0; height: 0; transition: all 3s; opacity: 0;'
      }
    },
    props: {
      heading: {
        type: String,
        default: null
      },
      show_content: {
        type: Boolean,
        default: null
      },
      blur_panel: {
        type: Boolean,
        default: true
      },
      css_variables: {
        type: Object,
        default: null
      }
    },
    computed: {
      is_open: function(){
        this.toggle_content_state();
        return this.show_it;
      }
    },
    methods: {
      blur_it: function(){
        if(this.show_it && this.blur_panel){
          this.show_it = false;
          this.content_style = 'width: 0;height: 0;transition: all 3s; opacity: 0;';
        }
      },
      icon_click: function(){
        this.show_it = !this.show_it;
      },
      toggle_content_state: function(){
        if(this.show_it || this.show_content){
          this.content_style = 'width: ' + this.drop_panel_width + ';height: ' + this.drop_panel_height + ';transition: all 3s; opacity: 1.0;';
        }else if(!this.show_content){
          this.content_style = 'width: 0;height: 0;transition: all 3s; opacity: 0;';
        }else {
          this.content_style = 'width: 0;height: 0;transition: all 3s; opacity: 0;';
        }
      }
    },
    components: {},
    mixins: [],
    mounted(){
      if(this.css_variables !== null){
        for(let key of Object.keys(this.css_variables)){
          this.$el.style.setProperty(`--${key}`, this.css_variables[key]);
        }
      }
      this.drop_panel_height = `${this.$slots.default[0].elm.clientHeight}px`;
      this.drop_panel_width = `${this.$slots.default[0].elm.clientWidth}px`;
    }
  }
</script>

<style lang="less">
  :root {
    --collapse_comp_font_family: Verdana,serif;

    --collapse_comp_heading_color: black;
    --collapse_comp_heading_font_size: 1rem;
    --collapse_comp_heading_font_weight: bold;

    --collapse_comp_down_icon: '\21D3';
    --collapse_comp_icon_color: black;

    --collapse_comp_content_position: static;
    --collapse_comp_content_z_index: auto;
  }

  .collapseComp {
    font-family: var(--collapse_comp_font_family);
    &:focus {
      outline: none;
    }

    &_headerSec {
      display: flex;
      flex-direction: row;
      color: var(--collapse_comp_heading_color);
      font-size: var(--collapse_comp_heading_font_size);
      font-weight: var(--collapse_comp_heading_font_weight);
      margin-bottom: .5rem;
    }

    &_arrowIcon__open::before {
      content: var(--collapse_comp_down_icon);
      display: inline-block;
      color: var(--collapse_comp_icon_color);
      transition: 600ms linear all;
      margin-right: .2rem;
      font-size: 1rem;
      cursor: pointer;
    }

    &_arrowIcon__closed::before {
      content: var(--collapse_comp_down_icon);
      display: inline-block;
      color: var(--collapse_comp_icon_color);
      transform: rotate(-90deg);
      transition: 600ms linear all;
      margin-right: .2rem;
      font-size: 1rem;
      cursor: pointer;
    }

    &_contentSec {
      position: var(--collapse_comp_content_position);
      transition: all 2s ease-in-out;
      z-index: var(--collapse_comp_content_z_index);
    }
  }
</style>
