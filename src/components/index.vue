<template>
    <div id="indexPage">
        <div class="bannerImg"><a href="#registration">
            <img class="forPc" src="../common/images/banner-pc-img.jpg">
            <img class="forSp" src="../common/images/banner-sp-img.jpg">
        </a></div>
        <div class="main">
            <div class="contents">
                <div class="activitySchedule">
                    <div class="commonTitle"><h3>活动时间安排</h3></div>
                    <div class="content">
                         <p><img src="../common/images/schedule-img.png"></p>
                    </div>
                </div>

                <div class="between">
                    <div class="commonTitle"><h3>机构合作联系</h3></div>
                    <div class="content">
                        <div class="imgLeft">
                            <p class="img"><img src="../common/images/between-img.png"></p>
                            <div class="block">
                                <ul>
                                    <li>机构合作有大礼相送</li>
                                    <li>机构合作请联系：<span class="bgRed">王先生 137 7425 9911</span></li>
                                    <li>名额有限，仅限<span class="colorRed">3个名额</span></li>
                                </ul>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="welfare">
                    <div class="commonTitle"><h3>新用户福利</h3></div>
                    <div class="content">
                        <div class="imgRight">
                            <p class="img"><img src="../common/images/welfare-img.png"></p>
                            <div class="block">首次成为达富易实盘用户<br>凭本次体验活动定制U盘<br>领取新用户福利：<span>超级红包一份</span></div>
                        </div>
                    </div>
                </div>

                <div class="activitiesSouvenirs">
                    <div class="commonTitle"><h3>活动纪念品</h3></div>
                    <div class="content">
                        <p><img src="../common/images/souvenirs-img.png"></p>
                        <span>达富易定制U盘1个<small>(达到标准即送，名额不限)</small></span>
                    </div>
                </div>


                <div class="selectionCriteria">
                    <div class="commonTitle"><h3>评选标准</h3></div>
                    <div class="content">
                        <p>账户初始体验金20万人民币，只要累计交易<span class="colorRed">15个交易日</span>以上就送一个纪念品。</p>
                    </div>
                </div>

                <div class="registration" id="registration">
                    <div class="commonTitle"><h3>申请报名</h3></div>
                    <div class="content">
                        <ul>
                            <li><input id="name" type="text" placeholder="请填写姓名" class="inputText"></li>
                            <li><input id="valueNum" type="text" placeholder="请填写联系电话/邮箱" class="inputText"></li>
                            <li style="position: relative"><input id="codeNum" type="text" placeholder="请填写验证码" class="inputText" maxlength="6">
                                <span @click="roundCode"><img :src="captchaImg"></span>
                                <!--<span> <img src="../common/images/logo-img02.png" ></span>-->

                            </li>
                        </ul>
                        <div class="regBtn"><span @click="submitFunc">确认提交</span></div>
                    </div>
                </div>

                <div class="privacy">
                    <div class="commonTitle"><h3>隐私声明/法律说明</h3></div>
                    <div class="content">
                        <ul>
                            <li>1、本活动将通过H5收集参赛个人信息（包括姓名、电话号码及邮箱），达渊软件科技将对信息严格保密，未经允许，不得进行除本次活动外的其他用途。</li>
                            <li>2、任何参赛机构和个人不得以本次活动进行法律所不允许的活动，如：诈骗。否则追究法律责任。</li>
                            <li>3、本次活动发现使用外挂，技术入侵等手段危害活动公平性的行为一律清退活动资格。</li>
                            <li>4、活动最终解释权归上海达渊软件科技有限公司所有。</li>
                        </ul>
                    </div>
                </div>

                <p class="organizers">活动主办方：上海达渊软件科技有限公司</p>
            </div>

        </div>


        <div class="footer">
            <div class="footerLogo">
                <div class="content">
                    <span><img src="../common/images/logo-img01.png"></span>
                    <span><img src="../common/images/logo-img02.png"></span>
                    <span><img src="../common/images/code-img.png"><h3>扫一扫下载达富易</h3></span>
                </div>
            </div>
            <div class="subNav">
                <div class="content">
                    <ul>
                        <li><a href="http://www.dyruanjian.com/service.html">商务合作</a></li>
                        <li><a href="http://www.dyruanjian.com/">达渊官网</a></li>
                        <li><a href="http://wenda.dyruanjian.com/">问题反馈</a></li>
                        <li><a href="http://www.dyruanjian.com/download.html">软件下载</a></li>
                    </ul>
                </div>

            </div>
        </div>

    </div>
</template>

<script>

    export default {
        name: 'indexPage',
        data() {
            return {
                // msg: 'Welcome to Your Vue.js App'
                hostUrl: "http://47.101.49.59:8081",
                captchaId: '',
                captchaImg: ''
            }
        },
        mounted(){
          this.roundCode()
        },
        methods:{
            roundCode:function(){
                this.$axios.post(this.hostUrl + '/v1/verifycode/new').then((response) => {
                    // console.log(response.data.data)
                    this.captchaId = response.data.data;
                    this.captchaImg = this.hostUrl + '/v1/verifycode/get/' + this.captchaId + '.png';

                    console.log( this.captchaImg )
                })
            },
            submitFunc: function () {
                this.name = document.getElementById('name').value;
                // this.card = document.getElementById('cardNum').value;
                this.value = document.getElementById('valueNum').value;
                this.captcha = document.getElementById('codeNum').value;

                if(this.value==''){
                    this.$layer.msg('请填写邮箱/联系电话');
                    return false;
                }
                if (this.name == '') {
                    this.$layer.msg('请填写姓名');
                    return false;
                }
                if(this.captcha==''){
                    this.$layer.msg('请填写验证码');
                    return false;
                }

                var data = {
                    Name: this.name,
                    // Card: '',
                    Value: this.value,
                    Captcha: this.captcha,
                    CaptchaId: this.captchaId
                }


                this.$axios({
                    method:'POST',
                   url: 'http://47.101.49.59:8880/v1/user/website/register',
                   //  url:this.hostUrl + '/v1/verifycode/register',
                    data: JSON.stringify(data),
                 //   timeout: 6000,
                    async:true,
                    crossDomain:true,

                    }).then((response) => {
                    // console.log(response.data.code)
                    if(response.data.code==0){
                        this.$layer.msg('您的帐号和密码将会发送到该邮箱/联系电话中！');
                        setTimeout(()=>{
                          window.location.reload()
                        },1500);
                        return false;
                    }else {
                        this.$layer.msg(response.data.msg);
                        return false;
                    }
                })
            },
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    *, *:before,
    *:after {
        -webkit-box-sizing: border-box;
        -moz-box-sizing: border-box;
        box-sizing: border-box
    }

    img {
        border: 0;
        /*max-width: 100%;*/
        height: auto;
        width: 100%;
        -ms-interpolation-mode: bicubic;
    }

    .forPc {
        display: block !important;
    }

    .forSp {
        display: none !important;
    }

    .bannerImg {
        line-height: 0;
    }

    .bannerImg img {
        width: 100%;
        height: auto;
    }

    .subNav {
        height: 85px;
        background: #05020a;
    }

    .subNav .content {
        width: 950px;
        margin: auto;
        font-size: 0;
        text-align: center;
    }

    .subNav .content ul {
        margin: 0;
        padding: 0;
    }

    .subNav .content ul li {
        list-style: none;
        width: 25%;
        display: inline-block;
        text-align: center;
        line-height: 85px;
    }

    .subNav .content ul li a {
        font-size: 24px;
        text-decoration: none;
        color: #fff;
        display: block;
    }

    .footerLogo {
        background: #0d0419;
    }

    .footerLogo .content {
        display: table;
        width: 950px;
        margin: auto;
        padding: 20px 10px;
    }

    .footerLogo .content span {
        display: table-cell;
        vertical-align: middle;
    }

    .footerLogo .content span:nth-child(1) {
        width: 35%;
        text-align: left;
    }

    .footerLogo .content span:nth-child(1) img {
        width: 302px;
        height: 116px;
    }

    .footerLogo .content span:nth-child(2) {
        width: 45%;
        text-align: center;
    }

    .footerLogo .content span:nth-child(2) img {
        width: 238px;
        height: 116px;
    }

    .footerLogo .content span:nth-child(3) {
        width: 20%;
        text-align: center;
    }

    .footerLogo .content span:nth-child(3) img {
        width: 117px;
        height: 117px;
    }

    .footerLogo .content span:nth-child(3) h3 {
        color: #a8a8a8;
        font-size: 12px;
        line-height: 1;
        padding: 10px 0;
        margin: 0;
    }

    #indexPage .main {
        /*background: #110221 url("../common/images/content-bg.jpg");*/
        background: #110221;
        width: 100%;
    }

    #indexPage .main .contents {
        width: 950px;
        margin: 0 auto;
    }

    .commonTitle h3 {
        padding: 40px 0;
        margin: 0px auto;
        color: #ffffff;
        font-size: 30px;
     /*//   background: url("../common/images/title-bg.png") no-repeat top center;*/
        text-align: center;
        position: relative;
    }
    .commonTitle h3:before{
        content: '';
        position: absolute;
        top: 0;
        left:50%;
        width: 58px;
        height: 48px;
        background: url("../common/images/title-bg.png") no-repeat;
        background-size: cover;
        margin-left: -29px;
    }

    .registration {
        padding: 55px 80px;
    }

    .registration ul, .registration ul li {
        margin: 0;
        padding: 0;
        list-style: none;
    }

    .registration ul li .inputText {
        width: 100%;
        font-size: 20px;
        height: 60px;
        border: none;
        padding: 20px;
        margin-bottom: 20px;
        border-radius: 0;
    }

    .registration .regBtn {
        width: 215px;
        height: 66px;
        color: #ffffff;
        font-size: 30px;
        line-height: 66px;
        background: #ff204a;
        text-align: center;
        margin: 0 auto;
        border-radius: 66px;
        cursor: pointer;
    }
    .registration ul li span{
        width:180px;
        height:60px;
        display: block;
        position: absolute; right: 0; top: 0px;
        z-index: 10;

    }
    .registration ul li span img{
        width: 100%;
        height: 100%;
    }
    .privacy {
        padding: 55px 20px;
    }

    .privacy ul, .privacy ul li {
        margin: 0;
        padding: 0;
        list-style: none;

    }

    .privacy ul li {
        font-size: 24px;
        color: #ffffff;
        margin-top: 20px;
        line-height: 1.4;
    }

    .organizers {
        margin: 0 auto;
        padding: 36px 0;
        color: #6600d2;
        font-size: 20px;
        text-align: center;
    }

    .colorRed {
        color: #ff204a;
    }

    .selectionCriteria {
        padding: 55px 0;
    }

    .selectionCriteria p {
        font-size: 36px;
        color: #ffffff;
        padding: 0px 120px;
        text-align: center;
        line-height: 1.3;
    }

    .activitiesSouvenirs {
        padding: 55px 50px;
    }

    .activitiesSouvenirs span {
        display: block;
        text-align: center;
        color: #ffffff;
        font-size: 36px;
    }

    .activitiesSouvenirs span small {
        display: block;
        font-size: 28px;
    }

    .welfare {
        padding: 55px 0px 55px 20px;
    }

    .welfare .imgRight {
        overflow: hidden;
    }

    .welfare .imgRight .block {
        overflow: hidden;
        color: #ffffff;
        font-size: 30px;
        line-height: 2.5;
        margin-top: 80px;
    }

    .welfare .imgRight .block span {
        background: #ff204a;
        padding: 0 5px;
    }

    .welfare .imgRight .img {
        float: right;
        width: 38%;
    }

    .between {
        padding: 55px 10px;
    }

    .between .imgLeft {
        overflow: hidden;
    }

    .between .imgLeft .img {
        float: left;
        width: 40%;
    }

    .between .imgLeft .block {
        overflow: hidden;
        margin-top: 50px;
    }

    .between .imgLeft .block ul, .between .imgLeft .block ul li {
        margin: 0;
        padding: 0;
        list-style: none;
    }

    .between .imgLeft .block ul li {
        font-size: 30px;
        color: #ffffff;
        position: relative;
        padding: 25px 0 25px 70px;
        line-height: 1.5;
        margin-left: 40px;
    }

    .between .imgLeft .block ul li span.bgRed {
        display: block;
        background: #ff204a;
        width: 420px;
    }

    .between .imgLeft .block ul li:before {
        content: '';
        position: absolute;
        width: 40px;
        height: 58px;
        background: url("../common/images/icon-between.png") no-repeat;
        background-size: cover;
        left: 0px;
        top: 50%;
        margin-top: -29px;
    }

    .activitySchedule{
        padding: 55px 0;
    }


    @media screen and ( max-width: 950px) {
        .forPc {
            display: none !important;
        }

        .forSp {
            display: block !important;
        }

        .subNav .content {
            width: 100%;
        }

        .footerLogo .content {
            width: 100%;
        }

        #indexPage .main .contents {
            width: 100%;
        }

        .welfare .imgRight .block {
            margin-top: 50px;
        }

    }
</style>
