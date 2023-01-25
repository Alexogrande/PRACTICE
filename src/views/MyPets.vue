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
								My pets !				
							</h1>
						</div>	
					</div>
				</div>
			</section>
			<!-- End banner Area -->	
				
			<!-- Start pet-list Area -->
			<section class="cat-list-area section-gap">
				<div class="container">
				
				  <div v-for="pet in pets" :key="pet.id" class="media">
					<div class="media-left">
					  <img :src="require(`../../public/img/${pet.pet_image}`)" alt="" class="img-fluid">
					</div>
					<div class="media-body">
					  <h3 class="mb-30">&nbsp;I am {{pet.pet_name}}!</h3>
					  <h4 class="media-heading">&nbsp;{{pet.pet_description}}</h4>
					  <br><p>I was adopted "{{pet.created_at}}"</p>
					</div>
				  </div>
				  
				  <br>
			
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
	name: 'dishes',
    components: {
		Footer,
        Header
	},
	data() {
		return {
			pets:[],
		}
	},
	mounted() {

	},
	methods: {      
		async fetchPets() {
            var user_id = this.$store.getters['user/getUser'].id;
            console.log(user_id)
            await this.$store.dispatch('adoptions/getMyadoptionsFromDB',user_id)
            
            this.pets = this.$store.getters['adoptions/getadoptions'];
            console.log(this.pets)
        },
	},
	created(){
        this.fetchPets();
    },
    computed: {
		
    },
}
</script>

<style scoped>
</style>