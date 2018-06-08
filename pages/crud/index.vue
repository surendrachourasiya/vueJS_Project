<template>
    <section id=""><br/>
      <!-- <div v-if="loading">
        <img src="~/assets/loader.gif"/>
          Loading.....
      </div>    -->
      <!-- <Alert v-if="alert" v-bind:message="alert" /> -->
    <!-- User Interface controls -->
    <b-row>
      <b-col md="5" class="my-1">
        <b-form-group horizontal label="Filter" class="mb-0">
          <b-input-group>
            <b-form-input v-model="filter" placeholder="Type to Search" />
            <b-input-group-append>
              <b-btn :disabled="!filter" @click="filter = ''">Clear</b-btn>
            </b-input-group-append>
          </b-input-group>
        </b-form-group>
      </b-col>
      <b-col md="3" class="my-1">
        <b-form-group horizontal label="Sort" class="mb-0">
          <b-input-group>
            <b-form-select v-model="sortBy" :options="sortOptions">
              <option slot="first" :value="null">-- none --</option>
            </b-form-select>
            <b-form-select :disabled="!sortBy" v-model="sortDesc" slot="append">
              <option :value="false">Asc</option>
              <option :value="true">Desc</option>
            </b-form-select>
          </b-input-group>
        </b-form-group>
      </b-col>
      <!-- <b-col md="6" class="my-1">
        <b-form-group horizontal label="Sort direction" class="mb-0">
          <b-input-group>
            <b-form-select v-model="sortDirection" slot="append">
              <option value="asc">Asc</option>
              <option value="desc">Desc</option>
              <option value="last">Last</option>
            </b-form-select>
          </b-input-group>
        </b-form-group>
      </b-col> -->
      <b-col md="4" class="my-1">
        <b-form-group horizontal label="Per page" class="mb-5">
          <b-form-select :options="pageOptions" v-model="perPage" />
        </b-form-group>
      </b-col>
    </b-row>

    <!-- Main table element -->
    <b-table show-empty
             stacked="md"
             :items="getData"
             :fields="fields"
             :current-page="currentPage"
             :per-page="perPage"
             :filter="filter"
             :sort-by.sync="sortBy"
             :sort-desc.sync="sortDesc"
             :sort-direction="sortDirection"
             @filtered="onFiltered"
    >
      <!-- <template slot="name" slot-scope="row">{{row.value.name}}</template>
      <template slot="email" slot-scope="row">{{row.value.email}}</template> -->
      <template slot="actions" slot-scope="row">
        <!-- We use @click.stop here to prevent a 'row-clicked' event from also happening -->
        <b-button size="sm" @click.stop="info(row.item, row.index, $event.target)" class="mr-1">
          Info modal
        </b-button>
        <b-button size="sm" @click.stop="row.toggleDetails">
          {{ row.detailsShowing ? 'Hide' : 'Show' }} Details
        </b-button>&nbsp;
        <b-button size="sm" v-on:click="deleteUser(row.item.id)">
          Delete
        </b-button>
      </template>
      <template slot="row-details" slot-scope="row">
        <b-card>
          <ul>
            <li v-for="(value, key) in row.item" :key="key">{{ key }}: {{ value}}</li>
          </ul>
        </b-card>
      </template>
    </b-table>

    <!-- <b-row>
      <b-col md="6" class="my-1">
        <b-pagination :total-rows="totalRows" :per-page="perPage" v-model="currentPage" class="my-0" />
      </b-col>
    </b-row> -->

    <!-- Info modal -->
    <b-modal id="modalInfo" @hide="resetModal" :title="modalInfo.title"  ok-only>
      <pre>{{ modalInfo.content }}</pre>
    </b-modal>
     
      <!-- <b-table striped hover :items="getData" :fields="fields">
        <template slot="detail" slot-scope="row">
           <nuxt-link v-bind:to="'/edit/_postId/'+ row.item.id" class="btn btn-default">Edit</nuxt-link>
         
          <b-button size="sm" class="mr-2" v-on:click="deleteUser(row.item.id)">
           Delete
          </b-button>
        </template>
        <template slot="row-details" slot-scope="row">
          <b-card>
            <b-row class="mb-2">
              <b-col sm="3" class="text-sm-right"><b>name:</b></b-col>
              <b-col>{{ row.item.name }}</b-col>
            </b-row>
            <b-row class="mb-2">
              <b-col sm="3" class="text-sm-right"><b>Email:</b></b-col>
              <b-col>{{ row.item.email }}</b-col>
            </b-row>
            <b-button size="sm" @click="row.toggleDetails">Hide Details</b-button>
          </b-card>
        </template>
      </b-table> -->
    </section>
</template>

<script>
import axios from 'axios';
import Alert from '~/components/Alert';
export default {
  data () {
    return {
      
      getData: [],
      fields: [
        { key: 'name', label: 'User name', sortable: true, sortDirection: 'desc' },
        { key: 'email', label: 'User email', sortable: true, 'class': 'text-center' },
        { key: 'actions', label: 'Actions' }
      ],
      currentPage: 1,
      perPage: 5,
      // totalRows: getData.length,
      pageOptions: [ 5, 10, 15 ],
      sortBy: null,
      sortDesc: false,
      sortDirection: 'asc',
      filter: null,
      modalInfo: { title: '', content: '' }
    }
  },

  computed: {
    sortOptions () {
      // Create an options list from our fields
      return this.fields
        .filter(f => f.sortable)
        .map(f => { return { text: f.label, value: f.key } })
    }
  },

   methods: {
    info (item, index, button) {
      this.modalInfo.title = `Row index: ${index}`
      this.modalInfo.content = JSON.stringify(item, null, 2)
      this.$root.$emit('bv::show::modal', 'modalInfo', button)
    },
    resetModal () {
      this.modalInfo.title = ''
      this.modalInfo.content = ''
    },
    onFiltered (filteredItems) {
      // Trigger pagination to update the number of buttons/pages due to filtering
      // this.totalRows = filteredItems.length
      this.currentPage = 1
    },

    getUser() {
      axios.get(`http://localhost/api/getUsers.php`)
    .then(response => { 
      // this.loading= false   
      this.getData = response.data;
     // alert(JSON.stringify(this.getData));
      // console.log(this.getData);
      
    })
    .catch(e => {
      // this.loading= false
      this.errors.push(e)
    })
    },

    filterBy(list, value) {
      return list.filter(function(user) {
        return user.name.indexOf(value) > -1;
      })
    },

    deleteUser(id) {
      console.log(id);
      axios.post(`http://localhost/api/delete.php?id=`+id)
      .then(response => {}, this.$router.push('/crud') )
      .catch(e => {
        this.errors.push(e)
      })
    }
   },

  // Fetches posts when the component is created.
  created() {
    // if(this.$route.query.alert) {
    //   this.alert = this.$route.query.alert
    // }
    this.getUser();
  },
  updated() {
    this.getUser();
  },

  components: {
    Alert
  }
}
</script>