<template>
    <div class="list">
        <article v-for="(pokemon,index) in pokemons"
        :key="'poke' + index"
        @click="setPokemonUrl(pokemon.url)">

        <img :src="imageUrl + pokemon.id + '.png'" width="96" height="96" alt="">
        <h3>{{ pokemon.name }}</h3>
        </article>

        <div id="scroll-trigger" ref="infinitescrolltrigger">
            <i class="fas fa-spinner fa-spin"></i>
      </div>
    </div>  
</template>

<script>
export default {
    props: [
    'imageUrl',
    'apiUrl'
    ],
    data:() => {
        return {
            pokemons:[],
            nextUrl : '',
            currentUrl : '',
        }
    },

    methods:{
        /*API functions which call the data required.
        Uses the Fetch API by Vue. 
        Code 200 = Success in fetch. Data returned in JSON format
        */
        fetchData() {
            let req = new Request(this.currentUrl);
            fetch(req).then ((resp) =>
            {
                if(resp.status == 200)
                return resp.json();
            })
            /*The next data is stored in nextUrl variable
            - The results of the data for each pokemon is stored into the id variable. 
            - The url is split using the "/"" symbol. 
            - Non null values will be removed using pop and returned*/
            .then((data) => {
                this.nextUrl = data.next;
                data.results.forEach(pokemon => {
                    pokemon.id = pokemon.url.split('/')
                    .filter(function(part){return !!part}).pop();
                    this.pokemons.push(pokemon);   
                });``

            })
            //Exception handling if error, shows error in console log
            .catch((error) =>
            {
                console.log(error);
            })
        },

        /*Intersection observer API used for unlimited scrolling 
        - For every Pokemon wnrey, the scrolling will continue. 
        - Intersection ratio shows how much of the entry is visible 
          within the root intersection rectangle. 
        - Non null values will be removed using pop and returned*/
        scrollTrigger()
        {
            const observer = new IntersectionObserver((entries) => {
                entries.forEach(entry => {
                    if(entry.intersectionRatio > 0 && this.nextUrl)
                    {
                        this.next();
                    }
                });
            });
            /*$ shows that a property is defined elsewhere 
              and not within the current component.*/
            observer.observe(this.$refs.infinitescrolltrigger);
        },
        next()
        {
            this.currentUrl = this.nextUrl;
            this.fetchData();
        },
        setPokemonUrl(url)
        {
            this.$emit('setPokemonUrl', url)
        }
    },
    created()
    {
        this.currentUrl = this.apiUrl;
        this.fetchData();
    },
    mounted()
    {
        this.scrollTrigger();
    }
}
</script>

<style lang="scss" scoped>

.list {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
    grid-gap: 10px;
    width: 100%;
    max-width: 510px;
    article {
      height: 150px;
      background-color: #efefef;
      text-align: center;
      text-transform: capitalize;
      border-radius: 5px;
      cursor: pointer;
      box-shadow: 0 15px 30px rgba(0,0,0,.2),
                  0 10px 10px rgba(0,0,0,.2);
      h3 {
        margin: 0;
      }
    }
  }

  #scroll-trigger
  {
      display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 150px;
    font-size: 2rem;
    color: #efefef;
  }

</style>
