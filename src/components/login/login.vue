<template>
    <div class="login-masking" @click="close">
        <div style="width: 100%;" @click.stop="func1()">
            <div class="main-page" v-if="tag == 1">
                <div class="close">
                    <img @click="close" :src="require('../../assets/login/close.png')" />
                </div>
                <div class="page-title">
                    <div class="title-item" :class="tag == 1 ? 'active' : ''" @click="changeTag(1)">
                        <div>{{ GLOBAL.lanLocal['login-low'] }}</div>
                    </div>
                    <div class="title-item" :class="tag == 2 ? 'active' : ''" @click="changeTag(2)">
                        <div>{{ GLOBAL.lanLocal['regnow'] }}</div>
                    </div>
                </div>
                <div class="input-box">
                    <span class="name-pre">+55</span>
                    <input class="input name-input" type="text" v-model="loginname"
                        :placeholder="GLOBAL.lanLocal['account']" />
                </div>
                <div class="input-box">
                    <input class="input password-input" type="text" v-if="isEye" v-model="passcode"
                        :placeholder="GLOBAL.lanLocal['passcode']" />
                    <input class="input password-input" type="password" v-else v-model="passcode"
                        :placeholder="GLOBAL.lanLocal['passcode']" />
                    <span class="input-eye" v-if="!isEye" @click="changeEye">
                        <img class="eye-img" :src="require('../../assets/login/pwd-normal.png')" />
                    </span>
                    <span class="input-eye" v-else @click="changeEye">
                        <img class="eye-img" :src="require('../../assets/login/pwd-show.png')" />
                    </span>
                </div>
                <div class="login-desc">
                    <img class="hd" v-if="isRemember" @click="changeRemember"
                        :src="require('../../assets/login/seleted1.png')" />
                    <img class="hd" v-else @click="changeRemember" :src="require('../../assets/login/normal1.png')" />
                    <div class="bd">{{ GLOBAL.lanLocal['keeplogin'] }}</div>
                </div>
                <div class="err-info" :style="{ visibility: loginErr == '' ? 'hidden' : 'visible' }">{{ loginErr ? loginErr
                    : 'info' }}
                </div>
                <div class="login-btn" @click="doLogin">{{ GLOBAL.lanLocal['login'] }}</div>
            </div>
            <div class="main-page" v-if="tag == 2">
                <div class="close">
                    <img @click="close" :src="require('../../assets/login/close.png')" />
                </div>
                <div class="page-title">
                    <div class="title-item" :class="tag == 1 ? 'active' : ''" @click="changeTag(1)">
                        <div>{{ GLOBAL.lanLocal['login-low'] }}</div>
                    </div>
                    <div class="title-item" :class="tag == 2 ? 'active' : ''" @click="changeTag(2)">
                        <div>{{ GLOBAL.lanLocal['regnow'] }}</div>
                    </div>
                </div>
                <div class="input-box">
                    <span class="name-pre">+55</span>
                    <input class="input name-input" type="text" v-model="loginname"
                        :placeholder="GLOBAL.lanLocal['account']" />
                </div>
                <div class="input-box">
                    <input class="input password-input" type="text" v-if="isEye" v-model="passcode"
                        :placeholder="GLOBAL.lanLocal['passcode']" />
                    <input class="input password-input" type="password" v-else v-model="passcode"
                        :placeholder="GLOBAL.lanLocal['passcode']" />
                    <span class="input-eye" v-if="!isEye" @click="changeEye">
                        <img class="eye-img" :src="require('../../assets/login/pwd-normal.png')" />
                    </span>
                    <span class="input-eye" v-else @click="changeEye">
                        <img class="eye-img" :src="require('../../assets/login/pwd-show.png')" />
                    </span>
                </div>
                <div class="input-box">
                    <input class="input password-input" type="text" v-if="isEye2" v-model="passcode2"
                        :placeholder="GLOBAL.lanLocal['passcode']" />
                    <input class="input password-input" type="password" v-else v-model="passcode2"
                        :placeholder="GLOBAL.lanLocal['passcode']" />
                    <span class="input-eye" v-if="!isEye2" @click="changeEye2">
                        <img class="eye-img" :src="require('../../assets/login/pwd-normal.png')" />
                    </span>
                    <span class="input-eye" v-else @click="changeEye2">
                        <img class="eye-img" :src="require('../../assets/login/pwd-show.png')" />
                    </span>
                </div>
                <div class="input-box">
                    <input class="input" type="text" v-model="nickname" :placeholder="GLOBAL.lanLocal['name']" />
                </div>
                <div class="input-box">
                    <input class="input" type="text" v-model="shareid" :placeholder="GLOBAL.lanLocal['shareid']" />
                </div>
                <div class="login-desc">
                    <img class="hd" v-if="isAgree" @click="changeAgree" :src="require('../../assets/login/seleted1.png')" />
                    <img class="hd" v-else @click="changeAgree" :src="require('../../assets/login/normal1.png')" />
                    <div class="bd">{{ GLOBAL.lanLocal['agreement'] }}<span @click="changeTag(3)">
                            {{ GLOBAL.lanLocal['readmore'] }} </span></div>
                </div>
                <div class="err-info" :style="{ visibility: loginErr == '' ? 'hidden' : 'visible' }">{{ loginErr ? loginErr
                    : 'info' }}
                </div>
                <div class="login-btn"
                    :class="(loginname != '' && passcode != '' && passcode2 != '' && nickname != '' && isAgree) ? '' : 'login-btn-disable'"
                    @click="doRegister">{{ GLOBAL.lanLocal['confirm'] }}</div>
            </div>
            <div class="main-page" v-if="tag == 3">
                <h3>{{ GLOBAL.lanLocal['registeragree'] }}</h3>
                <p>
                    1. {{ GLOBAL.lanLocal['agree11'] }}
                    {{ GLOBAL.lanLocal['agree12'] }}
                    {{ GLOBAL.lanLocal['agree13'] }}
                </p>
                <p>
                    2. {{ GLOBAL.lanLocal['agree21'] }}
                    {{ GLOBAL.lanLocal['agree22'] }}
                </p>
                <p>3. {{ GLOBAL.lanLocal['agree31'] }}</p>
                <p>
                    4. {{ GLOBAL.lanLocal['agree41'] }}
                    {{ GLOBAL.lanLocal['agree42'] }}
                </p>
                <p>
                    5. {{ GLOBAL.lanLocal['agree51'] }}
                    {{ GLOBAL.lanLocal['agree52'] }}
                </p>
                <div class="login-btn" @click="agreeProtocal">{{ GLOBAL.lanLocal['agree'] }}</div>
            </div>
        </div>
    </div>
</template>
  
<script>
import md5 from 'js-md5';
import loadFile from "../../api/loadFile.js"
import AES from "../../common/AES.js"
import { doPost } from '../../api/api.js'
import decodeApiLan from '../../api/decodeApiLan.js'
export default {
    name: 'login',
    data() {
        return {
            isEye: false,
            isRemember: true,
            loginname: '',
            passcode: '',
            passcode2: '',
            innerHeight: 0,
            loginErr: '',
            tag: 1,
            isEye2: false,
            nickname: '',
            isAgree: false,
            isProtocal: false,
            shareid: '',
        }
    },
    watch: {
        isReg: {
            immediate: true,
            handler(newValue, oldValue) {
                if (newValue) {
                    this.changeTag(2)
                }
            }
        },
    },
    props: {
        isReg: {
            type: Boolean,
            default: false
        },
    },
    created() {
        this.innerHeight = window.innerHeight - 60
        let shareid = localStorage.getItem(md5("__shareid___"))
        if (shareid) {
            this.shareid = shareid
        } else {
            doPost({
                n: 'AppShare',
                a: 'get_share_id',
                udid: this.GLOBAL.deviceid
            }).then((res) => {
                if (res.code === 0 && res.data) {
                    this.shareid = res.data
                }
            })
        }
    },
    methods: {
        func1() {
        },
        close() {
            this.$emit('close')
        },
        changeTag(tag) {
            if (this.tag != tag) {
                this.isEye = false
                this.isEye2 = false
                this.isRemember = true
                this.loginname = ''
                this.passcode = ''
                this.passcode2 = ''
                this.loginErr = ''
                this.nickname = ''
                this.isAgree = false
                this.tag = tag
            }
        },
        changeEye() {
            this.isEye = !this.isEye
        },
        changeEye2() {
            this.isEye2 = !this.isEye2
        },
        changeRemember() {
            this.isRemember = !this.isRemember
        },
        changeAgree() {
            this.isAgree = !this.isAgree
        },
        showProtocal() {
            this.isProtocal = true
        },
        agreeProtocal() {
            this.changeTag(2)
            this.isAgree = true
        },
        checkName(needResult = false) {
            let loginname = this.loginname.trim()
            if (loginname.length <= 0) {
                this.loginErr = this.GLOBAL.lanLocal['plzinput']
                if (needResult) {
                    return false
                }
            } else {
                if (needResult) {
                    return true
                }
            }
        },
        checkRegName(needResult = false) {
            var numReg = /^[0-9]*$/
            var numRe = new RegExp(numReg)
            let loginname = this.loginname.trim()
            if (loginname.length <= 0) {
                this.loginErr = this.GLOBAL.lanLocal['plzinput']
                if (needResult) {
                    return false
                }
            } else if (!numRe.test(loginname) || loginname.length < 10 || loginname.length > 11) {
                this.loginErr = this.GLOBAL.lanLocal['mobilelengtherror']
                if (needResult) {
                    return false
                }
            } else {
                if (needResult) {
                    return true
                }
            }
        },
        checkPasscode(needResult = false) {
            if (this.passcode.length <= 0) {
                this.loginErr = this.GLOBAL.lanLocal['plzinput']
                if (needResult) {
                    return false
                }
            } else if (this.passcode.length < 6) {
                this.loginErr = this.GLOBAL.lanLocal['sixpasscode']
                if (needResult) {
                    return false
                }
            } else {
                if (needResult) {
                    return true
                }
            }
        },
        doLogin() {
            let that = this
            this.loginErr = ''
            if (this.checkName(true) && this.checkPasscode(true)) {
                const passcode = md5(this.passcode)
                let loginname = this.loginname.trim()
                doPost({
                    n: 'AppGame',
                    a: 'do_login',
                    mobile: loginname,
                    password: passcode
                }).then((res) => {
                    if (res.code === 0) {
                        const json = loadFile("static/nonce", true);
                        if (json != null) {
                            let api_aes_key = json['api_aes_key']
                            localStorage.setItem(md5('__name__'), AES.encrypt(loginname, api_aes_key))
                            localStorage.setItem(md5('__pwd_'), AES.encrypt(passcode, api_aes_key))

                            this.GLOBAL.userInfo.name = loginname
                            this.GLOBAL.userInfo.passcode = passcode

                            that.$emit('success');
                        }
                    } else {
                        const data = decodeApiLan(res, this.GLOBAL.lanArr);
                        this.loginErr = data.message
                    }
                })
            }
        },
        checkPasscode2(needResult = false) {
            if (this.passcode != this.passcode2) {
                this.loginErr = this.GLOBAL.lanLocal['samepasscode']
                if (needResult) {
                    return false
                }
            } else {
                if (needResult) {
                    return true
                }
            }
        },
        checkNickname(needResult = false) {
            if (this.nickname.length <= 0) {
                this.loginErr = this.GLOBAL.lanLocal['plzinput']
                if (needResult) {
                    return false
                }
            } else {
                if (needResult) {
                    return true
                }
            }
        },
        doRegister() {
            this.loginErr = ''
            if (this.checkRegName(true) && this.checkNickname(true) && this.checkPasscode(true) && this.checkPasscode2(true) && this.isAgree) {
                const passcode = md5(this.passcode)
                let loginname = this.loginname
                doPost({
                    n: 'AppEx',
                    a: 'simple_phone_register',
                    username: loginname,
                    mobile: loginname,
                    password: passcode,
                    rolename: this.nickname,
                    deviceid: this.GLOBAL.deviceid,
                    shareid: this.shareid
                }).then((res) => {
                    if (res.code === 0) {
                        const json = loadFile("static/nonce", true);
                        if (json != null) {
                            let api_aes_key = json['api_aes_key']
                            localStorage.setItem(md5('__name__'), AES.encrypt(loginname, api_aes_key))
                            localStorage.setItem(md5('__pwd_'), AES.encrypt(passcode, api_aes_key))

                            this.GLOBAL.userInfo.name = loginname
                            this.GLOBAL.userInfo.passcode = passcode

                            localStorage.setItem('reg', 1);
                            this.$emit('success');
                        }
                    } else {
                        const data = decodeApiLan(res, this.GLOBAL.lanArr);
                        this.loginErr = data.message
                    }
                })
            }
        },
    }
};
</script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="less" scoped>
@media screen and (max-height: 600px) {
    .login-masking {
        align-items: flex-start !important;
    }

    .main-page {
        margin-top: 20px !important;
    }
}

.login-masking {
    position: fixed;
    top: -1px;
    left: 0;
    z-index: 9999;
    height: 100%;
    max-height: 100vh;
    overflow-y: scroll;
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: rgba(0, 0, 0, 0.7);

    .close {
        margin-top: 20px;
        display: flex;
        align-items: center;
        justify-content: flex-end;

        img {
            height: 28px;
            width: auto;
            cursor: pointer;
        }
    }

    .main-page::-webkit-scrollbar {
        width: 0;
    }

    .main-page {
        margin: 0 auto;
        background-color: #161f2c;
        background-repeat: no-repeat;
        background-size: cover;
        width: 100%;
        height: 100vh;
        max-width: 450px;
        max-height: 100%;
        overflow-y: scroll;
        padding: 26px 30px 30px;
        border-radius: 8px;
        border: 1px solid transparent;
        box-sizing: border-box;

        h3,
        p {
            color: #fff;
        }

        p {
            text-align: left;
        }

        .page-title {
            display: flex;
            align-items: center;
            justify-content: center;
            margin-bottom: 20px;
            margin-top: 70px;
            border-radius: 80px;            
            background: #1f2938;

            .title-item {
                color: #59677b;
                font-size: 16px;
                width: 50%;
                text-align: center;
                line-height: 1.2;
                cursor: pointer;
                height: 50px;
                line-height: 50px;
            }

            .title-item:hover {
                color: white;
                transition: all 0.3s;
            }

            .active {
                border-radius: 80px;
                background: #5941C9;
                color: white;
                font-weight: 700;
                transition: all 0.3s;
            }

            .active:hover {
                background: #664ff0;                
            }
        }

        .page-logo {
            display: flex;
            justify-content: flex-start;
            margin-bottom: 30px;

            .logo {
                width: 69px;
                height: 69px;
            }

            >div {
                display: flex;
                flex-direction: column;
                justify-content: center;
                color: white;
                margin-left: 10px;
                font-weight: 700;
                >p{
                    margin: 0px;
                }
            }
        }
        

        .input-box {
            position: relative;
            margin: 0 auto;

            .input {
                background: #1f2938;
                height: 44px;
                line-height: 44px;
                width: 100%;
                border-radius: 10px;
                border-width: 0;
                padding: 0 12px;
                font-size: 18px;
                color: #fff;
                box-sizing: border-box;
                margin-bottom: 16px;
            }

            .input:focus-visible {
                outline: 0px;
            }

            .input::placeholder {
                font-size: 16px;
                color: var(--van-cell-value-color);
            }

            .name-pre {
                height: 44px;
                line-height: 44px;
                font-size: 15px;
                color: #fff;
                position: absolute;
                top: 0;
                left: 0;
                width: 50px;
                text-align: center;
            }

            .name-input {
                padding-left: 50px;
            }

            .input-eye {
                height: 44px;
                line-height: 44px;
                position: absolute;
                top: 0;
                right: 0;
                width: 30px;
                text-align: center;
                display: flex;
                align-items: center;

                .eye-img {
                    height: 15px;
                    width: auto;
                }
            }

            .password-input {
                padding-right: 30px;
            }
        }

        .login-desc {
            display: flex;
            align-items: center;
            box-sizing: border-box;

            .hd {
                height: 20px;
                width: auto;
            }

            .bd {
                flex: 1;
                padding-left: 6px;
                color: #fff;
                font-size: 14px;
                text-align: left;

            }

        }

        .err-info {
            margin-top: 10px;
            color: #dd2c00;
            font-size: 14px;
            text-align: left;
        }

        .login-btn {
            margin: 4px auto 0;
            width: 90%;
            height: 48px;
            line-height: 48px;
            border-radius: 38px;
            text-align: center;
            color: white;
            cursor: pointer;
            font-size: 15px;
            border: 1px solid transparent;
            background: #5941C9;
            text-shadow: 0 1px 2px #104376;
            font-weight: 700;
            font-size: 16px;
        }

        .login-btn:hover {
            background: #664ff0;
            transition: all 0.3s;
        }

        // .login-btn-disable {
        //     opacity: 0.5;
        // }
    }
}</style>
  