<template>
    <!--<text class="button" @click="test2()"> 跳转至messages页面{{test}}dd</text>-->
    <!-- Flow  Float  Flayer  Flexbox  四种布局方式 -->
    <div class="g-flex-column">
        <div class="g-flex-full">
            <!--<div class="g-flayer g-flex-center" v-if="loading">-->
                <!--<text> loading ...</text>-->
            <!--</div>-->
            <list class="g-flex-full" @loadmore="loadMoreStories" loadmoreoffset="50">
                <cell v-for="movie in searchResult" :key="movie.url" append="tree">
                    <movie :data="movie"></movie>
                </cell>
            </list>
        </div>
    </div>
</template>

<script>
    import {mapGetters, mapActions} from 'vuex'
    import Movie from './movie.vue'
    import mixins from '../mixins'
    export default  {
        mixins: [mixins],
        components: {
            Movie
        },
        props: {
            keyWord: {
                type: String,
                required: true
            }
        },
        data(){
            return {
                loading: true,
                myPage:1
            }
        },
        created () {

        },
        computed: {
            searchResult () {
                return this.store.state.searchResult
            },
        },
        methods: {
            loadMoreStories() {
                this.myPage = this.myPage +1;
                this.searchList({keyWord: this.keyWord,page:this.myPage})
            },
            ...mapActions([
                'searchList'
            ])
        },
        watch: {
            "keyWord": {
                handler(val,oldVal) {
                    this.searchList({keyWord: this.keyWord,page:1})
                },
                // 深度观察
                deep: true
            }
        },
    };
</script>

<style scoped>
    .g-flex-row {
        display: flex;
        flex-direction: row;
    }

    .g-flex-column {
        display: flex;
        flex-direction: column;
    }

    .g-flayer {
        position: absolute;
        left: 0;
        top: 0;
        right: 0;
        bottom: 0;
    }

    .g-flex-center {
        flex: 1;
        justify-content: center; /*针对子view 是行内元素才起作用*/
        align-items: center; /*针对子view 是行内元素才起作用*/
    }

    .g-flex-full {
        flex: 1;
    }

    .c-red {
        background-color: #FF66ff;
    }
</style>
