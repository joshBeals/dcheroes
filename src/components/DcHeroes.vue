<template>
    <h1 style="text-align: center;">{{ title }} ({{ heroesCount }})</h1>
    <br><br>
    <div style="display: flex; justify-content: center; align-items: center; margin-bottom: 50px;" v-if="heroesCount === 0">
      <img style="height: 100px;" :src="require('../assets/superheroe.svg')" alt="Superhero">
    </div>
    <div style="display: flex; flex-direction: column; justify-content: center; align-items: center;">
      <div>
        <div style="display: flex; margin-bottom: 20px;" v-for="(hero, index) in heroes" :key="hero.name">
          <h5 style="margin: 0; padding: 0; margin-right: 10px;">{{index+1}}.</h5>
          <div style="max-width: 200px; word-wrap: break-word;">
            <h5 style="margin: 0; padding: 0;">{{hero.name}} </h5>
          </div>
          <div style="flex: 1; display: flex; justify-content: flex-end; align-items: center; margin: 0px 20px;" @click="removeHero(index)">
            <i class="far fa-trash-alt text-danger"></i>
          </div>
        </div>
      </div>
      <form @submit.prevent="addHero">
        <input class="form-control" v-model="newHero" placeholder="Type Hero Name Here">
        <div style="flex: 1; display: flex; justify-content: center; align-items: center; margin-top: 5px;">
          <button type="submit" class="btn btn-sm btn-secondary">Add Hero</button>
        </div>
      </form>
    </div>
</template>

<script>
    export default {
        computed:{
            heroesCount(){
                return this.heroes.length
            }
        },
        methods:{
            addHero(){
                if(this.newHero !== ''){
                    console.log(this.heroes.indexOf(this.newHero));
                    let hero = this.heroes.filter((hero) => hero.name == this.newHero);
                    if(hero.length == 0){
                        this.heroes.push({name: this.newHero});
                        this.newHero = '';
                    }else{
                        alert('Hero has already been added');
                    }
                }else{
                    alert('No hero entered');
                }
            },
            removeHero(index){
                this.heroes = this.heroes.filter((hero, i) => i !== index);
            }
        },
        data(){
            return {
                title: "DC Heroes",
                newHero: "",
                heroes: [
                
                ],
            }
        }
    }
</script>

<style>

</style>