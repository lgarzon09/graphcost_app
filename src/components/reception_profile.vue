<template>
	<div>
		<b-row style="justify-content: center; padding-bottom: 10px;">
			<b-col id="contForm" lg="8" class="pr-0">
				<div id="form-booking">
					<h4 class="mb-4">Nueva Reserva</h4>
					<b-form @submit.prevent="onSubmitNewBooking">
						<b-form-group label="Fecha de Entrada" label-for="datepicker1">
							<b-form-datepicker id="datepicker1" type="date" class="mb-2" required v-model="dateIn"></b-form-datepicker>
						</b-form-group>
						
						<b-form-group label="Fecha de Salida" label-for="datepicker2">
							<b-form-datepicker id="datepicker2" type="date" class="mb-2" required v-model="dateOut"></b-form-datepicker>
						</b-form-group>

						<b-form-group label="Tipo de habitación" label-for="optionsTypeRoom">
							<b-form-select name="option1s" :options="optionsTypeRoom" id="optionsTypeRoom" required v-model="typeRoom"></b-form-select>
						</b-form-group>
						<b-form-group label="Nombre habitación" label-for="optionsRooms">
							<b-form-select :options="optionsRooms" id="optionsRooms" required v-model="chooseRoom"></b-form-select>
						</b-form-group>

						<b-form  @submit.prevent="onSubmitClient">
							<b-form-group label="Cédula del cliente" label-for="input-2" class="mb-1">
								<b-form-input id="input-2" type="text" required v-model="clientCC"></b-form-input>
							</b-form-group>
							<p style="color: #ee5253"><small>{{descpClient}}</small></p>

						
							<b-form-group label="Nombre del cliente" label-for="input-1" class="mb-1">
								<b-form-input id="inputClientName" type="text" required readonly v-model="clientName"></b-form-input>
							</b-form-group>
							<p style="color: #0c4c03"><small>{{descRegister}}</small></p>

							<div v-if="exists" class="text-right">
								<b-button type="submit" variant="link" class="pt-0 pb-0"><small>Crear cliente</small></b-button>
							</div>

							<b-form-group label="Precio de reserva" label-for="input-1" class="mb-1">
								<b-form-input id="input-3" type="text" readonly v-model="costCharged"></b-form-input>
							</b-form-group>
							<!-- <p style="color: #ee5253"><small>{{costCharged}}</small></p> -->


							<!-- <b-icon icon="search" style="color: #7952b3;"></b-icon> -->
						</b-form>

						<div style="text-align: center">
							<b-button id="btn_res" class="font-weight-bolder text-white" type="submit">Reservar</b-button>
							<!-- <b-button id="btn_res" class="font-weight-bolder text-white" type="reset">Resetear</b-button> -->
						</div>
						
					</b-form>

					<b-modal id="modal-scoped">
						<template #modal-title>
							<div class="pl-3">Registro exitoso</div>
						</template>

						<template>
							<div class="pl-5 pr-5 mt-3 d-flex flex-column align-items-center">
								<div class="d-flex mb-3">
									<h5 class="mr-2">Cliente: </h5>
									<p class="mb-1" style="margin-top: 2px;">{{clientName}}</p>
								</div>
								<b-img src="confirmR.jpg" alt="Room" fluid style="max-width: 300px; border-radius: 20px;" class="mb-3"></b-img>
							</div>
							<div class="pl-5 pr-4 mb-4">
								<h5>Precio a pagar:</h5>
								<div style="background-color: #eee; padding-top: 12px; padding-bottom: 12px;">
									<h6 style="text-align: center;" class="mb-0">COP ${{costCharged}}</h6>
								</div>
							</div>
						</template>

						<template #modal-footer="{ cancel }">
							<div class="pr-3">
								<b-button size="sm" style="background-color: #0c4c03" class="pt-1 pb-1 pr-3 pl-3" @click="cleanForm">Aceptar</b-button>
								<b-button size="sm" class="pt-1 pb-1 pr-3 pl-3" @click="cancel()">Cancelar</b-button>
							</div>
						</template>
					</b-modal>
					
				</div>
			</b-col>

			<b-col lg="4" class="pl-2 pr-4" style="margin-top:40px">
				<aside id="indicators-recep">
					<div id="div_icons">
						<b-button class="iconsRedes">
							<img src="../assets/facebook.png" alt="Facebook" class="icon_media">
						</b-button>
						<b-button class="iconsRedes">
							<img src="../assets/whatsapp.png" alt="Whatsapp" class="icon_media">
						</b-button>
						<b-button class="iconsRedes">
							<img src="../assets/instagram.png" alt="Instagram" class="icon_media">
						</b-button>
						<b-button class="iconsRedes">
							<img src="../assets/mail.png" alt="Correo" class="icon_media">
						</b-button>
					</div>
					
					<div id="indicatorsToday">
						<h4 id="indicators" class="mb-4">Indicadores del día</h4>
						<b-row id="dataRow">
							<b-col cols="9" class="font-weight-bolder data">Número de reservas:</b-col>
							<b-col class="text-center align-self-center">{{contador}}</b-col>
						</b-row>
						<hr>
						<b-row id="dataRow">
							<b-col cols="9" class="font-weight-bolder data">Ocupación:</b-col>
							<b-col class="text-center align-self-center">{{ocupacion}}</b-col>
						</b-row>
						<hr>
						<b-row id="dataRow">
							<b-col cols="9" class="font-weight-bolder data">Habitaciones disponibles:</b-col>
							<b-col class="text-center align-self-center">{{habDisponibles}}</b-col>
						</b-row>
						<hr>
					</div>
					
					<div id="reports">
						<h4 style="padding-bottom: 20px;">Reportes</h4>
						<b-button id="btn_reports" class="font-weight-bold"><b-icon icon="search" font-scale="1"></b-icon> informe</b-button>
					</div>
				</aside>
			</b-col>
		</b-row>    
	</div>
</template>

<script>
	import axios from "axios";
	import { debounce } from "lodash";

	export default {
		name: 'receptionProfile',
		data () {
			return {
				contador: 0,
				ocupacion: '--',
				habDisponibles: 0,
				
				selected: "",
				optionsTypeRoom: [
					{value: "", text: "Seleccione una opción"},
				],
				optionsRooms: [
					{value: "", text: "Seleccione una opción"},
				],

				typeRoom: "",
				chooseRoom: "",
				dateIn: "",
				dateOut: "",
				
				clientID: "",
				clientCC: "",
				clientName: "",
				
				descpClient: "",
				descRegister: "",
				exists: false,

				bookingsActive: [],
				occupiedRooms: [],

				costCharged: "",
			}
		},
		watch: {
			typeRoom(newRoom, oldRoom) {
				if (newRoom.length > 0) {
					this.setRoomsOptions();
				}
			},
			dateOut(newDateOut, oldDateOut) {
				if (newDateOut.length > 0) {
					this.findBookingsActive();
				}
			},
			clientCC(newClient, oldClient) {
				this.clientName = "";
				this.descRegister = "";
				this.exists = false;
				if (newClient.length > 0) {
					this.descpClient = "Buscando...";
					this.debouncedGetClient();
				} else {
					this.descpClient = "";
				}
			},
			bookingsActive(newBoo, oldBoo) {
				if (this.typeRoom.length > 0) {
					this.setRoomsOptions();
				}
			},
			chooseRoom(newNameRoom, oldNameRoom) {
				if (newNameRoom.length > 0) {
					this.getPriceCharged();
				}
			}
		},
		methods: {
			setTypeRoomOptions() {
				axios.get("https://graphcode-api.herokuapp.com/rooms/", { headers: {
					"Access-Control-Allow-Origin": "https://graphcode-api.herokuapp.com/",
					"Access-Control-Allow-Methods": "GET",
					"Access-Control-Allow-Headers": "Content-Type",
					"Access-Control-Max-Age": 86400
				} })
				.then((result) => {
					for (let room of result.data) {
						this.optionsTypeRoom.push({
							value: room["roo_type"], 
							text: room["roo_description"]
						})
					}
				})
				.catch((error) => {
					console.log(error) //Arreglar sintaxis
				})
			},
			setRoomsOptions() {
				if (this.dateIn === "" || this.dateOut === "") {
					alert("Por favor, ingrese una fecha de entrada y de salida.")
				} else {

					let filtered = this.bookingsActive.filter(booking => booking.boo_name_roo[0] === this.typeRoom);

					for (let booking of filtered) {
						this.occupiedRooms.push(booking.boo_name_roo);
					}

					let setRooms = new Set(this.occupiedRooms);

					axios.get("https://graphcode-api.herokuapp.com/rooms/" + this.typeRoom, { headers: {
							"Access-Control-Allow-Origin": "https://graphcode-api.herokuapp.com/",
							"Access-Control-Allow-Methods": "GET",
							"Access-Control-Allow-Headers": "Content-Type",
							"Access-Control-Max-Age": 86400
						} })
					.then((result) => {
						this.habDisponibles = 0;
						let totalRooms = result.data.roo_total;
						this.optionsRooms = [{value: "", text: "Seleccione una opción"},];
						for (let i = 1; i <= totalRooms; i++) {
							let nameRoom = this.typeRoom + i;
							if (!setRooms.has(nameRoom)) {
								this.optionsRooms.push({
									value: nameRoom, 
									text: nameRoom
								});
								this.habDisponibles += 1;
							}
						}
					})
					.catch((error) => {
						console.log(error) //Arreglar sintaxis
					})
				}
			},
			findBookingsActive() {
				axios.get(`https://graphcode-api.herokuapp.com/bookings/?dateIn=${this.dateIn}&dateOut=${this.dateOut}`, {
					headers: {
						"Access-Control-Allow-Origin": "https://graphcode-api.herokuapp.com/",
						"Access-Control-Allow-Methods": "GET",
						"Access-Control-Allow-Headers": "Content-Type",
						"Access-Control-Max-Age": 86400
					}
				})
				.then((result) => {
					this.bookingsActive = this.bookingsActive.concat(...result.data);
					this.chooseRoom = "";
				})
				.catch((error) => {
					console.log(error);
				})
			},
			getClient() {
				let inputName = document.getElementById("inputClientName");
				inputName.setAttribute("readonly", true);

				if (this.clientCC > 0) {
					this.exists = false;
					this.descpClient = 'Buscando...';
				}

				if (this.clientCC.length >= 7) {
					axios.get("https://graphcode-api.herokuapp.com/clients/" + this.clientCC, {
						headers: {
							"Access-Control-Allow-Origin": "https://graphcode-api.herokuapp.com/",
							"Access-Control-Allow-Methods": "GET",
							"Access-Control-Allow-Headers": "Content-Type",
							"Access-Control-Max-Age": 86400
						}
					})
					.then((result) => {
						this.clientName = result.data.cli_name;
						this.clientID = result.data.cli_id;
						this.descpClient = "";
					})
					.catch((error) => {
						if (error.response) {
							inputName.removeAttribute("readonly");
							this.descpClient = error.response.data.detail;
							this.clientName = "";
							this.exists = true;
						}
					})
				} else {
					this.descpClient = "Ingrese una cédula válida."
				}
			},
			onSubmitClient() {
				let inputName = document.getElementById("inputClientName");
				let form = {
					cli_name: this.clientName,
					cli_docNumber: this.clientCC
				}
				
				axios.post("https://graphcode-api.herokuapp.com/clients/new/", JSON.stringify(form), {
					headers: {
						"Access-Control-Allow-Origin": "https://graphcode-api.herokuapp.com/",
						"Access-Control-Allow-Methods": "GET",
						"Access-Control-Allow-Headers": "Content-Type",
						"Access-Control-Max-Age": 86400
					}
				})
				.then((result) => {
					this.descRegister = "Registro exitoso.";
					this.clientID = result.data.cli_id;
					this.descpClient = "";
					this.exists = false;
					inputName.setAttribute("readonly", true);
				})
				.catch((error) => {
					console.log(error);
				})
			},
			getPriceCharged() {
				let form = {
					boo_cli_id: 0,
					boo_dateIN: this.dateIn,
					boo_dateOUT: this.dateOut,
					boo_roo_id: 1,
					boo_name_roo: this.chooseRoom,
					boo_rec_id: 1,
					boo_price_charged: 0
				}

				axios.post("https://graphcode-api.herokuapp.com/bookings/price/", JSON.stringify(form), {
					headers: {
						"Access-Control-Allow-Origin": "https://graphcode-api.herokuapp.com/",
						"Access-Control-Allow-Methods": "GET",
						"Access-Control-Allow-Headers": "Content-Type",
						"Access-Control-Max-Age": 86400
					}
				})
				.then((result) => {
					this.costCharged = result.data;
					// this.$bvModal.show("modal-scoped");
				})
				.catch((error) => {
					console.log(error)
				})
			},
			onSubmitNewBooking() {
				if (this.clientID.length <= 0 || this.clientName.length <= 0) {
					this.descpClient = "Por favor ingrese un cliente";
				} else {
					let form = {
						boo_cli_id: this.clientID,
						boo_dateIN: this.dateIn,
						boo_dateOUT: this.dateOut,
						boo_roo_id: 1,
						boo_name_roo: this.chooseRoom,
						boo_rec_id: 1,
						boo_price_charged: this.costCharged
					}

					axios.post("https://graphcode-api.herokuapp.com/bookings/new/", JSON.stringify(form), {
						headers: {
							"Access-Control-Allow-Origin": "https://graphcode-api.herokuapp.com/",
							"Access-Control-Allow-Methods": "GET",
							"Access-Control-Allow-Headers": "Content-Type",
							"Access-Control-Max-Age": 86400
						}
					})
					.then((result) => {
						this.descRegister = "";
						this.$bvModal.show("modal-scoped");
						this.contador += 1;
					})
					.catch((error) => {
						console.log(error)
					})
				}
			},
			cleanForm() {
				this.$bvModal.hide("modal-scoped");
				this.dateIn = "";
				this.dateOut = "";
				this.typeRoom = "";
				this.chooseRoom = "";
				this.clientCC = "";
				this.clientName = "";
				this.costCharged = "";
				this.bookingsActive = [];
			}
		},
		created() {
			this.setTypeRoomOptions();
			this.debouncedGetClient = _.debounce(this.getClient, 1000)
		}
	}
</script>

<style scoped>
	aside#indicators-recep {
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		align-content: space-between;
		height: 100%; 
	}

	#form-booking {
		padding: 45px;
		background-color: white;
		border-radius: 8px;
		margin: 20px;
		box-shadow: 2px 3px 12px 6px rgba(223,225,238);
	}   

	.data {
		color:#0c4c03;   
	}

	#dataRow {
		padding-bottom: 10px;
	}

	#btn_reports {
		align-self: center;
		padding-top: 6px;
		padding-bottom: 6px;
		width: 90%;
		border-radius: 5px;
		border-color: #0c4c03;
		border-width:2px;
		background-color: white;
		color: #0c4c03;
	}

	#reports{
		display: flex;
		flex-direction: column;
		text-align: center;
		background-color: white;
		border-radius: 8px;
		padding: 30px 20px;
		margin-top: 20px;
		margin-bottom: 20px;
		margin-right: 10px;
		box-shadow: 2px 3px 12px 6px rgba(223,225,238);
	}

	#btn_res{
		border-radius: 20px;
		width: 40%;
		background-color: #0c4c03;
		margin-top: 30px;
		box-shadow: 0 10px 13px -2px #ced6e0;
		letter-spacing: 1px;
		word-spacing: 2px;
	}

	.iconsRedes {
		width: 40px;
		height: 40px;
		margin-right: 10px;
		background-color: transparent !important;
		border: none;
		padding: 0;
	}

	.icon_media {
		width: 40px;
	}

	#btn_res{
		border-radius: 20px;
		width: 40%;
		background-color: #0c4c03;
		margin-top: 30px;
		box-shadow: 0 10px 13px -2px #ced6e0;
		letter-spacing: 1px;
		word-spacing: 2px;
	}

	#icons{
		background-color: white;
		width: 20%;
		margin-right: 5px;
	}

	#icon_media{
		width: 130%;
	}

	#div_icons{
		display: flex;
		justify-content: center; 
		padding-bottom: 65px;
	}

	@media screen and (max-width: 991px) {
		#btn_res{
			width: 80%;
		}

		#icon_media{
			width: 50%;
		}

		#indicators-recep{
			padding-left: 30px;
		}

		aside#indicators-recep {
			flex-direction: row;
			flex-wrap: wrap;
		}

		aside#indicators-recep div#div_icons {
			flex: 1 1 100%;
		}

		aside#indicators-recep div#indicatorsToday {
			flex: 2 1 350px;
			padding-right: 40px;
		}

		aside#indicators-recep div#reports {
			flex: 1 1 200px;
			align-self: center;
		}
	}

	@media screen and (max-width: 768px) {

		#contForm {
			padding-left: 0px;
		}

		aside#indicators-recep div#indicatorsToday {
			padding-right: 0px;
			max-width: 350px;
			margin: auto;
		}

		aside#indicators-recep div#indicatorsTody h4#indicators {
			text-align: center;
		}

		aside#indicators-recep div#reports {
			max-width: 3500px;
			margin: auto;
			margin-top: 40px;
			margin-bottom: 20px;
		}
	}

	@media screen and (max-width: 500px) {
		#form-booking {
			padding: 30px;
		}
	}

</style>
