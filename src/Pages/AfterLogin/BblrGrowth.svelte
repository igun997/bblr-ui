<script>
import {toast} from "svelte-toastify";
import {navigate} from "svelte-routing";

export let id ;
let dform = {};
async function submitAction() {
    dform.baby_id = id;
    dform.created_at = new Date().getFullYear()+"-"+new Date().getMonth()+"-"+new Date().getDate();
    const res = await fetch(ps.env.endpoint+"baby_growth",{
        method:"POST",
        headers:{
            "Content-Type":"application/json"
        },
        body:JSON.stringify(dform)
    });

    const response = await res.json();
    if(response.id !== undefined){
        toast.success("Data Di Tambahkan");
    }else{
        toast.error("Server Error");
    }
    navigate("/bblr/"+id+"/detail",{replace:true});
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
            <input type="number" bind:value={dform.weight} placeholder="Berat Badan (Kg)" class="form-control">
        </div>
        <div class="form-group">
            <input type="number" bind:value={dform.diameters} placeholder="Lingkar Kepala (CM)" class="form-control">
        </div>
        <div class="form-group">
            <input type="number" bind:value={dform.body_long} placeholder="Panjang Badan (CM)" class="form-control">
        </div>

        <div class="form-group">
            <button class="btn btn-bblr btn-block" on:click={submitAction} type="button">Simpan Data</button>
        </div>
    </div>
</div>