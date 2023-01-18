<script>
import Butter from "buttercms";

class Post {
  constructor(title, link, author, img) {
    this.title = title;
    this.link = link;
    this.author = author;
    this.img = img;
  }
}

export default {
  data() {
    return {
      search: "",
      fruits: [],
      body: [],
      postList: [
        new Post(
          "Vue.js",
          "https://vuejs.org/",
          "Chris",
          "https://vuejs.org//images/logo.png"
        ),
        new Post(
          "React.js",
          "https://facebook.github.io/react/",
          "Tim",
          "https://daynin.github.io/clojurescript-presentation/img/react-logo.png"
        ),
        new Post(
          "Angular.js",
          "https://angularjs.org/",
          "Sam",
          "https://angularjs.org/img/ng-logo.png"
        ),
        new Post(
          "Ember.js",
          "http://emberjs.com/",
          "Rachel",
          "http://www.gravatar.com/avatar/0cf15665a9146ba852bf042b0652780a?s=200"
        ),
        new Post(
          "Meteor.js",
          "https://www.meteor.com/",
          "Chris",
          "http://hacktivist.in/introduction-to-nodejs-mongodb-meteor/img/meteor.png"
        ),
        new Post(
          "Aurelia",
          "http://aurelia.io/",
          "Tim",
          "https://cdn.auth0.com/blog/aurelia-logo.png"
        ),
        new Post(
          "Node.js",
          "https://nodejs.org/en/",
          "A. A. Ron",
          "https://code-maven.com/img/node.png"
        ),
        new Post(
          "Pusher",
          "https://pusher.com/",
          "Alex",
          "https://avatars1.githubusercontent.com/u/739550?v=3&s=400"
        ),
        new Post(
          "Feathers.js",
          "http://feathersjs.com/",
          "Chuck",
          "https://cdn.worldvectorlogo.com/logos/feathersjs.svg"
        ),
      ],
    };
  },

  mounted() {
    console.log("comine");
    const butter = Butter("f957583e47b4abfd32e8921ff0987b6dbb0ce389");

    butter.page
      .retrieve("*", "how-to")
      .then((response) => {
        console.log(response);
        ({ body: this.body } = response.data.data.fields);

        console.log(this.body, "this", typeof this.body);
      })
      .catch(function (resp) {
        console.log(resp);
      });
  },

  computed: {
    filteredList() {
      return this.body.filter((post) => {
        return post.question.toLowerCase().includes(this.search.toLowerCase());
      });
    },

    // filteredList() {
    //   // const fruits = ["apple", "banana", "orange"];
    //   return this.fruits.filter((fruit) => {
    //     return fruit.toLowerCase().includes(this.input.toLowerCase());
    //   });
    // },
    // filteredPeople() {
    //   if (this.people) {
    //     return this.people.filter((person) => {
    //        return person.name.match(this.search);
    //     });
    //   }
    //   return false;
    // }
  },

  // import { ref, onMounted } from "vue";
  // import { $ref } from "vue/macros";

  // let input = ref("");
  // let arr = ref([]);

  // onMounted(() => {
  //   const butter = Butter(import.meta.env.VITE_BUTTER_API_KEY);

  //   butter.page
  //     .retrieve("*", "how-to")
  //     .then((response) => {
  //       console.log(response);
  //       // ({ body } = response.data.data);
  //       arr.value = response.data.data.fields.body;
  //       console.log(arr.value, typeof(arr.value));
  //     })
  //     .catch(function (resp) {
  //       console.log(resp);
  //     });
  // });

  //   // butter.page
  //   //   .retrieve("*", "home")
  //   //   .then((resp) => {
  //   //     ({
  //   //       image: this.image,
  //   //       title: this.title,
  //   //       description: this.description,
  //   //     } = resp.data.data.fields.header_component);
  //   //   })
  // .catch(function (resp) {
  //   console.log(resp);
  // });
  // butter.page
  //   .retrieve("*", "how-to")
  //   .then((response) => console.log(response));
};
</script>

<template>
  <div id="app">
    <div class="search-wrapper">
      <input type="text" v-model="search" placeholder="Search title.." />
      <label>Search title:</label>
    </div>
    <div class="wrapper">
      <div class="card" v-for="post in filteredList">
        <div class="timeDiv">
          <span class="green">{{ post.answered_by }}</span>
          <span>{{ new Date("2022-12-26T14:30:00").getUTCDate() }}</span>
        </div>

        <h2>{{ post.question }}</h2>
        <p v-html="post.answer"></p>
      </div>
    </div>
  </div>
</template>

<style lang="scss">
html,
body {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  margin-top: 16px;
  margin-bottom: 16px;
}

div#app {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;

  .search-wrapper {
    position: relative;
    label {
      position: absolute;
      font-size: 12px;
      color: rgba(0, 0, 0, 0.5);
      top: 8px;
      left: 12px;
      z-index: -1;
      transition: 0.15s all ease-in-out;
    }
    input {
      padding: 4px 12px;
      color: rgba(0, 0, 0, 0.7);
      border: 1px solid rgba(0, 0, 0, 0.12);
      transition: 0.15s all ease-in-out;
      background: white;
      &:focus {
        outline: none;
        transform: scale(1.05);
        & + label {
          font-size: 10px;
          transform: translateY(-24px) translateX(-12px);
        }
      }
      &::-webkit-input-placeholder {
        font-size: 12px;
        color: rgba(0, 0, 0, 0.5);
        font-weight: 100;
      }
    }
  }

  .wrapper {
    display: flex;
    /* max-width: 854px; */
    flex-wrap: wrap;
    padding-top: 12px;
    text-align: start;
  }

  .card {
    // background-color: white;
    box-shadow: rgba(0, 0, 0, 0.117647) 0px 1px 6px,
      rgba(0, 0, 0, 0.117647) 0px 1px 4px;
    /* max-width: 124px; */
    margin: 12px;
    transition: 0.15s all ease-in-out;
    &:hover {
      transform: scale(1.1);
    }
    a {
      text-decoration: none;
      padding: 12px;
      color: #03a9f4;
      font-size: 24px;
      display: flex;
      flex-direction: column;
      align-items: center;
      img {
        height: 100px;
      }
      small {
        font-size: 10px;
        padding: 4px;
      }
    }
  }

  .timeDiv {
    display: flex;
    justify-content: space-between;
  }

  .hotpink {
    background: hotpink;
  }

  .green {
    padding: 0 5px;
    border-radius: 10px;
    background: green;
  }

  .box {
    width: 100px;
    height: 100px;
    border: 1px solid rgba(0, 0, 0, 0.12);
  }
}
</style>
