<template>
  <base-container>
    <h2>Active Users</h2>
    <base-search @search="updateSearch" :search-term="search.enteredSearchTerm"></base-search>
    <div>
      <button @click="sort('asc')" :class="{selected: sortTerms.sorting === 'asc'}">Sort Ascending</button>
      <button @click="sort('desc')" :class="{selected: sortTerms.sorting === 'desc'}">Sort Descending</button>
    </div>
    <ul>
      <user-item
          v-for="user in displayedUsers"
          :key="user.id"
          :user-name="user.fullName"
          :id="user.id"
          @list-projects="$emit('list-projects', $event)"
      ></user-item>
    </ul>
  </base-container>
</template>

<script>
import { reactive, computed, watch} from 'vue';
import UserItem from './UserItem.vue';

export default {
  components: {
    UserItem
  },
  props: ['users'],
  emits: ['list-projects'],
  setup(props) {
    const search = reactive({
      enteredSearchTerm: '',
      activeSearchTerm: ''
    });

    const sortTerms = reactive({
      sorting: null
    });

    const availableUsers = computed(() => {
      let users = [];
      if (search.activeSearchTerm) {
        users = props.users.filter((usr) =>
            usr.fullName.includes(search.activeSearchTerm)
        );
      } else if (props.users) {
        users = props.users;
      }
      return users;

    });

    const displayedUsers = computed(() => {
      if (!sortTerms.sorting) {
        return availableUsers.value;
      }
      return availableUsers.value.slice().sort((u1, u2) => {
        if (sortTerms.sorting === 'asc' && u1.fullName > u2.fullName) {
          return 1;
        } else if (sortTerms.sorting === 'asc') {
          return -1;
        } else if (sortTerms.sorting === 'desc' && u1.fullName > u2.fullName) {
          return -1;
        } else {
          return 1;
        }
      });
    });

    function updateSearch(val) {
      search.enteredSearchTerm = val;
      search.activeSearchTerm = val;
    }

    function sort(mode) {
      sortTerms.sorting = mode;
    }

    return {
      displayedUsers,
      updateSearch,
      sort,
      search,
      sortTerms
    };
  }
}

</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
</style>