<template>
	<div id="image-reception">
	    <!-- <h4 id="logo-name" class="font-weight-bolder">{{title}}</h4> -->
        <div id="logoGC">
            <b-img id="logo-leyend" :src="require('../assets/LogoW.png')" style="max-width: 125px;" fluid alt="Responsive image"></b-img>
            <b-img id="only-logo" :src="require('../assets/LogoGCW.png')" style="max-width: 60px;" fluid alt="Responsive image"></b-img>
        </div>
	    <div id="avatar">
	    	<b-avatar variant="light" :src="require('../assets/imageUser.jpg')" size="9rem" style="padding: 7px;"></b-avatar>
	    </div>
	    <h4 id="name-receptionist" class="font-weight-bolder">{{receptionist}}</h4>
	    <h6 id="rol">{{rol}}</h6>
    </div>
</template>

<script>
	export default {
		name: "HeaderApp",
		data () {
            return {
                title: 'GraphCost',
                receptionist: "Ana Perez Ortiz",
                rol: 'Recepcionista',
            }
        }
	}
</script>

<style>
    #logoGC {
        padding-top: 35px;
        padding-right: 45px;
        display: flex;
        justify-content: flex-end;
    }

    h4#name-receptionist {
    	color: white;
    	text-align: center;
    	letter-spacing: 1px;
    	text-shadow: 1px 1px 2px black;
    }

    h6#rol {
    	color: white;
    	text-align: center;
    	letter-spacing: 2px;
    	text-shadow: 1px 1px 2px black;
    }

    #avatar {
    	width: 100%;
    	display: flex;
    	justify-content: center;
        margin-top: -10px;
    }

    #image-reception{
        width:100%;
        height: 400px;
        border-top-left-radius: 8px;
        border-top-right-radius: 8px;
        background: linear-gradient(to bottom, rgba(0,0,0,0), rgba(0,0,0,0.6)), url("../assets/imageReception.jpg");
        background-repeat: no-repeat;
        background-size: cover;
        background-position: center;
        position: relative;
        z-index: 1;
    }

    #only-logo {
        display: none;
    }

    @media screen and (max-width: 768px) {
        #only-logo {
            display: block;
        }

        #logo-leyend {
            display: none;
        }
    }
</style>