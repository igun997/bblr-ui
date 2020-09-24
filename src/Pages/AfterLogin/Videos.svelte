<script>
    import Icon from "fa-svelte";
    import { faBookmark } from '@fortawesome/free-solid-svg-icons';
    import Video from "../../Components/Seeds/Video";
    const seed = Video;
    let video_list = [];

    import {navigate} from "svelte-routing";

    if (video_list.length === 0){
        video_list = seed;
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
    {#each video_list as item,i}
        <div class="col-12 gap">
            <a href="{item.link}" target="_blank">
                <div class="card " >
                    <div class="card-body">
                        <div class="row">
                            <div class="col-3">
                                <img src="{item.img}" class="img-fluid" alt="">
                            </div>
                            <div class="col-9">
                                <h5 class="title">{item.title}</h5>
                            </div>
                        </div>
                    </div>
                </div>
            </a>
        </div>
    {/each}

</div>