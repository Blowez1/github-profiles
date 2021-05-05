<template>
  <div>
    <h4 class="white">User Name :</h4>
    <input type="text" v-on:keyup.enter="refreshData()" v-model="userName" class="form-control bb--input mb-4" />

    <div class="bb-card mb-4">
      <div class="row">
        <div class="col-lg-3">
          <a target="_BLANK" :href="user.html_url"><img class="user__img" :src="user.avatar_url" :alt="user.login" /></a>
        </div>
        <div class="col-lg-9 mt-lg-0 mt-3">
          <div class="d-flex align-items-center mb-3">
              <span class="user__name h3 mr-3" style="margin-bottom : 0px"><a target="_BLANK" :href="user.html_url">{{user.login}}</a></span>
            <span class="user__location d-flex align-items-center">
                <svg class="mr-2" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" width="15" height="23.015" viewBox="0 0 16 23.015">
            <defs>
                <linearGradient id="linear-gradient" x1="-0.25" x2="0.5" y2="1" gradientUnits="objectBoundingBox">
                <stop offset="0" stop-color="#00bfb2"/>
                <stop offset="1" stop-color="#028090"/>
                </linearGradient>
            </defs>
            <path id="placeholder" d="M1.75,0a8.009,8.009,0,0,0-8,8c0,5.544,8.008,15.015,8.008,15.015S9.75,13.272,9.75,8A8.009,8.009,0,0,0,1.75,0ZM4.164,10.342a3.414,3.414,0,1,1,0-4.827A3.4,3.4,0,0,1,4.164,10.342Zm0,0" transform="translate(6.25)" fill="url(#linear-gradient)"/>
            </svg> {{user.location}}</span>
          </div>
          <p class="user__desc mb-3">
            {{user.bio}}
          </p>
          <ul class="user__stats mb-3">
            <li>{{user.followers}} <span>Followers</span></li>
            <li>{{user.following}} <span>Following</span></li>
            <li>{{user.public_repos}} <span>Repositories</span></li>
          </ul>

          <h6 class="mb-3">Repos :</h6>
          <div>
            <span v-for="repos in userRepos" :key="repos.id" class="repos__item"><a target="_BLANK" :href="repos.html_url">{{repos.full_name}}</a></span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
        user: null,
        userRepos : null,
        userName : "Blowez1"   
    }
  },
  methods: {
      getUser() {
          axios.get('https://api.github.com/users/' + this.userName )
          .then((response => (this.user = response.data)))
      },
      getUserRepos() {
          axios.get('https://api.github.com/users/'+ this.userName + '/repos')
          .then((response => (this.userRepos = response.data)))
      },
      refreshData(){
        this.getUser();
        this.getUserRepos();
      }
  },
  mounted : function () {
      this.refreshData()
      this.getToken()
  }
};
</script>

<style lang="scss">
h4 {
  font-weight: 600;
}

.white {
  color: #fff;
}

.bb--input {
  border-radius: 0;
  background-image: linear-gradient(315deg, #d7e1ec 0%, #ffffff 74%);
  background-color: #fff;
  border: none;
}
.bb-card {
  padding: 20px;
  box-shadow: 0 0 99px 0 rgba(0, 0, 0, 0.1);
  background-image: linear-gradient(315deg, #ffffff 0%, #d7e1ec 74%);
  background-color: #fff;
}

.user__name {
  font-weight: 600;
  color: #000;
  a {
    text-decoration: none;
    color: #000;
    &:hover {
      color: #000;
    }
  }
}

.user__img {
  width: 225px;
}

.user__stats {
  list-style-type: none;
  padding: 0;
  margin: 0;
  display: flex;

  li {
    margin-right: 20px;
    &:nth-last-child(1) {
      margin-right: 0px;
    }

    span {
      font-weight: 600;
    }
  }
}

.repos__item {
  background-color: #00bfb2;
  display: inline-block;
  margin-right: 0.5rem;
  margin-bottom: 0.5rem;
  padding: 0.25rem 0.5rem;
  background-image: linear-gradient(315deg, #00bfb2 0%, #028090 74%);
  color: #fff;
  a {
    text-decoration: none;
    color: #fff;
    &:hover {
      color: #fff;
    }
  }
}

</style>