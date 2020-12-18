<template>
	<div id="image-reception">
	    <h4 id="logo-name" class="font-weight-bolder">{{title}}</h4>
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
    h4#logo-name {
    	padding-top: 45px;
    	padding-right: 80px;
    	text-align: right;
    	color: white;
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
</style>