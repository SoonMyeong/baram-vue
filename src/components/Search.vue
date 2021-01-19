<template>
    <center>
            <div class="search-wrap">
                <b-input-group                                
                    key="sm"
                    size="sm"                  
                >
                    <b-form-input v-model="query" @click="toggle()" placeholder="장비이름을 입력 하세요" >{{query}}</b-form-input>
                    <b-input-group-append>
                    <b-button size="sm" text="Button" variant="success">검색</b-button>
                    </b-input-group-append>                    
                </b-input-group>

                <div class="options" v-show="visible">
                  <ul>
                    <li v-for="(match,index) in matches"
                    :key="match[filterby]"
                    :class="{'selected':(selected == index)}"
                    @click="itemClicked(index)"
                    v-text="match[filterby]"
                    ></li>
                  </ul>
                </div>                
            </div>
    </center>
</template>

<script>
export default {
  props : ['list','filterby'],
    data() {
      return {
        selectedItem: '',
        query : '',
        selected: 0,
        visible: false
      };
    },
  methods: {
    toggle(){
      this.visible = !this.visible;
    },
    itemClicked(index){
      this.selected = index;
      this.selectItem();     
    },
    selectItem(){
      this.selectedItem = this.matches[this.selected];
      console.log(this.selectedItem[this.filterby]);
      this.query = this.selectedItem[this.filterby];
      this.toggle();
    }
  },
  computed:{
    matches(){ 
      if(this.query ==''){
        return [];
      }    
      return this.list.filter((item)=>item[this.filterby].includes(this.query));
    }
  }
};
</script>
<style scoped>
.search-wrap{padding-top:80%;height: 10%; width:300px;}
.m3{margin-bottom: 0.1 rem !important;}
ul{list-style-type: none; text-align: left; padding-left: 0;}
.options{max-height:200px; overflow-y:scroll; margin-top:2px; color: black;}
.options ul li{padding:5px; cursor:pointer; background-color: white; border-bottom: 1px solid white;}
.options ul li.selected{background-color: blanchedalmond;}
</style>