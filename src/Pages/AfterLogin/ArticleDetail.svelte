<script>
    export let id;
    import ArticleDetail from "../../Components/Seeds/ArticleDetail";
    const seed = ArticleDetail;

    let detail = null;

    if (detail === null){
        detail = seed;
    }
</script>
<style>
    .img-position {
        padding: 0px 0px 0px;
        margin-bottom: 4px;
    }
    .title {
        color: #808080;
        font-size: 18px;
    }
    .sub_title {
        color: #9CA4A3;
        font-size: 11px;
    }
    .time {
        font-size: 11px;
        text-align: center;
    }
    .gap {
        margin-top: 12px;
    }
</style>
<div class="row" id="article_detail_layout">
    <div class="col-12 img-position">
        <img src="{detail.img}" class="img-fluid" alt="">
    </div>
    <div class="col-12 img-position gap">
        <h4 class="title">{detail.title}</h4>
        <hr>
        <div class="card-text sub_title">
            {@html detail.long_desc}
        </div>
    </div>
</div>