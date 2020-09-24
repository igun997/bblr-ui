<script>
    import Icon from "fa-svelte";
    import { faBookmark } from '@fortawesome/free-solid-svg-icons';
    import Articles from "../../Components/Seeds/Articles";
    const seed = Articles;
    let article_list = [];

    import {navigate} from "svelte-routing";
    function detail(id) {
        navigate("artikel/"+id,{replace:true});
    }
    if (article_list.length === 0){
        article_list = seed;
    }
</script>
<style>
    .title {
        color: #808080;
        font-size: 15px;
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
        margin-bottom: 5px;
    }
    a:link {
        text-decoration: none;
    }

    a:visited {
        text-decoration: none;
    }

    a:hover {
        text-decoration: none;
    }

    a:active {
        text-decoration: none;
    }
</style>
<div class="row" id="article_layout">
    {#each article_list as item,i}
    <div class="col-12 gap">
        <a href="artikel/{item.id}">
            <div class="card " >
                <div class="card-body">
                    <div class="row">
                        <div class="col-3">
                            <img src="{item.img}" class="img-fluid" alt="">
                        </div>
                        <div class="col-6">
                            <h5 class="title">{item.title}</h5>
                            <p class="card-text sub_title">
                                {item.short_desc}
                            </p>
                        </div>
                        <div class="col-3">
                            <p class="time sub_title">{item.time} <Icon icon="{faBookmark}" /></p>
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </div>
    {/each}

</div>