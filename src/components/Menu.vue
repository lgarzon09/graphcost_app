<template>
	<div id="menu" class="position-relative">
        <div id="navRes">
            <b-button v-b-toggle.sidebar-backdrop id="iconBarMenu"><img src="../assets/imageMenu.png" alt="Menu"></b-button>

            <b-sidebar id="sidebar-backdrop" title="Ana Perez Ortiz" :backdrop-variant="variant" backdrop shadow>
                <p style="margin-left: 15px;margin-bottom: 40px;"><small>Recepcionista</small></p>
                <a id="navResProfile" class="btn_animate"><b-icon icon="person-fill" style="margin-right: 10px"></b-icon>Mi Perfil</a>
                <a id="navResBooking" class="btn_animate isActive"><b-icon icon="calendar2-date" style="margin-right: 10px;"></b-icon>Nueva Reservación</a>
                <a id="navResSession" class="btn_animate"><b-icon icon="power" style="margin-right: 10px;" aria-hidden="true"></b-icon>Cerrar sesión</a>
            </b-sidebar>
        </div>

        <!-- Este se debe mostrar al principio -->
	    <b-nav vertical id="navMain" class="position-relative">
	        <b-nav-item class="position-relative">
	        	<b-button id="navMainProfile" class="btn_nav" style="top: 50px">Mi perfil</b-button>
	        </b-nav-item>
	        <b-nav-item class="position-relative">
	        	<b-button id="navMainBooking" class="btn_nav isActive" style="top: 100px">Nueva Reserva</b-button>
	        </b-nav-item>
	        <b-nav-item class="position-relative">
	        	<b-button id="navMainSession" class="btn_nav" style="top: 150px">Cerrar Sesión</b-button>
	        </b-nav-item>
	    </b-nav>
	</div>
</template>

<script>
	export default {
        name: 'Menu'
    }
</script>

<style>
	#menu{
        width: 18%;
        padding: 10px;
        margin-left: 0px;
    }

    .btn_nav {
        width: 105%;
        height: 50px;
        position: absolute;
        background-color: white !important;
        color: black !important;
        left:-30px;
        border: none !important;
        border-left: 5px solid #0c4c03 !important;
        transition: background 0.5s cubic-bezier(0.1, 0.7, 0.6, 0.9) !important;
        text-align: left !important;
       	padding-left: 15px !important;
       	font-weight: bold !important;
    }

    .btn_nav:hover {
    	background-color: #0c4c03 !important;
    	border-left: 5px solid #0c4c03;
        color: white !important;
    }

    .btn_nav:active {
    	background-color: #0c4c03 !important;
    }

    .btn_nav:focus {
    	background-color: green;
    	border-left: 5px solid #0c4c03;
    }
    
    .btn_animate{
        position: relative;
        display:flex;
        margin: 10px;
        width: 300px;
        height: 50px;
        border: none;
        color: #0c4c03;
        font-weight: bolder;
        text-decoration: none;
        cursor: pointer;
        justify-content: flex-start;
        align-items: center;
        overflow: hidden;
        transition: color 1s;
        border-left: 5px solid #0c4c03 !important;
        padding-left: 20px; /*Aqui voooy*/
    }

    .btn_animate:before{
        display: inline-block;
        content: "";
        position: absolute;
        left:-2px;
        top:0;
        background-color: #0c4c03;
        width: 300px;
        height: 80px;
        z-index: -1;
        transform: translateX(-100%);
        transition: all 1s;
    }

    .btn_animate:hover:before{
        transform: translateX(0);
    }

    .btn_animate:hover{color: white;transition: all 1s;}

    #iconBarMenu {
        position: absolute;
        top: -295px;
        left: 30px;
        background-color: transparent;
        border: none;
    }

    #navRes {
        display: none;
    }

    #sidebar-backdrop {
        padding-top: 30px;
        padding-right: 20px;
        padding-left: 20px;
    }

    b-sidebar#sidebar-backdrop > a {
        text-decoration: none;
    }

    @media screen and (max-width: 991px) {
        /*#menu{width: 8%;}*/
        #navMain {
            display: none;
        }

        #navRes {
            display: block;
        }

        #menu {
            width: 20px;
        }
        /*.topnav{display: none}
        .iconBarMenu{display: block}*/
    }

    .isActive {
        background-color: #0c4c03 !important;
        color: white !important;
    }

</style>