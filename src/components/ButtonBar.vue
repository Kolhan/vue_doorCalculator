<template>
    <div class="panel">
        <div>{{ panelName }}</div>
        <div class="buttonBar">
            <button type="button" class="btnp" 
                    v-for="(tab, index)  in items"  :key="index"
                    @click="SelectedIndex = index" 
                    v-bind:class="{ tabSelected: SelectedIndex == index}">
                {{ tab.name }}
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

    .panel {
        margin: 15px 0px;
    }
    .buttonBar {        
        margin: 8px 0px 0px 0px;
        display: flex;
        justify-content: stretch;
        /* margin: 5px -5px 5px -5px; */
        min-height: 32px;
        font-size: 14px;
    }
    .btnp {
        color: $color-gray;
        background-color: white;
        border: 2px solid $color-gray;
        font-weight: bold;
        padding: 10px;
        max-width: 155px;
        cursor: pointer;
        flex: 1;
        margin: 0px 3px;
        &:last-child {
                margin-right: 0;
            }
        &:first-child {
                margin-left: 0;
            }
    }
    .btnp:focus {
        border: 2px solid $color-orange !important;
    } 
    .btnp:hover {
        border: 2px solid $color-orange-hover !important;
        color: $color-orange-hover !important;
    } 

    .tabSelected {
        border: 2px solid $color-orange !important;
        color: $color-orange !important;
    }
</style>