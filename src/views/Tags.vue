<template>
    <div class="tags">
        <main>
            <div class="main-inner">
                <div class="content">
                    <div class="posts-expand">
                        <div class="post-block">
                            <div class="post-body">
                                <div class="tag-cloud">
                                    <div class="tag-cloud-title">目前共计{{tagsList.length}}个标签</div>
                                    <div class="tag-cloud-tags">
                                        <!--                                        :style="{fontSize: tag.articles.length * 2 + 13 + 'px'}"-->
                                        <router-link :style="{fontSize:  tag.articles.length * 2 + 13+ 'px'}"
                                                     :to="{name: 'tagarticle',params:{id: tag.tagId}}"
                                                     v-for="(tag,i) in tagsList" :key="i">{{tag.tagName}}
                                        </router-link>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </main>
        <router-view></router-view>
    </div>
</template>

<script>
    import {getTagsAll} from '../api/request'

    export default {
        name: "tags",
        data() {
            return {
                tagsList: []
            }
        },
        mounted() {
            document.title = '标签'
            getTagsAll().then(res => {
                this.tagsList = res.data.data
            })
        }
    }
</script>

<style lang="scss" scoped>
    .main-inner {
        width: 700px;
        height: auto;
        margin: 0 auto;
        min-width: 350px;
    }
    .content {
        min-height: 320px;
        .posts-expand {
            padding-top: 40px;
        }
        .post-block {
            /*opacity: 0;*/
            top: -10px;
            position: relative;
            animation: down 0.5s 0.5s linear;
            animation-fill-mode: both;
        }
        .tag-cloud {
            text-align: center;
        }
        .tag-cloud-title {
            line-height: 2;
        }
        .tag-cloud-tags {
            a {
                display: inline-block;
                margin: 10px;
                color: #555;
                text-decoration: none;
                outline: none;
                border-bottom: 1px solid #999;
                word-wrap: break-word;
                &:hover {
                    color: #222;
                    border-bottom-color: #222;
                }
            }
        }
    }

</style>