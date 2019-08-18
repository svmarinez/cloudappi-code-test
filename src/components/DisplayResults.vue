<template>
   <div id="display-results" v-if="filteredUsers" class="table-container">
      <table class="table is-striped is-hoverable">
         <thead>
            <tr>
               <th>
                  Name
               </th>
               <th>
                  Email Address
               </th>
            </tr>
         </thead>
         <tbody>
            <tr v-for:"user in filteredUsers" v-bind:key="filteredUsers">
               <td>{{ user.name }}</td>
               <td>{{ user.email }}</td>
            </tr>
         </tbody>
      </table>
    </div>
    <!--<div v-else class="is-warning">
      <p>{{ errorMessage }}</p>
   </div>-->
</template>

<script>
export default {
   name: "display-results",
   props: ["filteredUsers"],
   data() {
      return {
         errorMessage: 'User not found, please try again.',
         }
   }
}
</script>

<style>

</style>