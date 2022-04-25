<template>
        <div class="leftBar">
            <div class="stiky">

            <!--
                <div class="imgLayers" v-for="(item, index) in items" :key="index">
                    <img :src="item.tab_colorBar[item.selected_colorBar].path"/>
                    <img  :src="item.tab_frezaBar[item.selected_frezaBar].path"/>
                    <img  :src="ImgPath"/>
                    <div class="doorPreview-label">{{item.name}}</div>              
                </div>
            -->

                <table>
                    <tr>
                        <td class="td_top" v-for="(item, index) in items" :key="index">
                            <div class="imgContainer">
                                <div class="imgLayer layerBase"><img :src="item.tab_colorBar[item.selected_colorBar].path"/></div>
                                <div class="imgLayer layer"><img  :src="item.tab_frezaBar[item.selected_frezaBar].path"/></div>
                                <div class="imgLayer layer"><img  :src="ImgPath"/></div>    
                            </div>        
                        </td>
                    </tr>
                    <tr>
                        <td>Внешняя отделка</td>
                        <td>Внутренняя отделка</td>
                    </tr>
                    <tr>
                        <td class="td_propety" v-for="(item, index) in items" :key="index">
                            <div>&#10004; {{item.tab_materialBar[item.selected_materialBar].name}}</div>
                            <div>&#10004; Цвет {{item.tab_colorBar[item.selected_colorBar].name}}</div>
                            <div>&#10004; {{item.tab_frezaBar[item.selected_frezaBar].name}}</div>
                        </td>
                    </tr>
                    
                    <tr>
                        <td colspan="2" class="td_summa">
                            <h1>
                                <!-- <animatedInteger :value="summa"></animatedInteger> &#8381; -->
                                {{summa}} &#8381;
                            </h1>
                        </td>
                    </tr>
                    
                    <tr>
                        <td>
                            Изготовим за 7 дней!
                        </td>
                        <td>
                            <button type="button" class="btno" @click="$emit('showModalOrder')">Оставить заявку</button>
                        </td>
                    </tr>
                </table>
            
            </div>
            <div style="height: 60ch;"></div>
        </div>
</template>

<script>
import animatedInteger from '@/components/UI/AnimatedInteger.vue'
export default {
    components: {
        animatedInteger
    },
    props: {
        items: {
            type: Array,
            require: true
        },
        summa: {
            type: Number,
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

    .leftBar-imgLayers img {
        top: 0px;
        max-width: 400px;
        max-height:400px;
    }
    .leftBar-imgLayers {
        text-align: center;
    }





    .imgContainer {
        text-align: center;
        position: relative;
        .imgLayer {
            top: 0px;
            //position: absolute;
            width: 220px;
            height: 470px;
            display: block;
            
            
            &.layerBase{
                margin-top: 0px;
                z-index: 1;
            }
            &.layer{
                margin-top: -470px;
                z-index: 2;
            }
        }
    }

    .leftBar {
        width: 500px;        
    }
    .stiky {
        position: -webkit-sticky;
        position: -moz-sticky;
        position: -ms-sticky;
        position: sticky;
        top: 0;
        z-index: 10;
    }
    .td_summa {
        color: $color-orange;
        text-align: center;
        font-size: 40px;
    }
    .td_top {
        vertical-align: top;
    }
</style>