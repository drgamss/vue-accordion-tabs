<template>
  <div id="app">
    <div class="container" v-if="uiStyle === 'accordion'">
      <div class="panel-group" v-for="(item, index) in items" :key='index'>
        <div class="panel panel-default">
          <div class="panel-heading">
            <h4 class="panel-title text-left">

            <i class="fa"
            :class="{ 'fa-plus-circle': !item.showInfo, 'fa-minus-circle': item.showInfo }"></i>

            <a @click="ToggleShowInfo(index)"
              :href="getIdWithHash(item.id)">{{ item.name }}
            </a>

            </h4>
          </div>
          <div :id="item.id" class="panel-collapse collapse" :class="{ in: item.showInfo === true}">
              <div class="row">
                <div class="col-sm-8">
                  <div class="panel-body">
                    <p class="text-left">Location - {{ item.location }}</p>
                    <p class="text-left">Age - {{ item.age }}</p>
                    <p class="text-left">
                      {{ item.paragraph }}
                    </p>
                    <a class="read-more" href="javascript:;">Read More</a>
                  </div>
                </div>
                <div class="col-sm-4">
                  <img class="img img-responsive" :src="item.img">
                </div>
              </div>
          </div>
        </div>
      </div>
    </div>
    <div class="container" v-if="uiStyle === 'tabs'">
      <!-- Nav tabs -->
      <ul class="nav nav-tabs" role="tablist">
        <li role="presentation" v-for="(item, index) in items" :key="item.id" :class="{'active': items[index].showInfo === true}">
          <a :href="returnId(item.id)" :aria-controls="item.name" role="tab" data-toggle="tab" @click="ToggleShowInfo(index)">{{ item.name }}</a>
        </li>
      </ul>

      <!-- Tab panes -->
      <div class="tab-content">
        <div role="tabpanel" class="tab-pane" :class="{'active': item.showInfo === true}" :id="item.id" v-for="item in items" :key="item.id">
          <div class="row">
            <div class="col-sm-8">
              <div class="panel-body">
                <p class="text-left">Location - {{ item.location }}</p>
                <p class="text-left">Age - {{ item.age }}</p>
                <p class="text-left">
                  {{ item.paragraph }}
                </p>
                <a class="read-more" href="javascript:;">Read More</a>
              </div>
            </div>
            <div class="col-sm-4">
              <img class="img img-responsive" :src="item.img">
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

/* eslint-disable */
import config from './services/config.js';
export default {
  name: 'App',
  created: function(){
    this.uiStyle = config.uiStyle;
    this.openUnique = config.openUnique;
    if(this.uiStyle == 'tabs'){
      this.items[0].showInfo = true;
    }
  },
  data: function () {
    return {
      uiStyle: '',
      openUnique: true,
      items: [
        {name: 'Daniel Brooks', age: 34, location: 'New York', profession: 'Architect', showInfo: false, id: 0, img: 'https://source.unsplash.com/random/200x200', link: 'https://www.google.co.il/', paragraph: 'Story - Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim adminim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat lajsh hhdos ksjdjd.'},
        {name: 'Avi Gamss', age: 23, location: 'California', profession: 'Lawyer', showInfo: false, id: 1, img: 'https://source.unsplash.com/user/erondu/200x200', link: 'https://www.google.co.il/', paragraph: 'Story - Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim adminim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat lajsh hhdos ksjdjd like his kids.'},
        {name: 'Eric Foster', age: 12, location: 'Texas', profession: 'Doctor', showInfo: false, id: 2, img: 'http://via.placeholder.com/350x250', link: 'https://www.google.co.il/', paragraph: 'Story - Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim adminim veniam.'}
      ]
    }
  },
  watch: {
    uiStyle: function (newVal) {
      console.log(newVal);
    }
  },  
  methods: {
    returnId: function(id){
      return '#' + id;
    },
    ToggleShowInfo: function (index) {
      if (this.openUnique === true) {
        for (var i = 0; i < this.items.length; i++) {
          if (index === i) {
            this.items[index].showInfo = !this.items[index].showInfo;
          } else {
            this.items[i].showInfo = false;
          }
        }
      } else {
        this.items[index].showInfo = !this.items[index].showInfo;
      }
    },
    getIdWithHash: function (id){
      return '#' + id;
    }
  },
  computed: {
      selected: {
        get () {
          return null;
        },
        set (optionValue) {
          this.options = this.options.filter(o => o !== optionValue);
        },
      },
  }
}
</script>


<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px; 

  .col-sm-4 img {
    margin: auto;
    margin-top: 20px;
    margin-bottom: 20px;    
  }

  .style-filter {
    max-width: 200px;
    margin-bottom: 40px;    
  }
}

@import "../node_modules/bootstrap-sass/assets/stylesheets/bootstrap/variables";
@import "../node_modules/bootstrap-sass/assets/stylesheets/bootstrap/mixins";
@import "../node_modules/bootstrap-sass/assets/stylesheets/bootstrap/normalize";
@import "../node_modules/bootstrap-sass/assets/stylesheets/bootstrap/scaffolding";
@import "../node_modules/bootstrap-sass/assets/stylesheets/bootstrap/component-animations";
@import "../node_modules/bootstrap-sass/assets/stylesheets/bootstrap/type";
@import "../node_modules/bootstrap-sass/assets/stylesheets/bootstrap/grid";
@import "../node_modules/bootstrap-sass/assets/stylesheets/bootstrap/panels";
@import "../node_modules/bootstrap-sass/assets/stylesheets/bootstrap/navs";
@import "../node_modules/bootstrap-sass/assets/stylesheets/bootstrap/forms";
@import "../node_modules/bootstrap-sass/assets/stylesheets/bootstrap/utilities";
@import "../node_modules/bootstrap-sass/assets/stylesheets/bootstrap/responsive-utilities";
</style>
