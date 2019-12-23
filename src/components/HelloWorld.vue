<template>
  <v-container>
    <v-app id="inspire">
      <v-text><h2>Bank Search Table</h2></v-text>
    <v-card>
      <v-card-title>
   <v-toolbar-title>
     <v-select v-model="enabled" :items="slots" label="Cities" clearable></v-select> 
   </v-toolbar-title>
        <v-spacer></v-spacer>
    
        <v-text-field
          v-model="search"
         
          label="Search"
          single-line
          hide-details
        ></v-text-field>
      </v-card-title>
    
      <v-data-table

        :headers="headers"
        :items="bank"
        :search="search"

      >
     
      </v-data-table>
      
    
    </v-card>
   





  </v-app>

    <v-footer
      dark
      padless
    >
      <v-card
        class="flex"
        flat
        tile
      >
      
  
        <v-card-text class="py-2 white--text text-center">
          {{ new Date().getFullYear() }} — <strong>  <a href="https://www.linkedin.com/in/shahbaz-zaidi-87b4bb144/">Shahbaz</a> </strong>
        </v-card-text>
      </v-card>
    </v-footer>
  </v-container>
  
</template>





<script>
import axios from 'axios';

export default {
  data() {
    return {
       search: '',
       text:'',
       bank:'',
       rate:2,
       loading: false,
       slots: ['Kolkata','Delhi','Mumbai'],
      headers: [
        
        { text: 'IFSC',align:'center', value: 'ifsc' },
         { text: 'BANK ID', align:'center',value: 'bank_id' },
          { text: 'BRANCH', align:'center',value: 'branch' },
           { text: 'ADDRESS',align:'center', value: 'address' },
            { text: 'CITY',align:'center', value: 'city' },
             { text: 'DISTRICT', align:'center',value: 'district' },
              { text: 'STATE',align:'center', value: 'state' },
               { text: 'BANK NAME',align:'center', value: 'bank_name' },
               
              
               
      
      ],
       icons: [
      'fab fa-facebook',
      'fab fa-twitter',
      'fab fa-google-plus',
      'fab fa-linkedin',
      'fab fa-instagram',
    ],
    }
  },


 created(){

   
    axios.get(`https://vast-shore-74260.herokuapp.com/banks?city=MUMBAI `)
    .then(response => {
     
      this.bank = response.data
    })
    .catch(e => {
      this.errors.push(e)
    })
    this.loading = false;
 
  },
    
}
</script>
