<template>
    <div class="firstStep">
        <alert-v v-on:close="close" v-on:next="next" :btn="btn">
            <span slot="name">{{$store.getters.firstStepAlert.type==1?'新增':'编辑'}}监控点</span>
            <div class="tep-in" slot="con">
                <div class="tep-bar">
                    <div class="tep-bar-item" :class="{select: firstStepAlert.state==1}">
                        监控点参数
                    </div>
                    <div class="tep-bar-item" :class="{select: firstStepAlert.state==2}">
                        模块信息列表
                    </div>
                    <div class="tep-bar-item" :class="{select: firstStepAlert.state==3}">
                        监控参数信息
                    </div>
                </div>
                <first-v v-if="firstStepAlert.state == 1" ref="first" v-on:btntext="changeAlert"></first-v>
                <second-v v-if="firstStepAlert.state == 2" ref="second" v-on:btntext="changeAlert"></second-v>
                <third-v v-if="firstStepAlert.state == 3" ref="third"></third-v>
            </div>
        </alert-v>
    </div>
</template>
<script type="text/javascript">
    import alert from '../../components/alert.vue';
    import first from './first.vue';
    import second from './second.vue';
    import third from './third.vue';
    export default{
        data(){
            return{
                btn: '下一步',
            }
        },
        computed:{
            firstStepAlert(){//新增弹窗状态
                return this.$store.getters.firstStepAlert;
            }
        },
        components:{
            'alert-v' : alert,
            'first-v' : first,
            'second-v' : second,
            'third-v' : third,
        },
        methods:{
            close(){//关闭弹窗
                this.changeAlert(0);
            },
            next(){//下方下一步或者确定按钮点击
                switch (this.firstStepAlert.state) {
                    case 1:
                        this.$refs.first.sunmessage(); // 方法2
                        break;
                    case 2:
                        this.$refs.second.sunmessage(); // 方法2
                        break;
                    case 3:
                        this.$refs.third.sunmessage(); // 方法2
                        break;
                    default:
						break;
                }
            },
            changeAlert(step){//改变步数状态
                console.log('step',step)
                if(step == 3){
                    this.btn = '确定';
                }else{
                    this.btn = '下一步';
                };
                if(step == 0){
                    this.$store.dispatch('SetFirstStepAlert',{
                        type: this.firstStepAlert.type,
                        state: step,
                    });
                }
            }
        },
        created(){

        }
    }
</script>
<style lang="scss">
    .firstStep{
        .tep-in{
            width: 100%;
            padding-top: 7px;
            .tep-bar{
                width: 100%;
                height: 30px;
            }
            .tep-bar-item{
                float: left;
                margin-right: 5px;
                height: 30px;
                padding: 0 10px;
                font-size: 12px;
                color: #999999;
                line-height: 28px;
                border: 1px solid #CFDDE7;
                border-bottom: none;
                border-radius: 3px 3px 0 0;
                cursor: pointer;
            }
            .select{
                background: #2899EE;
                border-color: #2899EE;
                color: #fff;
            }

        }

    }
</style>
