<template>

    <div>


        <text>启动页面{{}}</text>


        <text class="button" @click="goMain2()">去主页le</text>
        <bui-image src="/image/logo.png" width="244px" height="172px"></bui-image>

    </div>

</template>

<script>
    import mixins from '../mixins'
    import pageMixins from '../mixins/page-mixins'
    export default {
        mixins: [mixins, pageMixins],
        data(){
            return {
                state: ''
            }
        },
        computed: {
            userId () {
                if (this.$router && this.$router.params) {
                    return this.$router.params.id
                }
                return 'Hanks10100'
            }
//            ,user () {
//                return this.$store.state.users[this.userId]
//            }
        },
        created: function () {
            //var bundleUrl = this.$getConfig().bundleUrl;
            //bundleUrl = new String(bundleUrl);

            console.log('dddddd' + this.userId)

//            storage.setItem('name', 'Hanks', event => {
//                this.state = 'set success'
//                console.log('set success')
//            })
//
//
//            storage.getItem('name', event => {
//                console.log('get value:', event.data)
//                this.state = 'value: ' + event.data
//
//                modal.toast({
//                    message: 'This is a toast'+this.state,
//                    duration: 0.3
//                })
//            })

            setTimeout(() => {
                this.goMain()
            }, 500);

            //this.globalEvent.removeEventListener("androidback")
            this.log('index create done')
        },
        mounted () {
            this.log('index mounted start')
        },
        methods: {
            goback() {
                this.router.back()
            },
            goMain(){
                this.router.back()
                //this.router.push('/testNative/123')
                this.router.push('/main')
            }
            , goMain2(){
                this.router.push('/native/' + encodeURIComponent('/provider/log?text=sssssss'))
            }
        }
    };
</script>