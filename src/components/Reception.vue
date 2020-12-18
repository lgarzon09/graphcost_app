<template>
   <div id="container">
        <header>
            <HeaderApp/>
        </header>
       
        <main class="mb-4">
            <Menu/>
            
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
        }
    }
</script>

<style scoped>
    #container{
        width: 90%;
        margin: auto;
        background-color: rgb(235,235, 245);
        margin-top: 50px;
        margin-bottom: 50px;
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
        #container-content{width: 100%;}
    }

</style>