<template>
    <div class="panel">
        <div>{{ panelName }}</div>
        <div class="frezaBar">
            <button type="button" class="btnf" v-bind:style="{ 'background-color': tab.bgColor }"
                    v-for="(tab, index)  in items"  :key="index"
                    @click="SelectedIndex = tab.id" 
                    v-bind:class="{ 'freza-tabSelected': SelectedIndex == tab.id}">
                <img :src="tab.path"/>
            </button>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        panelName: {
            type: String
        },
        items: {
            type: Array,
            required: true
        },
        selectedIndex: {
            type: Number,
            require: true
        }
    },
    computed: {
        SelectedIndex: {
            get: function() {
                return this.selectedIndex
            },
            set: function(value) {
                this.$emit('selectedIndexChange', value)
            }
        }
    }
}
</script>


<style lang="scss">
// тк мы к ним обращаемся везде ниже
@import "../assets/scss/utils/vars";
@import "../assets/scss/utils/reset";

    .frezaBar {        
        margin: 8px 0px 0px 0px;
        margin: 0px auto;
    }
    .btnf {
        background-color: white;
        border: 2px solid $color-gray;
        cursor: pointer;
        margin: 5px;
        //padding: 17px;
        
    }
    .btnf img {
        max-width: 78px;
    }
    .btnf:focus {
        border: 2px solid $color-orange !important;
    }
    .btnf:hover {
        border: 2px solid $color-orange-hover !important;
    }  


    .panel {
        margin: 15px 0px;
    }
    
      
    .freza-tabSelected {
        border: 2px solid $color-orange !important;
        color: $color-orange !important;
    }
</style>