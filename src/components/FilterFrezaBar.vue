<template>
    <div class="panel">
        <div>{{ panelName }}</div>
        <div class="buttonBarff">
            <button type="button" class="btnff" 
                    v-for="(tab, index)  in items"  :key="index"
                    @click="onClickTab(index)" 
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
        },
        list: {
            type: Array,
            required: true
        }
    },
    methods: {
        onClickTab(index) {
            this.SelectedIndex = index  
            //this.SetFilter(index)  
        },
        SetFilter(index) {
            let list = this.list

            let filter = this.items[index].filterGroup

            if (filter <0) return list

            //filter
            list  = list.filter(function (item) {
                if (item.group == filter) {
                    return item
                }
            })

            this.$emit('filtredFrezaList', list)
        }
    },
    computed: {
        SelectedIndex: {
            get: function() {
                this.SetFilter(this.selectedIndex)
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
    .buttonBarff {        
        //margin: 8px 0px 0px 0px;
        //display: flex;
        justify-content: space-between;
        /* margin: 5px -5px 5px -5px; */
        min-height: 32px;
        font-size: 14px;
    }
    .btnff {
        color: $color-gray;
        background-color: white;
        border: 2px solid $color-gray;
        font-weight: bold;
        padding: 10px;
        cursor: pointer;
        //flex: 1;
        margin: 5px 5px 5px 0px;
        min-width: 155px;
        &:last-child {
                margin-right: 0;
            }
        &:first-child {
                margin-left: 0;
            }
    }
    .btnff:focus {
        border: 2px solid $color-orange !important;
    } 
    .btnff:hover {
        border: 2px solid $color-orange-hover !important;
        color: $color-orange-hover !important;
    } 

    .tabSelected {
        border: 2px solid $color-orange !important;
        color: $color-orange !important;
    }
</style>