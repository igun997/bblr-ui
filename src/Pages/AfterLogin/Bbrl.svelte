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
        margin-top: 70px !important;
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
</script>

<div class="row">
    <div class="col-12 ">
        <a href="bblr/add" class="btn btn-bblr float-left rounded-circle align" >
            <Fa icon="{faPlus}" size="sm" />
        </a>
    </div>
    <div class="col-12">
        <div class="card">
            <div class="card-body">
                <div class="row">
                    <div class="col-3">
                        <div class="eye">
                            <Fa icon="{faEye}" size="2x"/>
                        </div>
                    </div>
                    <div class="col-9">
                        <h5 class="title">Nama Anak</h5>
                        <p class="card-text sub_title">
                            desc
                        </p>
                    </div>
                </div>
            </div>
        </div>
    </div>


</div>