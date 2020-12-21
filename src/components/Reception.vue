<template>
   <div id="container">
		<header>
			<HeaderApp/>
		</header>
	   
		<main class="mb-4">
			<Menu/>
			<div>
				<b-modal id="modal-center" centered title="Descripción de Sprint 4">
					<template #modal-title>
							<div class="pl-3">Descripción de Sprint 4</div>
						</template>

						<template>
							<div class="p-3">
								<h5>Reto 2</h5>
								<p>Se exponen las siguientes operaciones HTTP:</p>
								<ol>
									<li>Get Room Type (GET)</li>
									<li>Booking Price (POST)</li>
								</ol>
								<h5>Reto 3</h5>
								<p>Las anteriores operaciones HTTP se consumen respectivamente en:</p>
								<ol>
									<li>Cuando se selecciona el tipo de habitación.</li>
									<li>Cuando se selecciona el nombre de la habitación. Con esto se muestra el precio de la habitación de acuerdo a la temporada turística.</li>
								</ol>
								<h5>Reto 4</h5>
								<p>Se exponen las siguientes operaciones HTTP:</p>
								<ol start="3">
									<li>Get Client Doc (GET)</li>
									<li>Add client (POST)</li>
								</ol>
								<h5>Reto 5</h5>
								<p>Las anteriores operaciones HTTP se consumen respectivamente en:</p>
								<ol start="3">
									<li>Cuando se digita la cédula del cliente.</li>
									<li>Cuando se solicita crear al cliente, si no existe en la BD.</li>
								</ol>
							</div>
						</template>

						<template #modal-footer="{ ok }">
							<div class="pr-3">
								<b-button size="sm" style="background-color: #0c4c03" class="pt-1 pb-1 pr-3 pl-3" @click="ok()">Aceptar</b-button>
							</div>
						</template>
				</b-modal>
			</div>

			<div id="container-content">
				<receptionProfile/>
			</div>
		</main>

		<footer class="mt-5 text-center"><p>Copyright © 2020 GraphCost - Desarrollado por <strong>E3</strong></p></footer>
   </div>
	
</template>

<script>
	import receptionProfile from './reception_profile';
	import Menu from "./Menu";
	import HeaderApp from "./HeaderApp";

	export default {
		name: 'Reception',
		components:{
			receptionProfile, 
			Menu,
			HeaderApp
		},
		methods: {
			openModal() {
				this.$bvModal.show("modal-center");
			}
		},
		mounted() {
			this.openModal();
		}
	}
</script>

<style scoped>
	#container{
		max-width: 1250px;
		margin: auto;
		background-color: rgb(235,235, 245);
		border-radius: 8px;
		padding-bottom: 40px;
	}
	main {
		display: flex;
		justify-content: space-between;
		z-index: 3;
		margin-top: -77px;
		position: relative;
	}
	#container-content{
		width: 80%;
		background-color: rgb(244, 244, 252);
		padding: 20px;
		border-radius: 8px;
		box-shadow: 10px 20px 30px 0px rgba(223,225,238);
		margin-right: 40px;
	}

	@media screen and (max-width: 991px) {
		#container-content {
			width: 100%;
		}
	}

	@media screen and (max-width: 768px) {
		#container-content {
			margin-right: 20px;
		}
	}

</style>