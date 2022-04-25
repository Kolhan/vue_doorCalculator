<template>
    <div>
        <div class="doorPreviews fixed">

            <div class="doorPreview" v-for="(item, index) in items" :key="index">
                <div>                
                    <div class="layer0">
                        <img :src="item.tab_colorBar[item.selected_colorBar].path"/>
                    </div>
                    <div class="layer1">
                        <img  :src="item.tab_frezaBar[item.selected_frezaBar].path"/>
                    </div>
                    <div class="layer2">
                        <img  :src="ImgPath"/>
                    </div> 
                </div> 
                <div class="doorPreview-label">{{item.name}}</div>              
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        items: {
            type: Array,
            require: true
        }
    },
    computed: {
        ImgPath() { return './img/outer.png' }
    }
}
</script>


<style lang="scss">
// тк мы к ним обращаемся везде ниже
@import "../assets/scss/utils/vars";
@import "../assets/scss/utils/reset";

    .doorPreviews {
        display: flex;
        align-items: center;
        justify-content: space-around;
        flex-wrap: wrap;
        &.fixed {
            position: fixed;
            background-color: white;
            top: 0px;
            width: 100vw;
            left: 0px;
            border-bottom: 1px solid $color-orange;
            box-shadow: 1px 0px 10px 3px #00000038;
        }
        
    }

    .doorPreview {
        width: 100px;
        //padding: 18px 20px;
        //margin-bottom: 20px;
        background-color: white;
        height: 250px;
        padding-top: 10px;
        
        
        .layer0 {
            z-index: 0;
            //position: absolute;
            //display: table;
            //top: 0px;
            //margin: 0px;
            height: 0px;
        }
        .layer1 {
            z-index: 1;
            //position: absolute;
            //display: table;
            //top: 0px;            
            //margin: 0px;
            height: 0px;
        }
        .layer2 {
            z-index: 2;
            //position: absolute;
            //display: table;
            //top: 0px;            
            //margin: 0px;
            height: 0px;
        }
    }

    .doorPreview-label {
        font-size: 10px;
        bottom: 0px;
        position: absolute;
        padding-bottom: 5px;
    }

    .imgLayers img {
        position: absolute;
        top: 0px;
        max-width: 100%;
        max-height: 100%;
    }
    .imgLayers {
        position: relative;
        /* max-width: 630px; */
        /* max-height: 630px; */
        width: 630px;
        display: table-cell;
    }
</style>