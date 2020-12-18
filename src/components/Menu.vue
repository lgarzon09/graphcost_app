<template>
	<div id="menu" class="position-relative">
        <div>
            <b-button v-b-toggle.sidebar-backdrop class="iconBarMenu"><img src="../assets/imageMenu.png" alt="Menu"></b-button>

            <b-sidebar id="sidebar-backdrop" title="Ana Perez Ortiz" :backdrop-variant="variant" backdrop shadow>
                <p style="margin-left: 20px;margin-bottom: 40px;">Recepcionista</p>
                <a class="btn_animate"><b-icon icon="person-fill" style="margin-right: 10px"></b-icon>Mi Perfil</a>
                <a class="btn_animate"><b-icon icon="calendar2-date" style="margin-right: 10px;"></b-icon>Nueva Reservación</a>
                <a class="btn_animate"><b-icon icon="power" style="margin-right: 10px;" aria-hidden="true"></b-icon>Cerrar sesión</a>
            </b-sidebar>
        </div>


	    <b-nav vertical class="position-relative topnav" id="myTopnav">
	        <b-nav-item class="position-relative">
	        	<b-button class="btn_nav" style="top: 50px">Mi perfil</b-button>
	        </b-nav-item>
	        <b-nav-item class="position-relative">
	        	<b-button class="btn_nav" style="top: 100px">Nueva Reserva</b-button>
	        </b-nav-item>
	        <b-nav-item class="position-relative">
	        	<b-button class="btn_nav" style="top: 150px">Cerrar Sesión</b-button>
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
        width: 100%;
        height: 50px;
        position: absolute;
        background-color: white;
        color: black;
        left:-30px;
        border: none;
        border-left: 5px solid #0c4c03;
        transition: background 0.5s cubic-bezier(0.1, 0.7, 0.6, 0.9);
        text-align: left;
       	padding-left: 30px;
       	font-weight: bold;
    }

    .btn_nav:hover {
    	background-color: #0c4c03;
    	border-left: 5px solid #0c4c03;
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
        justify-content: center;
        align-items: center;
        overflow: hidden;
        transition: color 1s;
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

    .iconBarMenu{
        display: none;
        position: absolute;
        top: -295px;
        left: 30px;
        background: none;
        border: none;
    }

    @media screen and (max-width: 991px) {
        #menu{width: 8%;}
        .topnav{display: none}
        .iconBarMenu{display: block}
    }

</style>