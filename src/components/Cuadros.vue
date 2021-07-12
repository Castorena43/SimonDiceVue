<template>
    <div class="container">
        <div class="flex1">
            <div class="cuadro cuadro1" v-bind:class="{ on : isActive[0]}" v-on:click="checar($event)" id="1">
            
            </div>
            <input type="button" v-on:click="desordenar()" value="Jugar" class="jugar">
            <div class="cuadro cuadro2" v-bind:class="{ on : isActive[1]}" v-on:click="checar($event)" id="2">
                
            </div>
        </div>
        <div class="flex2">
            <div class="cuadro cuadro2" v-bind:class="{ on : isActive[2]}" v-on:click="checar($event)" id="3">
                
            </div>
        </div>
        <div class="flex3">
            <div class="cuadro cuadro1" v-bind:class="{ on : isActive[3]}" v-on:click="checar($event)" id="4">
                
            </div>
            <div class="cuadro cuadro2" v-bind:class="{ on : isActive[4]}" v-on:click="checar($event)" id="5">
                
            </div>
        </div>
       
        
    </div>
    
</template>

<script>
export default {
     name: 'Cuadros',
     data() {
         return {
             order: [1,2,3,4,5],
             uno: false,
             active: 'on',
             inactive: 'off',
             isActive: [false,false,false,false,false],
             intento: [],
             jugar: false
         }
     },
     mounted() {
     },
     methods: {
        sleep: function(ms) {
            return new Promise(resolve => setTimeout(resolve, ms));
        },
         desordenar: function() {
             this.order.sort(function() { return Math.random() - .5});
             this.mostrar()
        },
        mostrar: async function(){
            for (let ord of this.order){   
                switch (ord){
                    case 1:
                        this.isActive[ord-1] = true;
                        await this.sleep(1000);
                        this.isActive[ord-1] = false;
                        break;
                    case 2:
                        this.isActive[ord-1] = true;
                        await this.sleep(1000);
                        this.isActive[ord-1] = false;
                        break;
                    case 3:
                        this.isActive[ord-1] = true;
                        await this.sleep(1000);
                        this.isActive[ord-1] = false;
                        break;
                    case 4:
                        this.isActive[ord-1] = true;
                        await this.sleep(1000);
                        this.isActive[ord-1] = false;
                        break;
                    case 5:
                        this.isActive[ord-1] = true;
                        await this.sleep(1000);
                        this.isActive[ord-1] = false;
                        break;
                }
            }
            this.jugar = true;
            this.$swal({
                    title: 'Empieza el juego!',
                    icon: 'info'
                });
        },
        checar: function(event){
            if (this.jugar !== true) { return }
            let id = parseInt(event.srcElement.id);
            this.intento.push(id);
            if (this.intento.indexOf(id) !== this.order.indexOf(id)){
                this.$swal({
                    title: 'Error!',
                    text: 'Haz Fallado!!',
                    icon: 'error'
                });
                this.jugar = false;
                this.intento = [];
            }
            if (this.intento.length === this.order.length){
                this.$swal({
                    title: 'HAZ GANADO!',
                    text: 'VICTORIA!!',
                    icon: 'success'
                });
                this.jugar = false;
                this.intento = [];
                for(let i of this.isActive){
                    this.isActive[i] = false;
                }
            }
        }
     }
}
</script>

<style>
.on{
    background-color: #C62121;
}
.off{
    background-color: white;
}
.container {
    display: flex;
    flex-direction: column;
    height: 100vh;
    justify-content: space-between;
}

.flex1 {
    display: flex;
    justify-content: space-between;
}
.flex2 {
    display: flex;
    justify-content: center;
    align-items: center;
}
.flex3 {
    display: flex;
    justify-content: space-between;
}

.cuadro{
    height: 150px;
    width: 150px;
    border: 1px solid black;
}

.jugar {
    height: 25px;
}

</style>