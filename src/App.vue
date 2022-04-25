<template>
  <div class="wrapper">
    
    <!-- <header></header> -->

    <div class="wrapper-content">
      <section>
        <div class="container">

            <!-- Верхная фиксированная часть в мобильной версии -->
            <headerMobile :items="panels" class="visibleOnlyMobile"/>
            
            <!-- Таблица с левой и правой частью -->
            <table class="mainContainerTable">
              <tr>
                <td class="leftBar hideOnlyMobile">
                  <!-- Левая фиксированная часть -->
                  <leftBar :items="panels" :summa="summa" @showModalOrder="modalValidate = true"/>
                </td>
                <td style="vertical-align: top;">
                  <!-- Правая прокручиваемая часть -->
                  <div class="mainContainer">
                      <div v-for="(item, item_index) in panels" :key="item_index" class="panelBar" >
                          <!-- Материалы -->
                          <buttonBar 
                              :items="item.tab_materialBar" 
                              :selectedIndex="item.selected_materialBar" 
                              :panelName="item.name_materialBar"
                              @selectedIndexChange = "item.selected_materialBar = $event"/>
                          
                          <!-- Цвет -->
                          <colorBar 
                              :items="item.tab_colorBar" 
                              :selectedIndex="item.selected_colorBar" 
                              :panelName="item.name_colorBar"
                              @selectedIndexChange = "item.selected_colorBar = $event"/>
                                              
                          <!-- Фильтр рисунка -->
                          <filterFrezaBar 
                              :items="item.tab_filterFrezaBar"                      
                              :selectedIndex="item.filter_frezaBarGroup" 
                              :list="item.tab_frezaBar"
                              :panelName="item.name_frezaBar"
                              @selectedIndexChange = "item.filter_frezaBarGroup = $event"
                              @filtredFrezaList = "item.filtredFrezaList = $event"/>
                          
                          <!-- Рисунок -->
                          <frezaBar 
                              :items="item.filtredFrezaList" 
                              :selectedIndex="item.selected_frezaBar" 
                              @selectedIndexChange = "item.selected_frezaBar = $event"/>
                      </div>          
                  </div> 
                </td>
              </tr>
            </table>              

            <!-- footer для мобильной версии -->
            <footerMobile :summa="summa" class="visibleOnlyMobile" @showModalOrder="modalValidate = true"/>

            <!-- Модальное окно с отправкой на почту -->
            <modalValidate v-if="modalValidate" @close="modalValidate = false"/>

        </div>
      </section>
    </div>

    <!-- <footer></footer> --> 
      
  </div>

</template>



<script>


var outerdisign = { 
    name: "Внешная отделка",
    name_materialBar: "Материал внешней отделки:", 
    name_colorBar: "Цвет внешней отделки:", 
    name_frezaBar: "Рисунок внешней панели:",
    
    selected_materialBar: 0,
    selected_colorBar: 0,
    selected_frezaBar: 0,
    filter_frezaBarGroup: 0,
    
    tab_materialBar: [
         { name: "МЕТАЛЛ",  price: 13000 },
         { name: "МДФ",     price: 20000 },    
    ],

    tab_colorBar: [
         { name: "цвет1",   price: 1000, bgColor: "#D9D9D9", path:'./img/innerFreza/Base/1.jpg'},
         { name: "цвет2",   price: 1400, bgColor: "#b7c149", path:'./img/innerFreza/Base/2.jpg'},
         { name: "цвет3",   price: 1400, bgColor: "#dcb594", path:'./img/innerFreza/Base/3.jpg'},
         { name: "цвет4",   price: 1400, bgColor: "#b24143", path:'./img/innerFreza/Base/4.jpg'},
         { name: "цвет5",   price: 1400, bgColor: "#E8E9ED", path:'./img/innerFreza/Base/5.jpg'},
         { name: "цвет6",   price: 1400, bgColor: "#85939C", path:'./img/innerFreza/Base/6.jpg'},
         { name: "цвет7",   price: 1400, bgColor: "#be6c94", path:'./img/innerFreza/Base/7.jpg'},
         { name: "цвет8",   price: 1400, bgColor: "#DFDAD7", path:'./img/innerFreza/Base/8.jpg'},
         { name: "цвет9",   price: 1400, bgColor: "#83619b", path:'./img/innerFreza/Base/9.jpg'},  
         { name: "цвет10",   price: 1400, bgColor: "#999999", path:'./img/innerFreza/Base/10.jpg'}, 
    ],   
    
    tab_filterFrezaBar: [
         { name: "КЛАССИКА",    filterGroup: 1}, 
         { name: "НЕОН",        filterGroup: 2}, 
         { name: "ГРАНД",       filterGroup: 3},  
         { name: "СОВРЕМЕННЫЕ", filterGroup: 4}, 
         { name: "ЗЕРКАЛО",     filterGroup: 5},            
    ],
    tab_frezaBar: [
         { id:'0', name: "Фрезеровка №1", price: 1300, group: 1, path:'./img/innerFreza/Classic/1.png'},
         { id:'1', name: "Фрезеровка №2", price: 1500, group: 1, path:'./img/innerFreza/Classic/2.png'},
         { id:'2', name: "Фрезеровка №3", price: 1800, group: 2, path:'./img/innerFreza/Classic/3.png'},
         { id:'3', name: "Фрезеровка №4", price: 1200, group: 2, path:'./img/innerFreza/Classic/4.png'},
         { id:'4', name: "Фрезеровка №5", price: 1800, group: 3, path:'./img/innerFreza/Classic/5.png'},
         { id:'5', name: "Фрезеровка №6", price: 1200, group: 4, path:'./img/innerFreza/Classic/6.png'},
         { id:'6', name: "Фрезеровка №7", price: 1200, group: 5, path:'./img/innerFreza/Classic/7.png'},
    ],
    filtredFrezaList: []
}

var innerdisign = { 
    name: "Внутренная отделка",
    name_materialBar: "Материал внутренней отделки:", 
    name_colorBar: "Цвет внутренней отделки:", 
    name_frezaBar: "Рисунок внутренней панели:",
    
    selected_materialBar: 0,
    selected_colorBar: 0,
    selected_frezaBar: 0,
    filter_frezaBarGroup: 0,
    
    tab_materialBar: [
         { name: "МЕТАЛЛ", price: 3200 },
         { name: "МДФ", price: 4600    },    
    ],

    tab_colorBar: [
         { name: "цвет1",   price: 1000, bgColor: "#D9D9D9", path:'./img/innerFreza/Base/1.jpg'},
         { name: "цвет2",   price: 1400, bgColor: "#b7c149", path:'./img/innerFreza/Base/2.jpg'},
         { name: "цвет3",   price: 1400, bgColor: "#dcb594", path:'./img/innerFreza/Base/3.jpg'},
         { name: "цвет4",   price: 1400, bgColor: "#b24143", path:'./img/innerFreza/Base/4.jpg'},
         { name: "цвет5",   price: 1400, bgColor: "#E8E9ED", path:'./img/innerFreza/Base/5.jpg'},
         { name: "цвет6",   price: 1400, bgColor: "#85939C", path:'./img/innerFreza/Base/6.jpg'},
         { name: "цвет7",   price: 1400, bgColor: "#be6c94", path:'./img/innerFreza/Base/7.jpg'},
         { name: "цвет8",   price: 1400, bgColor: "#DFDAD7", path:'./img/innerFreza/Base/8.jpg'},
         { name: "цвет9",   price: 1400, bgColor: "#83619b", path:'./img/innerFreza/Base/9.jpg'},  
         { name: "цвет10",   price: 1400, bgColor: "#999999", path:'./img/innerFreza/Base/10.jpg'},    
    ],   
    
    tab_filterFrezaBar: [
         { name: "КЛАССИКА",    filterGroup: 1}, 
         { name: "НЕОН",        filterGroup: 2}, 
         { name: "ГРАНД",       filterGroup: 3},  
         { name: "СОВРЕМЕННЫЕ", filterGroup: 4}, 
         { name: "ЗЕРКАЛО",     filterGroup: 5},            
    ],
    tab_frezaBar: [
         { id:'0', name: "Фрезеровка №1", price: 1300, group: 1, path:'./img/innerFreza/Classic/1.png'},
         { id:'1', name: "Фрезеровка №2", price: 1500, group: 1, path:'./img/innerFreza/Classic/2.png'},
         { id:'2', name: "Фрезеровка №3", price: 1800, group: 2, path:'./img/innerFreza/Classic/3.png'},
         { id:'3', name: "Фрезеровка №4", price: 1200, group: 2, path:'./img/innerFreza/Classic/4.png'},
         { id:'4', name: "Фрезеровка №5", price: 1800, group: 3, path:'./img/innerFreza/Classic/5.png'},
         { id:'5', name: "Фрезеровка №6", price: 1200, group: 4, path:'./img/innerFreza/Classic/6.png'},
         { id:'6', name: "Фрезеровка №7", price: 1200, group: 5, path:'./img/innerFreza/Classic/7.png'},
    ],
    filtredFrezaList: []
}

var panels = [
    outerdisign, innerdisign
]

import buttonBar from '@/components/ButtonBar.vue'
import colorBar from '@/components/ColorBar.vue'
import frezaBar from '@/components/FrezaBar.vue'
import filterFrezaBar from '@/components/FilterFrezaBar.vue'
import footerMobile from '@/components/FooterMobile.vue'
import headerMobile from '@/components/HeaderMobile.vue'
import leftBar from '@/components/LeftBar.vue'

import modals from '@/components/UI/Modal.vue'
import modalValidate from '@/components/ModalValidate.vue'

export default {
  components: {
    buttonBar, colorBar, frezaBar, filterFrezaBar, footerMobile, headerMobile, leftBar, 
    modals, modalValidate
  },
  data(){
    return {
      title: 'Notes App',
      panels: panels,
      modalValidate: false,
    }
  },

  methods: {

  },

  computed: {
    // если свойство только возвращает данные, достаточно простой функции:
    summa() {
        let _summa = 0;
        this.panels.forEach(function(item) {
            _summa = _summa + 
                item.tab_materialBar[item.selected_materialBar].price+
                item.tab_colorBar[item.selected_colorBar].price+
                item.tab_frezaBar[item.selected_frezaBar].price
        });
        return _summa;
    },    

  },
  watch: {
    number: function(newValue) {
      TweenLite.to(this.$data, 0.5, { tweenedNumber: newValue });
    }
  }

}
</script>

<style lang="scss">
// тк мы к ним обращаемся везде ниже
@import "./assets/scss/utils/vars";
@import "./assets/scss/utils/reset"; 

  .visibleOnlyMobile {
    @media screen and (min-width: $tableWidth) {
      display: none;
    }
  }
  .hideOnlyMobile {
    @media screen and (max-width: $phoneWidth) {
      display: none;
    }
  }


  .mainContainer{
    @media screen and (max-width: $phoneWidth) {
      margin-top: 210px;
      margin-bottom: 22px;
    }
    
  }

  .container {
    @media screen and (max-width: $smDesktopWidth) {
      display: flex;
    }
    @media screen and (max-width: $tableWidth) {
      display: flex;
    }
    @media screen and (max-width: $phoneWidth) {

    }
    
  }

  .mainContainerTable {
    @media screen and (min-width: $desktopWidth) {
      margin-top: -84px
    }
    @media screen and (min-width: $tableWidth) {
      margin-top: -84px
    }
    @media screen and (min-width: $phoneWidth) {
       margin-top: -74px
    }
    
  }

  

  table td {
      padding: 0px !important;
  }
</style>
