<template>
  <div>
    <div class="control">
      <button
        class="button is-link is-light"
        @click.prevent="receiveList"
      >
        <router-link
          to="/list"
          exact
        >
          مشاهده افراد
        </router-link>
      </button>
    </div>
    <ul>
      <li
        v-for="item in userDetails"
        :key="item.index"
      >
        {{ item.username }}
        {{ item.nationalID }}
        {{ item.mobilePhone }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      userDetails: '',
    };
  },
  methods: {
    receiveList() {
      const receiveRequest = {
        method: 'GET',
        headers: { 'Content-Type': 'application/json' },
      };
      fetch('http://127.0.0.1:9000/user/list', receiveRequest)
        // eslint-disable-next-line consistent-return
        .then((response) => {
          if (response.status === 200) {
            return response.json();
          }
        })
        .then((data) => {
          this.userDetails = data;
        });
    },
  },
};
</script>
