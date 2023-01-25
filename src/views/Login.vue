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
								Login			
							</h1>	
						</div>	
					</div>
				</div>
			</section>
			<!-- End banner Area -->	
				
			<!-- Start Volunteer-form Area -->
			<section class="Volunteer-form-area section-gap">
				<div class="container">
					
					<div class="row justify-content-center">
						<form @submit.prevent="login" class="col-lg-9">
						  
						  <div class="form-row"> 							  	
						  	<div class="col-6 mb-30">
						  		<label for="email">Email</label>
						   		<input v-model="user.email" type="email" class="form-control" placeholder="Enter a valid email" required>
						  	</div>
						  	<div class="col-6 mb-30">
						  		<label for="password">Password</label>
						   		<input v-model="user.password" type="password" class="form-control" placeholder="Enter Password" required>						  		
						  	</div>
						  </div>		
						  
						  <button type="submit" class="primary-btn float-right">Submit</button>
						</form>
					</div>
				</div>	
			</section>
			<!-- End Volunteer-form Area -->

    
	



<Footer />

</div>
</template>
<script>
import Footer from '@/components/Footer.vue'
import Header from '@/components/Header.vue'



export default {
    name: 'login',
    components: {
        Footer,
        Header
    },
    data() {
        return {
            user:{
                email: '',
                password: '', 
            },
            alertMessageStyle: 'display:none;'      
        }
    },
    mounted() {
    },
    methods: {    
        async login() {
			console.log(this.user);

			const canLogin = await this.$store.dispatch('user/loginUser', this.user);
			if (canLogin) {
				
				console.log(this.$store.getters['user/getUser']);
                localStorage.setItem('message', "Welcome back " + this.$store.getters['user/getUser'].name + "!");
				this.$router.push({ path: '/message' });
			}
            else{
                // alert('Login failed: wrong email or password!');
				this.user.email='';
				this.user.password='';
            }
		},
    },
    computed: {
                       
    },
}
</script>