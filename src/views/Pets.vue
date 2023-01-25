<template>
<div>


  
<Header />

<!-- start banner Area -->
<section class="banner-area relative" id="home">	
				<div class="overlay overlay-bg"></div>
				<div class="container">				
					<div class="row d-flex align-items-center justify-content-center">
						<div class="about-content col-lg-12">
							<h1 class="text-white">
								Dogs				
							</h1>
						</div>	
					</div>
				</div>
			</section>
			<!-- End banner Area -->	
				
			<!-- Start pet-list Area -->
			<section class="cat-list-area section-gap">
				<div class="container">
					<div class="row">
						<div v-for="pet in filteredPets" :key="pet.id" class="col-lg-3 col-md-6">
							<div class="single-cat-list">
							  <img :src="require(`../../public/img/${pet.image}`)"  alt="" class="img-fluid">
							  <div class="overlay">
							    <div class="text">
								<p>    I am {{pet.name}}!</p>
								<p><a v-if="!userIsEmptyComputed" @click="adoted(pet)" href="#" style="color: white"><u>Adopt me!</u></a></p>
								</div>
							  </div>
							</div>
						</div>											
					</div>
				</div>	
			</section>
			<!-- End pet-list Area -->


				
	



<Footer />

</div>
</template>

<script>
import Footer from '@/components/Footer.vue'
import Header from '@/components/Header.vue'

export default {

    components: {
        Footer,
        Header
    },
  

    data() {
        return {
            pets:[],
            newAdoption:{
                pet_name:'',
                pet_id:'',
                pet_image:'',
                petlover_id:'',
            }
        }
    },
    created() {
        this.fetchPets();
    },
    methods: {       
        async fetchPets() {
            await this.$store.dispatch('pets/getPetsFromDB');
            this.pets = this.$store.getters['pets/getpets'];
            console.log(this.pets)
        },

        adoted(pet){
            console.log(pet);
            this.newAdoption.petlover_id=this.$store.getters['user/getUser'].id;
            this.newAdoption.pet_id=pet.id;
            this.newAdoption.pet_image=pet.image;
            this.newAdoption.pet_name=pet.name;

            this.$store.dispatch('adoptions/newAdoption', this.newAdoption);

            localStorage.setItem('message', '"Success! Pet adopted!');
			this.$router.push({ path: '/message' });

        }

       
    },
    computed: {
        filteredPets() {
            return this.pets.filter(pet => pet.status === "0")
        },

        userIsEmptyComputed: function() {
            let obj = this.$store.getters['user/getUser']
            return Object.keys(obj).length === 0;
            
        },
    }
 
}
</script>

<style scoped>


</style>