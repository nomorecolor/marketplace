<template>
    <div class="rl">
        <div class="d-flex flex-column">
            <!-- <div class="upper-label">
               WEAPONS
            </div> -->
             <div class="tabs"  v-bind:class="{ upperLabel: !weapons == '' }" id="weapon" @click="selectTab('weapon')">
               WEAPONS
            </div>
            <transition name="fadeInUp" mode="out-in">
                <component v-bind:is="weapons" />
            </transition>
            <div class="tabs"  v-bind:class="{ upperLabel: !shields == '' }" id="shield" @click="selectTab('shield')">
               SHIELDS & ARMORS
            </div>
            <transition name="fadeInUp" mode="out-in">
                <component v-bind:is="shields" />
            </transition>
            <div class="tabs"  v-bind:class="{ upperLabel: !character == '' }" id="character" @click="selectTab('character')">
               CHARACTERS
            </div>
            <transition name="fadeInUp" mode="out-in">
                <component v-bind:is="character" />
            </transition>
            <div class="tabs"  v-bind:class="{ upperLabel: !skill == '' }" id="skillshop" @click="selectTab('skillshop')">
               SKILL SHOP
            </div>
            <div class="tabs"  v-bind:class="{ upperLabel: !others == '' }" id="others" @click="selectTab('others')">
               OTHER NFT
            </div>
            <transition name="fadeInUp" mode="out-in">
                <component v-bind:is="others" />
            </transition>
            <div class="log-out csr-pointer">
                <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" aria-hidden="true" role="img" width="1em" height="1em" preserveAspectRatio="xMidYMid meet" viewBox="0 0 24 24"><path d="M4 18h2v2h12V4H6v2H4V3a1 1 0 0 1 1-1h14a1 1 0 0 1 1 1v18a1 1 0 0 1-1 1H5a1 1 0 0 1-1-1v-3zm2-7h7v2H6v3l-5-4l5-4v3z" fill="currentColor"/></svg>
                <span>Logout</span>
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import Vue from 'vue';
import Filters from '../components/Filters.vue'

export default Vue.extend({
    name: 'MarketFilter',
    components:{'filters':Filters},
    data: function(){
        return{
            weapons: 'filters',
            shields: "",
            character: "",
            skill: "",
            others: "",
            activeUppderMidTab: "w",
            activeBottomTab: 'f',
            elements:[
                {
                    id: 1,
                    el: 'earth',
                    isToggled: true
                },
                {
                    id: 2,
                    el: 'fire',
                    isToggled: false
                },
                {
                    id: 3,
                    el: 'water',
                    isToggled: false
                },
                {
                    id: 4,
                    el: 'lightning',
                    isToggled: false
                }
            ],
        }
    },
    methods:{
        selectTab(tab:string){
            if(tab == 'weapon'){
                this.$root.$emit('refresh-list', 'weapon')
                this.weapons = 'filters'
                this.shields = ""
                this.character = ""
                this.skill = ""
                this.others = ""
            }else if(tab == 'shield'){
                this.shields = 'filters'
                this.weapons = ''
                this.character = ""
                this.skill = ""
                this.others = ""
            }else if(tab == 'character'){
                this.$root.$emit('refresh-list', 'character')
                this.character = 'filters'
                this.shields = ''
                this.weapons = ''
                this.skill = ""
                this.others = ""
            }else if(tab == 'skillshop'){
                this.$root.$emit('refresh-list', 'skillshop')
                this.skill = 'filters'
                this.character = ''
                this.shields = ''
                this.weapons = ''
                this.others = ""
            }else if(tab == 'others'){
                this.others = 'filters'
                this.skill = ''
                this.character = ''
                this.shields = ''
                this.weapons = ''
            }
        },
        clickedFilter(x:string){
            if(x=='f'){
                this.$root.$emit('filter-value', false)
            }
            this.activeBottomTab=x
        },
        setActive(tab:string,types:string){
            if(types=='upperMidBtn'){
                if(tab==this.activeUppderMidTab){
                    return 'border-bottom: 3px solid #1168d0 !important;'
                }else{
                    return 'border-bottom: 3px solid #08142b !important;'
                }
            }else if(types=='bottomBtn'){
                if(tab==this.activeBottomTab){
                    return '  background-color: #1168d0;color: #fff;'
                }else{
                    return ' background-color: #08142b; color: #fff; border: 1px solid rgba(255, 255, 255, 0.357);'
                }
            }
            
        },
        setElement(el:string){
            for(var x in this.elements){
                if(el== this.elements[x].el && this.elements[x].isToggled){
                    this.elements[x].isToggled = false
                }else if(el== this.elements[x].el && !this.elements[x].isToggled ){
                    this.elements[x].isToggled = true
                }
            }
        },
        getElement(stat:boolean,el:string){
            if(stat){
                return el
            }else{
                return el+'-off'
            }
        }
    }
});

</script>

<style scoped>
    .rl{
        overflow-y: auto !important;
    }
</style>
