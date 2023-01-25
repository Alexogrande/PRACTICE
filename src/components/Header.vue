 <template>
			  <header id="header">
			    <div class="container main-menu">
			    	<div class="row align-items-center justify-content-between d-flex">
				      <div id="logo">
				        <router-link to="/"><img :src="'img/logo.png'" alt="" title="" /></router-link>
				      </div>
				      <nav id="nav-menu-container">
				        <ul class="nav-menu">
						  <li><router-link to="/pets">Pets</router-link></li>
						  						 
				          <li><router-link v-if="userIsEmptyComputed" to="/register">Register</router-link>
							  <router-link v-else to="/mypets">My pets</router-link>
						  </li>
				          <li><router-link v-if="userIsEmptyComputed" to="/login">Login</router-link>
							  <router-link @click.native="logout" v-else to="">Logout</router-link>
						  </li>
				          <li><a v-if="!userIsEmptyComputed" href="#">Welcome {{userName}}</a></li>						  
				        </ul>
				      </nav><!-- #nav-menu-container -->		    		
			    	</div>
			    </div>
			  </header><!-- #header -->
</template>

<script>


export default {
    methods: {

		logout() {
            this.$store.commit('user/logoutUser')
            localStorage.setItem('message', 'Bye, see you back soon!');
            this.$router.push('/message')
        },
    },
    computed: {
		userIsEmptyComputed: function() {
            let obj = this.$store.getters['user/getUser']
            return Object.keys(obj).length === 0;
            
        },
		userName: function() {
            return this.$store.getters['user/getUser'].name
        }
    },

}


</script>  
