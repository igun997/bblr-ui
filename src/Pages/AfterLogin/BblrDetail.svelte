<style>

    .section {
        margin-top: 10px;
    }

</style>
<script>
    import {toast} from "svelte-toastify";

    export let id;
    console.log(id)
    function comingSoon() {
        toast.info("Under Construct Dude");
    }
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
                    <th>Nama</th>
                    <th>BB</th>
                    <th>PJ</th>
                    <th>LK</th>
                </tr>
                </thead>
            </table>
        </div>
    </div>
</div>
