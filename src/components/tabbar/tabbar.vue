<template>
    <div style="display: flex; justify-content: center;">
        <div class="x-footer">
            <div class="x-sub">
                <div class="item" :class="tabIndex == 1 ? 'tab-selected' : ''"@click="toPage(1)">
                    <div class="tab-info">
                        <img class="sub-img" :class="tabIndex == 1 ? 'selected-sub-img' : ''" :src="tabIndex == 1 ? require('../../assets/index/lobby2.png') : require('../../assets/index/lobby1.png')" />
                    </div>
                </div>
            </div>
            <div class="x-sub">
                <div class="item" :class="tabIndex == 10 ? 'tab-selected' : ''" @click="toPage(10)">
                    <div class="tab-info">
                        <img class="sub-img" :class="tabIndex == 10 ? 'selected-sub-img' : ''" :src="tabIndex == 10 ?require('../../assets/index/refer2.png'):require('../../assets/index/refer1.png')" />
                    </div>
                </div>
            </div>
            <div class="x-sub">
                <div class="item" :class="tabIndex == 11 ? 'tab-selected' : ''" @click="toPage(11)">
                    <div class="tab-info">
                        <img class="sub-img" :class="tabIndex == 11 ? 'selected-sub-img' : ''" :src="tabIndex == 11 ?require('../../assets/index/vip2.png'):require('../../assets/index/vip1.png')" />
                    </div>
                </div>
            </div>
            <div class="x-sub">
                <div class="item" :class="tabIndex == 4 ? 'tab-selected' : ''" @click="toPage(4)">
                    <div class="tab-info">
                        <img class="sub-img" :class="tabIndex == 4 ? 'selected-sub-img' : ''" :src="tabIndex == 4 ? require('../../assets/index/me2.png'):require('../../assets/index/me1.png')" />
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    name: 'tabbar',
    data() {
        return {
            tabIndex: 1
        }
    },
    created() {

    },
    computed: {

    },
    watch: {
        accountid :{
            immediate: true,
            handler(newValue, oldValue) {
                
            }
        },
        index :{
            immediate: true,
            handler(newValue, oldValue) {
                    this.tabIndex = newValue
            }
        },
        emailCount :{
            immediate: true,
            handler(newValue, oldValue) {
            }
        }
    },
    props: {
        accountid: {
            type: Number,
            default: 0
        },
        index: {
            type: Number,
            default: 1
        },
        emailCount: {
            type: Number,
            default: 0
        }
    },
    mounted() { },
    methods: {
        toPage(type) {
            this.tabIndex = type
            this.$emit('change', type)
        },
        toChangeSlider() {
            this.$emit('changeSlider')
        }
    }
}
</script>
<style lang="less" scoped>
.x-footer {
    display: flex;
    align-items: center;
    height: 60px;
    position: fixed;
    bottom: 0;
    width: 100%;
    z-index: 11;
    background: #161f2c;
}

.x-sub {
    width: 35%;
    height: 100%;
    display: flex;
    justify-content: center;

    .item {
        display: flex;
        flex-direction: column;
        justify-content: center;
        text-align: center;
        position: relative;
        height: 100%;
        width: 70px;
        .selected-bg {
            display: none;
            position:absolute;
            bottom: 0;
            left: -8px;
            height: 80px;
            width: auto;
        }

        .selected-img {
            display: none;
        }
        .red-dot {
            height: 12px;
            width: 12px;
            position: absolute;
            top: 8px;
            right: 10px;
            z-index: 2;
        }
        .tab-info {
            position: absolute;
            left: 0;
            z-index: 1;
            width: 70px;
            text-align: center;

            .sub-img {
                width: 34px;
                height: 34px;
                -o-object-fit: contain;
                object-fit: contain;
                margin: 0 auto;
            }

            .selected-sub-img {
                width: 45px;
                height: 45px;
            }

            .sub-txt {
                font-family: Arial;
                color: white;
                white-space: nowrap;
                font-size: 10px;
                line-height: 1;
            }

            .main-img {
                width: 70px;
                height: 70px;
                -o-object-fit: contain;
                object-fit: contain;
                margin: 0 auto;
            }
        }
    }

    .tab-selected {

        background: rgb(25,32,42);
        background: linear-gradient(to right, rgba(25,32,42,1), rgba(41,61,82,1), rgba(25,32,42,1));
        .selected-bg {
            display: block;
        }
        .tab-info {
            .sub-txt {
                color: white;
            }
        }
    }
}

.x-main {
    width: 30% !important;

    .item {
        .tab-info {
            bottom: 0 !important;
            height: 100% !important;
        }
    }
}
</style>