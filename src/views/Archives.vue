<template>
    <div class="archives">
        <main>
            <div class="main-inner">
                <div class="content">
                    <div class="post-expand">
                        <div class="posts-collapse">
                            <span class="archive-move-on"></span>
                            <span class="archive-page-counter">
                目前共计 {{total}} 篇日志,继续努力。
              </span>
                            <div v-for="(item,i) in articles" :key="i">
<!--                                <div class="collection-title">-->
<!--                                    <h3 class="archive-year">{{item.year}}</h3>-->
<!--                                </div>-->
<!--                                <article class="post" v-for="(articles,y) in item" :key="y">-->
<!--                                    <div class="post-header">-->
<!--                                        <div class="post-meta">{{time(articles.date)}}</div>-->
<!--                                        <div class="post-title">-->
<!--                                            <router-link :to="{ name: 'articles', params: { id: articles.postId }}">{{articles.title}}</router-link>-->
<!--                                        </div>-->
<!--                                    </div>-->
<!--                                </article>-->
                                <div class="post-header">
                                    <div class="post-meta">{{time(item.created_at)}}</div>
                                    <div class="post-title">
                                        <router-link :to="{ name: 'articles', params: { id: item.post_id }}">{{item.title}}</router-link>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </main>
    </div>
</template>

<script>
    import { getArticleAll } from '../api/request'
    import { formatTime } from '../utils/util'
    export default {
        name: "Archives",
        data () {
            return {
                articles: [],
                total: ''
            }
        },
        mounted () {
            document.title = '归档'
            getArticleAll().then(res => {
                this.articles = res.data.data.articles
                this.total = res.data.data.total
            })
        },
        methods: {
            time (date) {
                return formatTime(date*1000, 'yyyy-mm-dd')
            }
        }
    }
</script>

<style lang="scss" scoped>
    .content {
        min-height: 320px;
        margin-top:50px;
        .posts-expand {
            padding-top: 40px;
        }
        .posts-collapse {
            position: relative;
            margin-left: 55px;
            top: -10px;
            /*opacity: 0;*/
            animation: down 0.5s 0.5s linear;
            animation-fill-mode: both;
            &::after {
                content: ' ';
                position: absolute;
                top: 20px;
                left: 0;
                margin-left: -2px;
                width: 4px;
                height: 100%;
                background: #f5f5f5;
                z-index: -1;
            }
        }
        .archive-move-on {
            position: absolute;
            top: 11px;
            left: 0;
            margin-left: -6px;
            width: 10px;
            height: 10px;
            opacity: 0.5;
            background: #555;
            border: 1px solid #fff;
            border-radius: 50%;
        }
        .archive-page-counter {
            position: relative;
            top: 3px;
            left: 20px;
            line-height: 2;
        }
        .collection-title {
            position: relative;
            margin: 60px 0;
            line-height: 2;
            &::before {
                content: ' ';
                position: absolute;
                left: 0;
                top: 50%;
                margin-left: -4px;
                margin-top: -4px;
                width: 8px;
                height: 8px;
                background: #bbb;
                border-radius: 50%;
            }
        }
        .archive-year {
            margin-left: 20px;
            font-size: 20px;
            margin-left: 20px;
        }
        .post {
            margin: 30px 0;
        }
        .post-header {
            position: relative;
            transition: border .2s ease-in-out;
            border-bottom: 1px dashed #ccc;
            line-height: 2;
            &::before {
                content: ' ';
                position: absolute;
                left: 0;
                top: 12px;
                width: 6px;
                height: 6px;
                margin-left: -4px;
                background: #bbb;
                border-radius: 50%;
                border: 1px solid #fff;
                transition: background .2s ease-in-out;
            }
            &:hover {
                border-bottom-color: #666;
                &::before {
                    background: #666;
                }
            }
        }
        .post-meta {
            position: absolute;
            font-size: 12px;
            left: 20px;
            top: 5px;
        }
        .post-title {
            margin: 20px 0 15px 60px;
            font-size: 16px;
            font-weight: normal;
            line-height: inherit;
            a {
                color: #666;
                border-bottom: none;
            }
        }
    }

    @media screen and(min-width: 300px)and (max-width:768px) {
        .content {
            .posts-collapse {
                margin: 0 20px;
            }
        }
    }

</style>