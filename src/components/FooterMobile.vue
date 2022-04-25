<template>
    <div>
        <div class="button_bar_label">
            <div class="jastText">
                <center><span class="summa"><h4>
                    <!--<animatedInteger :value="summa"></animatedInteger> &#8381;-->
                    {{summa}}
                </h4></span></center>
            </div>
            <div><button type="button" class="btno" @click="$emit('showModalOrder')">Оставить заявку</button></div>
        </div>
    </div>
</template>

<script>
import animatedInteger from '@/components/UI/AnimatedInteger.vue'
export default {
    components: {
        animatedInteger
    },
    props: {
        summa: {
            type: Number,
            require: true
        }
    }
}
</script>


<style lang="scss">
// тк мы к ним обращаемся везде ниже
@import "../assets/scss/utils/vars";
@import "../assets/scss/utils/reset";
/*
html {
  line-height: $mainLineHeight;
	font-size: $mainFontSize;
	color: $mainFontColor;
  height: 100%;
  @media screen and (max-width: $desktopWidth) {
		font-size: 16px;
  }
  @media screen and (max-width: $tableWidth) {
		font-size: 15px;
  }
  @media screen and (max-width: $phoneWidth) {
		font-size: 14px;
  }
}*/


    .button_bar_label {
        display: flex;
        justify-content: space-between;
        position: fixed;
        bottom: 0px;
        width: 100vw;
        left: 0px;
        background-color: white;
        border-top: 1px solid $color-orange;
        /*@media screen and (min-width: $tableWidth) {
                display: none;
        }*/
        box-shadow: -1px 0px 10px 3px #00000038;
    }
    .summa {
        color: $color-orange;
        padding: 20px 0px;
    }
    .btno {
        min-width: 200px;
        color: white;
        background-color: $color-orange;
        border: 2px solid $color-orange;
        font-weight: bold;
        padding: 8px 37px;
        cursor: pointer;
    }
    .jastText {
        flex: 1;
        margin: auto 5px;
        font-size: 1.3em;
        color: var(--color-darkgray);
        z-index: 2;
    }
</style>