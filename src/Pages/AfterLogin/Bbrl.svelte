<style>
    .float{

    }

    .my-float{
        margin-top:22px;
    }
    .align {
        margin-left: 40%;
        color: white !important;
    }
    .card {
        margin-top: 10px !important;
    }
    .eye {
        color: #0e9aa7;
        border-color: #0e9aa7;
    }

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

</style>
<script>
    import Fa from "svelte-fa";
    import { faPlus,faEye } from '@fortawesome/free-solid-svg-icons';
    import {toast} from "svelte-toastify";
    import {navigate} from "svelte-routing";
    let babies = [];
    const myIdentity = JSON.parse(localStorage.getItem("fullIdentity"));
    let myName = myIdentity.name;
    const request = {
        type:"GET",
        content_type:"application/json",
        endpoint:ps.env.endpoint+"dash?type=1&user_id="+myIdentity.id
    }

    async function loadChild() {
        const res = await fetch(request.endpoint, {
            method: request.type,
            headers: {
                'Accept-Type': request.content_type
            }
        })
        const json = await res.json();
        babies = json.detail;
    }
    loadChild()

    function detail(id) {
        navigate("/bblr/"+id+"/detail",{replace:false});
    }

</script>

<div class="row">
    <div class="col-12 ">
        <a href="bblr/add" class="btn btn-bblr float-left rounded-circle align" >
            <Fa icon="{faPlus}" size="sm" />
        </a>
    </div>
    {#each babies as baby,i}
    <div class="col-12">
        <div class="card">
            <div class="card-body">
                <div class="row">
                    <div class="col-3">
                        <div class="eye" on:click={detail(baby.id)}>
                            <Fa icon="{faEye}" size="2x"/>
                        </div>
                    </div>
                    <div class="col-9">
                        <h5 class="title">{baby.name}</h5>
                    </div>
                </div>
            </div>
        </div>
    </div>
    {/each}


</div>