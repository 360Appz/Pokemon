<!--{{}} - Acts as data binding placeholders, 
the HTML element will change when Vue object changes
-->

<template>

    <div class="detail">
        <div class="detail-view" v-if="show">
            <div v-if="pokemon" class="image">
                <img :src="imageUrl + pokemon.id + '.png'" alt="">
            </div>
           <div v-if="pokemon" class="data">
               <h2>{{pokemon.name}}</h2>
               <div class="property">
                   <div class="left">Base Experience</div>
                   <div class="right">{{pokemon.base_experience}} XP</div>
                   </div> 


                   <div class="property">
                       <div  class="left">Item </div>
                       <div class="right" 
                      v-for="(value, index) in pokemon.held_items"
                      :key="'value'+index">
                      {{ value.item.name }}
                       </div>

                        <div v-if="pokemon.held_items == 0" class="right" >
                          None
                       </div>
                   </div>

                   <div class="property">
                       <div  class="left"> Base Stat </div>
                       <div class="right" 
                      v-for="(value, index) in pokemon.stats"
                      :key="'value'+index">
                      {{ value.base_stat}}
                       </div>   

                         <div v-if="pokemon.stats == null">
                          No stat availalbe
                       </div>

                   </div>

                    <div class="property">
                       <div  class="left"> Type </div>
                       <div class="right" 
                      v-for="(value, index) in pokemon.types"
                      :key="'value'+index">
                      {{ value.type.name}}
                       </div> 

                      <div v-if="pokemon.types == null " class="right">
                          Not available
                       </div>

                   </div>

                       
     

                <h3> Pokemon Types </h3>
                <div class="types">
                <div class="type" 
                v-for="(value, index) in pokemon.types"
                :key="'value'+index">
                {{ value.type.name }}
                  </div>
                </div>
           
          <h3> Abilities </h3>
          <div class="abilities">
            <div class="ability" 
                v-for="(value, index) in pokemon.abilities"
                :key="'value'+index">
                {{ value.ability.name }}
              </div>
            </div>
          </div>
          <h2 v-else>Invalid Pokemon. Check spelling </h2>
          <button class="close" @click="closeDetail">close</button>
        </div>
           <i v-else class="fas fa-spinner fa-spin"></i>
        </div>
      
</template>

<script>

export default {

    props: [
        'pokemonUrl',
        'imageUrl'
    ],
    data: () => {
        return {
            show: false,
            pokemon: {}
        }
    },
    methods: {
        fetchData()
        {
            let req = new Request(this.pokemonUrl);
            fetch(req)
            .then((resp) => {
              //Shows that request has succeeded
                if(resp.status == 200)
                return resp.json();
            })
            .then((data) => {
                this.pokemon = data;
                this.show = true;
            })
            .catch((error) => {
                console.log(error);
            })
        },
        closeDetail()
        {
            this.$emit('closeDetail');
        }
    },
    created()
    {
        this.fetchData();
    }
}
</script>

<style lang="scss" scoped>
  .detail {
    animation: ease-in 60s;
    display: flex;
    justify-content: center;
    align-items: flex-start;
    position: fixed;
    top: 0;
    left: 0;
    padding: 90px 10px 10px;
    width: calc(100% - 20px);
    height: calc(100vh - 20px);
    background: rgba($color: #000000, $alpha: .7);
    .detail-view {
      display: flex;
      justify-content: center;
      align-items: center;
      flex-direction: column;
      position: relative;
      width: 100%;
      max-width: 510px;
      padding: 50px 0 0;
      background-color: #fff;
      border-radius: 5px;
      box-shadow: 0 15px 30px rgba(0,0,0,.2),
                  0 10px 10px rgba(0,0,0,.2);
    
      .image {
        display: flex;
        justify-content: center;
        align-items: center;
        position: absolute;
        top: -60px;
        width: 120px;
        height: 120px;
        background-color: #333;
        border-radius: 50%;
        overflow: hidden;
        box-shadow: 0 15px 30px rgba(0,0,0,.2),
                    0 10px 10px rgba(0,0,0,.2);
      }
      h2 {
        text-transform: capitalize;
      }
      .data {
        display: flex;
        justify-content: flex-start;
        align-items: center;
        flex-direction: column;
        width: 100%;
        margin-bottom: 40px;
        .property {
          width: 90%;
          max-width: 400px;
          border-bottom: 1px solid #ccc;
          margin-bottom: 10px;
          .left { float: left; }
          .right { float: right; }
        }
        h3 {
          width: 90%;
          max-width: 400px;
          border-bottom: 1px solid #ccc;
        }
        .types, .abilities {
          display: flex;
          justify-content: flex-start;
          flex-wrap: wrap;
          width: 90%;
          max-width: 400px;
          .type, .ability {
            margin: 0 10px 10px 0;
            padding: 5px 10px;
            border-radius: 20px;
            color: rgb(0, 0, 0);
            font-size: 1rem;
            letter-spacing: 2px;
            text-transform: capitalize;
            word-wrap: none;
            word-break: keep-all;
          }
          .type { background-color: #8CFA4B; }
          .ability { background-color: #ED8E53; }
        }
      }
      .close {
        outline: none;
        border: none;
        border-radius: 5px;
        background-color: #333;
        color: #efefef;
        padding: 10px 20px;
        margin-bottom: 20px;
        font-size: 1.2rem;
        cursor: pointer;
      }
    }
    i {
      font-size: 2rem;
      color: #efefef;
    }
  }
</style>

