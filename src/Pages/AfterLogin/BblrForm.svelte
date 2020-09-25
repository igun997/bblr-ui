<script>
    import {toast} from "svelte-toastify";
    import {isLogin} from "../../Components/Common/Store";
    import {navigate} from "svelte-routing";

    export let id;
    let isAdd = false;
    let btnName = "Simpan";
    let dform = {};
    if (id === undefined){
        isAdd = true;
    }else{
        console.log("Updated");
        isAdd = false;
        btnName = "Ubah";
        getDetail(id);
    }
    async function getDetail(id_func){
        const res = await fetch(ps.env.endpoint+"babies/"+id_func, {
            method: 'GET',
            headers: {
                'Accept-Type': 'application/json'
            }
        })

        const json = await res.json()

        if (json.id !== undefined){
            dform.name = json.name;
            dform.born_weight = json.born_weight;
            dform.birth = json.birth;
            dform.jk = json.jk;
        }else{

        }
    }
    async function submitAction() {
        const myId = JSON.parse(localStorage.getItem("fullIdentity"))
        dform.jk = parseInt(dform.jk)
        dform.user_id = myId.id;
        if (isAdd){
            const res = await fetch(ps.env.endpoint+"babies", {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify(dform)
            })

            const json = await res.json()

            if (json.id !== undefined){
                toast.success("Berhasil Menambahkan Info Anak")
                navigate("/bblr",{replace:true})
            }else {
                toast.info("Gagal Menambahkan Info Anak")
            }
        }else{
            const res = await fetch(ps.env.endpoint+"babies/"+id, {
                method: 'PUT',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify(dform)
            })

            const json = await res.json()

            if (json.id !== undefined){
                toast.success("Berhasil Mengubah Info Anak")
                navigate("/bblr",{replace:true})
            }else {
                toast.info("Gagal Mengubah Info Anak")
            }
        }
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
            <label for="jk">Jenis Kelamin</label>
            <select name="jk" bind:value={dform.jk} id="jk" class="form-control">
                <option value="-">== Pilih ==</option>
                <option value="0">Laki - Laki</option>
                <option value="1">Perempuan</option>
            </select>
        </div>

        <div class="form-group">
            <button class="btn btn-bblr btn-block" on:click={submitAction} type="button">{btnName}</button>
        </div>
    </div>
</div>
