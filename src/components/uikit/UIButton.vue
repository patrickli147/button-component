
<template>
    <button class="ui-btn" @click="onClickBtn"
        :class="{
            'ui-btn-xsmall': xsmall,
            'ui-btn-small': small,
            'ui-btn-large': large,
            'ui-btn-xlarge': xlarge,
            'ui-btn-tile': tile,
            'ui-btn-rounded': rounded,
            'ui-btn-circle': circle,
            'ui-btn-disabled': disabled
        }"
        :style="`
            --color-tint: ${
                TintColor
            }
        `"
    >
        <slot>默认值</slot>
    </button>
</template>

<script lang="ts">
import { Component, Vue, Emit, Prop } from 'vue-property-decorator';

@Component

export default class UIButton extends Vue{

    @Prop(Boolean) private xsmall: boolean | undefined; //防止ts报错
    @Prop(Boolean) private small: boolean | undefined;
    @Prop(Boolean) private large: boolean | undefined;
    @Prop(Boolean) private xlarge: boolean | undefined;
    @Prop(Boolean) private tile: boolean | undefined;
    @Prop(Boolean) private rounded: boolean | undefined;
    @Prop(Boolean) private circle: boolean | undefined;
    @Prop(Boolean) private disabled: boolean | undefined;
    @Prop(String) private color: string | undefined;

    @Emit('click') private emitClickEvent(event: MouseEvent) {
        console.log("发送 带参数");
    }

    // 计算属性 
    private get TintColor() {
        //如果直接将color传给--color-tint，var函数无法识别undefined，也不会给出默认值
        if (this.color) {
            return this.color;
        } else {
            return '#2D8CF0'
        }
    }

    private mounted() {
        console.log(this.large);
    }

    private onClickBtn(event: MouseEvent) {
        if (!this.disabled) {
            this.emitClickEvent(event);
        }
    }
}
</script>

<style lang="stylus">

/* mixIn */
resize(minWidth, height, paddingLR, fontSize)
    min-width minWidth
    height height
    padding 0 paddingLR 
    font-size fontSize
    &.ui-btn-rounded, &.ui-btn-circle   /*半圆形 圆角度数是按钮高度的一半 */
        /*放到resize里面，使得按钮的height变化时，border-radius能随之变化*/
        border-radius (@height / 2) /*stylus支持算数运算，但是除法需要加上小括号*/
    &.ui-btn-circle  /*按钮为圆形： border-radius = (height / 2) && 宽度等于高度 */
        width @height
        min-width 0 /* 解除最小宽度的约束，使得width永远等于height*/
        padding 0 /* 保证按钮标题居中 */

.ui-btn
    resize(64px, 36px, 16px, 0.875rem)
    border 0 solid black 
    border-radius 4px
    color #17233D /*标题颜色*/
    background-color var(--color-tint, #2D8CF0) /* 使用css中的变量，var（）函数, 第二个参数为默认值 */
    font-weight 500
    letter-spacing 0.09em
    cursor pointer /*移动鼠标到按钮上光标发生变化*/
    user-select none /*拖动鼠标无法选中按钮上的文本*/
    outline none /*点击后没有蓝色的边框 */

    //光标放上去高亮
    &:hover
        filter brightness(200%)
    //按下去按钮变暗
    &:active 
        filter brightness(50%)
        
    &.ui-btn-xsmall
        resize(36px, 20px, 9px, 0.625rem)
    &.ui-btn-small
        resize(50px, 28px, 12px, 0.75rem)
    &.ui-btn-large
        resize(78px, 44px, 19px, 0.875rem)
    &.ui-btn-xlarge
        resize(92px, 52px, 23px, 1rem)   
    &.ui-btn-tile
        border-radius 0
    &.ui-btn-disabled
        background-color #F5F5F5
        color #c5c8ce
        cursor not-allowed

</style>