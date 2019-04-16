<template>
  <div class="single-vehicle">
  	<div v-if="loaded">
	   	<h3>Vehicle details</h3>
	   	<div class="card">
	      <div class="card-header">
	        header
	      </div>
	      <div class="card-body">
	      	<p >ID: {{vehicleId}}</p>
	        <p >Vehicle Name: {{vehicleName}}</p>
	        <p >Vehicle Type: {{vehicleType}}</p>
	        <p >Vehicle Date: {{vehicleTimestamp}}</p>
	        <p >Connection: {{vehicleConn}}</p>
	        <button class="btn btn-success"> Buy Now</button>
	        <router-link :to="'/'" class="btn btn-primary"> Back </router-link>
	      </div>
		</div>
    </div>
    <div v-else> 
    	<h3>Loading...</h3>
    </div>
  </div>
</template>

<script>
import db from '@/db';
import axios from 'axios';

export default {
  name: 'VehiclePage',
  data () {
    return {
    	vehicleId:'',
    	vehicleName: '',
    	vehicleType: '',
    	vehicleTimestamp: '',
    	vehicleConn: '',
    	loaded: false
    }
  },
  beforeCreate (){
axios.get('http://localhost:3000/vehicles/' + this.$route.params.id)
        .then(response => {
					this.vehicleId = this.$route.params.id;
	        this.vehicleName = response.data.name;
	        this.vehicleType = response.data.type;
	        this.vehicleTimestamp = response.data.timestamp;
	        this.vehicleConn = response.data.last_successful_connection;
	        this.loaded = true;
        });

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3{
  text-align: center;
  margin-top: 30px;
  margin-bottom: 20px;
}

</style>
