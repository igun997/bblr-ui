<script>
    import {toast} from "svelte-toastify";
    import {navigate} from "svelte-routing";
    import Toggle from "../../Components/Utility/Toogle.svelte"
    import Fa from "fa-svelte"
    import { faCheckCircle,faCircle } from '@fortawesome/free-solid-svg-icons';
    import {Store} from "../../Components/Common/MultiStore";
    export let id ;
    let dform = {};
    let selectedList = [
        {
            id:1,
            name:"Payudara"
        },{
            id:2,
            name:"Gelas"
        },{
            id:3,
            name:"Botol"
        }
    ]
    let babyBehavior = [];
    let breastPosit = null;
    let isFeedForm = false;
    let babyBehaviorOld = null;
    let babyBehaviorAfter = null;
    let isNappyChanged = false;
    let babiesBehavior = [
        {
            id:"is_brought_wind",
            name:"Bayi Bersendawa ? "
        },{
            id:"is_nappy_changed",
            name:"Bayi Ganti Popok ? "
        }
    ]

    let babiesBehaviorAfter = [
        {
            id:"is_soiled_nappy",
            name:"Buang Air Besar "
        },{
            id:"is_wet_nappy",
            name:"Buang Air Kecil "
        }
    ]
    let breastPosition = [
        {
            id:"breast_left_long",
            name:"Payudara Kiri"
        },{
            id:"breast_right_long",
            name:"Payudara Kanan"
        }
    ]
    let feedForm = null;
    function feed_form(from_what) {
        feedForm = from_what;
        isFeedForm = true
    }
    function notifyNappy(notify,checked){
        console.log(notify)
        if (notify === "is_nappy_changed" && checked){
            console.log(checked)
            isNappyChanged = true;
        }else if (notify === "is_nappy_changed" && !checked){
            console.log(checked)
            isNappyChanged = false;

        }
    }
    async function submitAction() {
        dform.baby_id = id;

        dform.created_at = new Date().getFullYear()+"-"+new Date().getMonth()+"-"+new Date().getDate();
        if (babyBehavior.is_brought_wind !== undefined && babyBehavior.is_nappy_changed !== undefined){
            for (const babyBehaviorKey in babyBehavior) {
                if (babyBehaviorKey === "is_brought_wind"){
                    dform.is_brought_wind = babyBehavior[babyBehaviorKey]
                }

                if (babyBehaviorKey === "is_nappy_changed"){
                    dform.is_nappy_changed = babyBehavior[babyBehaviorKey]
                }
            }
        }else {
            dform.is_brought_wind = 0;
            dform.is_nappy_changed = 0;
        }
        if (babyBehaviorAfter === "is_soiled_nappy"){
            dform.is_wet_nappy = 0;
            dform.is_soiled_nappy = 1;
        }else {
            dform.is_wet_nappy = 1;
            dform.is_soiled_nappy = 0;
        }
        dform.breast_left_long = 0
        dform.breast_right_long = 0
        if (breastPosit === "breast_left_long"){
            dform.breast_left_long = 1;
        }else{
            dform.breast_right_long = 1
        }

        if (dform.amount_offer === undefined){
            dform.amount_offer = 0;
        }

        const res = await fetch(ps.env.endpoint+"baby_feed",{
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

    let isView = false;
    let viewValue = null;
    const storage = ((localStorage.getItem("detail_nutrition") == null)?false:JSON.parse(localStorage.getItem("detail_nutrition")));
    if (storage !== false){
        isView = true;
        viewValue = storage;
    }

</script>

<style>
    .margin-center {
        margin-top: 20%;
    }
    .gap {
        margin-top: 10px;
    }
    .margin-bottom {
        margin-bottom: 100px;
    }
</style>
<div class="row margin-bottom">
    <div class="col-12 margin-center">
        <a href="/bblr/{id}/detail" class="btn btn-bblr float-left">
            Kembali
        </a>
    </div>
    {#if (viewValue === null)}
        <div class="col-12 gap">
            <div class="form-group">
                <label for="setDate">Tanggal Perekaman</label>
                <input type="date" id="setDate" bind:value={dform.record_date} placeholder="Tanggal Perekaman" class="form-control">
            </div>
        </div>
        <div class="col-12">
            <h5 style="font-size: 15px">Metode</h5>
            <hr/>
        </div>

        <div class="col-6">
        {#each selectedList as option_item,i}

            <Toggle type='radio' bind:group={dform.feed_from} value={option_item.id} let:checked={checked}>
                {#if checked}
                    <label on:click={feed_form(option_item.id)}><Fa icon="{faCheckCircle}" /> {option_item.name}</label>
                {:else}
                    <label><Fa icon="{faCircle}" /> {option_item.name}</label>
                {/if}
            </Toggle>
        {/each}
    </div>
    <div class="col-6">
        {#if (feedForm === 1)}

            {#each breastPosition as option_item,i}

                <Toggle type='radio' bind:group={breastPosit} value={option_item.id} let:checked={checked}>
                    {#if checked}
                        <label><Fa icon="{faCheckCircle}" /> {option_item.name}</label>
                    {:else}
                        <label><Fa icon="{faCircle}" /> {option_item.name}</label>
                    {/if}
                </Toggle>
            {/each}
        {/if}
    </div>
    <div class="col-12">
        <h5 style="font-size: 15px">Setelah Makan ?</h5>
        <hr/>
    </div>
    {#each babiesBehavior as baby_bv,i}
        <div class="col-6">

            <Toggle type='checkbox' bind:group={babyBehaviorOld} value={baby_bv.id} let:checked={checked}>
                {#if checked}

                    <label data-id={babyBehavior[baby_bv.id] = 1} on:click={notifyNappy(baby_bv.id,1)}><Fa icon="{faCheckCircle}" /> {baby_bv.name}</label>
                {:else}
                    <label data-id={babyBehavior[baby_bv.id] = 0} on:click={notifyNappy(baby_bv.id,0)}><Fa icon="{faCircle}" /> {baby_bv.name}</label>
                {/if}
            </Toggle>
        </div>
    {/each}

    {#if isNappyChanged}
        <div class="col-12">
            <h5 style="font-size: 15px">Karena ..</h5>
            <hr/>
        </div>
        {#each babiesBehaviorAfter as baby_bva,i}
            <div class="col-6">
                <Toggle type='radio' bind:group={babyBehaviorAfter} value={baby_bva.id} let:checked={checked}>
                    {#if checked}
                        <label><Fa icon="{faCheckCircle}"  /> {baby_bva.name}</label>
                    {:else}
                        <label><Fa icon="{faCircle}" /> {baby_bva.name}</label>
                    {/if}
                </Toggle>
            </div>
        {/each}
    {/if}
    {#if isFeedForm}
        <div class="col-12">
            <h5 style="font-size: 15px">Kuantitas</h5>
            <hr/>
            <div class="form-group">
                <input type="number" bind:value={dform.feed_min} class="form-control" placeholder="Durasi Minum (Menit)"/>
            </div>
            <div class="form-group">
                <input type="number" bind:value={dform.amount_taken} class="form-control" placeholder="Jumlah Yang Di Minum (cc)"/>
            </div>
            {#if feedForm !== 1}
                <div class="form-group">
                    <input type="number" bind:value={dform.amount_offer} class="form-control" placeholder="Jumlah Yang Diberikan (cc)"/>
                </div>
            {/if}
        </div>

    {/if}
    <div class="col-12">
        <div class="form-group">
            <button class="btn btn-bblr btn-block" on:click={submitAction} type="button">Simpan Data</button>
        </div>
    </div>
    {:else}

        <div class="col-12 gap">
            <label for="tgl">Tanggal Perekaman</label>
            <input type="text" class="form-control" disabled bind:value={viewValue.record_date}>
        </div>
        <div class="col-6 gap">
            <label for="tgl">Method</label>
            <input type="text" class="form-control" disabled value="Oral">
        </div>
        <div class="col-6 gap">
            <label for="tgl">Type</label>
            {#if (viewValue.feed_from === 1)}
            <input type="text" class="form-control" disabled value="Payudara">
            {:else if (viewValue.feed_from === 2)}
                <input type="text" class="form-control" disabled value="Gelas">
            {:else if (viewValue.feed_from === 3)}
                <input type="text" class="form-control" disabled value="Botol">
            {/if}
        </div>
        {#if (viewValue.feed_from === 1)}
        <div class="col-12 gap">
            <label>Lama Menyusui ({(viewValue.breast_left_long > 0)?"Payudara Kiri":"Payudara Kanan"})</label>
            {#if (viewValue.breast_left_long > 0)}
            <input type="text" class="form-control" disabled value="{viewValue.breast_left_long+" Menit"}">
            {:else}
            <input type="text" class="form-control" disabled value="{viewValue.breast_right_long+" Menit"}">
            {/if}
        </div>
        {/if}

        <div class="col-6 gap">
            <label>Bayi Bersendawa ? <br><b>{(viewValue.is_brought_wind)?"Ya":"Tidak"}</b></label>
            <label>Popok Bayi Diganti ? <br><b>{(viewValue.is_nappy_changed)?"Ya":"Tidak"}</b></label>
            {#if (viewValue.is_nappy_changed)}
                <label>Kondisi Popok ? <br><b>{(viewValue.is_soiled_nappy)?"Buang Air Besar":"Buang Air Kecil"}</b></label>
            {/if}
        </div>
        <div class="col-6 gap">
            {#if (viewValue.feed_from !== 1)}
            <label>Waktu Minum <br><b>{viewValue.feed_min} Menit</b></label>
            <label>Jumlah Diberikan <br><b>{viewValue.amount_offer} CC</b></label>
            <label>Jumlah Dihabiskan <br><b>{viewValue.amount_taken} CC</b></label>
            {/if}
        </div>
    {/if}
</div>
