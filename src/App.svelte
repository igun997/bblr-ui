<script>
	import { Router, Link, Route } from "svelte-routing";
	import Popper from 'popper.js';
	import { toast, ToastContainer } from "svelte-toastify";
	import 'bootstrap/dist/js/bootstrap.bundle.min';
	import Foot from "./Components/Partials/Foot.svelte";
	import Menus from "./Components/Partials/Menus.svelte";
	import Head from "./Components/Partials/Head.svelte";
	import HomeBL from "./Pages/BeforeLogin/Home.svelte";
	import RegisterBL from "./Pages/BeforeLogin/Register.svelte";
	import Dashboard from "./Pages/AfterLogin/Dashboard.svelte"
	import Article from "./Pages/AfterLogin/Articles.svelte";
	import Video from "./Pages/AfterLogin/Videos.svelte";
	import Alarm from "./Pages/AfterLogin/Alarm.svelte";

	import Bbrl from "./Pages/AfterLogin/Bbrl.svelte";
	import BblrDetail from "./Pages/AfterLogin/BblrDetail.svelte";
	import BblrNutrition from "./Pages/AfterLogin/BblrNutrition.svelte";
	import BblrGrowth from "./Pages/AfterLogin/BblrGrowth.svelte";
	import BblrForm from "./Pages/AfterLogin/BblrForm.svelte";

	import ArticleDetail from "./Pages/AfterLogin/ArticleDetail.svelte";
	toast.configure({
		position: "top-left"
	});
	export let url = "";
</script>
<svelte:head>
	<svelte:component this="{Head}"/>
</svelte:head>
<Router url="{url}">
	<svelte:component this="{Menus}"/>
	<style>

		.pull-right {
			float: right;
		}
		.btn-bblr {
			color: #fff;
			background-color: #0e9aa7;
			border-color: #0e9aa7;
		}

		.btn-bblr:hover {
			color: #fff;
			background-color: #3da4ab;
			border-color: #3da4ab;
		}

		.btn-bblr:focus, .btn-primary.focus {
			color: #fff;
			background-color: #3da4ab;
			border-color: #3da4ab;
			box-shadow: 0 0 0 0.2rem rgba(61, 164, 171, 0.5);
		}

		.btn-bblr.disabled, .btn-primary:disabled {
			color: #fff;
			background-color: #0e9aa7;
			border-color: #0e9aa7;
		}

		.btn-bblr:not(:disabled):not(.disabled):active, .btn-bblr:not(:disabled):not(.disabled).active,
		.show > .btn-bblr.dropdown-toggle {
			color: #fff;
			background-color: #75b4b8;
			border-color: #75b4b8;
		}

		.btn-bblr:not(:disabled):not(.disabled):active:focus, .btn-bblr:not(:disabled):not(.disabled).active:focus,
		.show > .btn-bblr.dropdown-toggle:focus {
			box-shadow: 0 0 0 0.2rem rgba(61, 164, 171, 0.5);
		}
	</style>
	<div class="container">
		<Route path="/" component="{HomeBL}" />
		<Route path="register" component="{RegisterBL}" />
		<Route path="home" component="{Dashboard}" />
		<Route path="artikel" component="{Article}" />
		<Route path="video" component="{Video}" />
		<Route path="alarm" component="{Alarm}" />
		<Route path="bblr" component="{Bbrl}" />

		<Route path="bblr/:id/detail" component="{BblrDetail}" let:params>
			<BblrDetail id="params.id" />
		</Route>
		<Route path="bblr/add" component="{BblrForm}" />
		<Route path="bblr/:id/edit" component="{BblrForm}" let:params>
			<BblrForm id="params.id" />
		</Route>

		<Route path="bblr/:id/growth" component="{BblrGrowth}" let:params>
			<BblrGrowth id="params.id" />
		</Route>

		<Route path="bblr/:id/nutrition" component="{BblrNutrition}" let:params>
			<BblrNutrition id="params.id" />
		</Route>

		<Route path="artikel/:id" component="{ArticleDetail}" let:params>
			<ArticleDetail id="params.id" />
		</Route>
	</div>
	<ToastContainer />

</Router>
<svelte:component this="{Foot}"/>
