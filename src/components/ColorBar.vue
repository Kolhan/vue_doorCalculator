<template>
    <div class="panel">
        <div>{{ panelName }}</div>
        <div class="colorBar">
            <button type="button" class="btnc" v-bind:style="{ 'background-color': tab.bgColor }"
                    v-for="(tab, index)  in items"  :key="index"
                    @click="SelectedIndex = index" 
                    v-bind:class="{ 'color-tabSelected': SelectedIndex == index}">
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

    .colorBar {        
        margin: 8px 0px 0px 0px;
        margin: 0px auto;
    }
    .btnc {
        background-color: white;
        border: 4px solid white;
        cursor: pointer;
        margin: 5px;
        border-radius: 50px;
        padding: 17px;
    }
    .btnc:focus {
        border: 4px solid $color-orange !important;
    }
    .btnc:hover {
        border: 4px solid $color-orange-hover !important;
    }  


    .panel {
        margin: 15px 0px;
    }
    
      
    .color-tabSelected {
        border: 4px solid $color-orange !important;
        color: $color-orange !important;
    }
</style>