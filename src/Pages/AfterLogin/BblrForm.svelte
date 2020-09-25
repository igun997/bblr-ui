<script>
    export let id;
    let isAdd = false;
    let btnName = "Simpan";
    let dform = {};
    if (id === undefined){
        isAdd = true;
    }else{
        isAdd = false;
        btnName = "Ubah";
    }
    function submitAction() {
        console.log("Duaar")
    }
</script>
<style>
    .margin-center {
        margin-top: 50%;
    }
</style>
<div class="row">
    <div class="col-12 margin-center">
        <div class="form-group">
            <input type="text" bind:value={dform.name} name="name" placeholder="Nama Anak" class="form-control">
        </div>
        <div class="form-group">
            <input type="number" bind:value={dform.born_weight} name="born_weight" placeholder="Berat Badan Anak Saat Lahir"  class="form-control">
        </div>

        <div class="form-group">
            <input type="date" bind:value={dform.birth} name="birth" placeholder="Tanggal Lahir"  class="form-control">
        </div>

        <div class="form-group">
            <button class="btn btn-bblr btn-block" on:click={submitAction} type="button">{btnName}</button>
        </div>
    </div>
</div>
