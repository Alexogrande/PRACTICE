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
								Register			
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
						<form @submit.prevent="register" class="col-lg-9">
						  <div class="form-group">
						    <label for="first-name">Name</label>
						    <input  v-model="user.name" type="text" class="form-control" placeholder="Name" required autofocus>
						  </div>
						   <div class="form-group">
								<label for="email">Email Address</label>
						   		<input  v-model="user.email" type="email" class="form-control" placeholder="Valid email Address" required>
							</div>	
						  
						  <div class="form-row"> 							  	
						  	<div class="col-6 mb-30">
						  		<label for="password1">Password</label>
						   		<input  v-model="user.password" type="password" class="form-control" placeholder="Password" required>
						  	</div>
						  	<div class="col-6 mb-30">
						  		<label for="password2">Confirm Password</label>
						   		<input  v-model="passwordConfirm" type="password" class="form-control" placeholder="Repeat Password" required>						  		
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
    name: 'register',
    components: {
        Footer,
        Header
    },

    data() {
        return {
            user:{
                name: '',
                email: '',
                password: '',
            },
            
            passwordConfirm: '',        
        }
    },

    mounted() {
    },
    methods: {    
        validateForm() {
			var validRegex = /^[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$/;

			console.log(this.user.password + " " + this.passwordConfirm);

			if (!this.user.email.match(validRegex)) {
				alert('Invalid email format!!');
				this.email='';
				return false;
			}
			else if (this.user.password !== this.passwordConfirm) {
				alert('Passwords dont match!!');
				this.passwordConfirm = '';
				return false;
			}
			else if (this.user.password.length < 6) {
				
				alert('Passwords must be at least 6 characters long!!');
				this.user.password = '';
                this.passwordConfirm = '';
				return false;
			}
			return true;
		},

        async register() {
			if (!this.validateForm()) {
				return;
			}
			const exists = await this.$store.dispatch('user/userExists', this.user);
			if (exists) {
				console.log("existe na BD");
			}
			else { //add user to database
				const addedUser = await this.$store.dispatch('user/addUser');
                localStorage.setItem('message', 'Welcome! You can now login');
				this.$router.push({ path: '/message' });
			}
		},
    },
    computed: {
               
    },

}
</script>