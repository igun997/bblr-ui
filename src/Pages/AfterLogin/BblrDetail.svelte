<style>

    .section {
        margin-top: 10px;
    }

</style>
<script>
    import {toast} from "svelte-toastify";
    export let id;
    import Fa from "svelte-fa"
    import { faEye } from '@fortawesome/free-solid-svg-icons';
    import {navigate} from "svelte-routing";
    console.log(id)
    function comingSoon() {
        toast.info("Under Construct Dude");
    }
    let loaded = {
        feed : [],
        growth:[]
    }
    async function load() {
        const req = await fetch(ps.env.endpoint+"baby_detail?baby_id="+id, {
            method: "GET",
            headers:{
                "Accept-Type":"application/json"
            }
        })
        const resp = await req.json();
        if (resp.status === 200){
            loaded.feed = resp.detail.feeds;
            loaded.growth = resp.detail.growth;
        }else {
            toast.info("Invalid Get Detail")
        }
    }
    localStorage.setItem("detail_nutrition",null)
    function nav(item) {
        console.log(item)
        localStorage.setItem("detail_nutrition",JSON.stringify(item))
        navigate("/bblr/"+id+"/nutrition",{replace:false});
    }
    load();
</script>

<div class="row">
    <div class="col-6 section">
        <a href="/bblr/{id}/edit" class="btn btn-bblr">
            Ubah Data
        </a>
    </div>
    <div class="col-6 section">
        <div class="dropdown">
            <button class="btn btn-bblr dropdown-toggle float-right" type="button" id="dropdownMenuButton" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                Pemantauan
            </button>
            <div class="dropdown-menu" aria-labelledby="dropdownMenuButton">
                <a class="dropdown-item" href="/bblr/{id}/nutrition">Nutrisi</a>
                <a class="dropdown-item" href="/bblr/{id}/growth">Pertumbuhan</a>
            </div>
        </div>
    </div>
    <div class="col-12 section">
        <button class="btn btn-bblr section btn-block" on:click={comingSoon}>
           Grafik Pertumbuhan
        </button>
    </div>
    <div class="col-12 section  btn-block" on:click={comingSoon}>
        <button class="btn btn-bblr btn-block">
            Grafik Rekomendasi
        </button>
    </div>
    <div class="col-12 section">
        <p>Tabel Nutrisi</p>
        <div class="table-responsive">
            <table class="table table-bordered table-sm">
                <thead>
                    <tr>
                        <th>Tgl</th>
                        <th>Type</th>
                        <th>Method</th>
                        <th>#</th>
                    </tr>
                </thead>
                <tbody>
                {#each loaded.feed as item_feed,i}
                    <tr>
                        <td>{((item_feed.record_date)?((item_feed.record_date).split(" "))[0]:"-")}</td>
                        <td>Oral</td>
                        <td>
                            {#if (item_feed.feed_from === 1)}
                                Payudara
                            {:else if (item_feed.feed_from === 2)}
                                Gelas
                            {:else if (item_feed.feed_from === 3)}
                                Cup
                            {/if}
                        </td>
                        <td>
                            <button on:click={nav(item_feed)} class="btn btn-bblr">
                                <Fa icon={faEye} size="2x"/>
                            </button>
                        </td>
                    </tr>
                {/each}
                </tbody>
            </table>
        </div>
    </div>

    <div class="col-12 section">
        <p>Tabel Pertumbuhan</p>
        <div class="table-responsive">
            <table class="table table-bordered table-sm">
                <thead>
                    <tr>
                        <th>Tgl</th>
                        <th>Berat Badan</th>
                        <th>Panjang Badan</th>
                        <th>Lingkar Kepala</th>
                    </tr>
                </thead>
                <tbody>
                {#each loaded.growth as item_growth,i}
                    <tr>
                        <td>{((item_growth.created_at)?item_growth.created_at:"-")}</td>
                        <td>
                            {item_growth.weight} Kg
                        </td>
                        <td>
                            {item_growth.body_long} CM
                        </td>
                        <td>
                            {item_growth.diameters} CM
                        </td>
                    </tr>
                {/each}
                </tbody>
            </table>
        </div>
    </div>
</div>
