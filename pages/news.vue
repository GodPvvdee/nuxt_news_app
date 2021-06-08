<template>
  <div>
    <v-container>
      <v-flex xs12>
        <h2>мэдээ</h2>
      </v-flex>
      <v-flex>
        <v-layout row>
          <!-- xs6
            sm6
            offset-sm3
            v-for="(article, index) in acticles"
            :key="index" -->
          <v-flex xs6 v-for="(article, index) in articles" :key="index">
            <!-- мэдээ -->
            <br />
            <v-card class="mx-auto" max-width="400">
              <img :src="article.urlToImage" width="100%" height="200px" />
              гарчиг
              <v-card-title>{{ article.title }}</v-card-title>

              контент
              <v-card-title>{{ article.content }}</v-card-title>

              <!-- <v-card-title>Дэлхийн топ 10 дурсгалт газар</v-card-title> -->
              <!-- <div>{{ article.author }}</div> -->
              <v-card-subtitle class="pb-0"> </v-card-subtitle>

              <v-card-text class="text--primary"> </v-card-text>
              <!-- үнэлгээ өгөх -->

              <v-card class="elevation-16 mx-auto" height="140" width="280">
                <v-card-title class="text-h5"> </v-card-title>

                Таньд энэ мэдээ хэр таалагдсан бэ?
                <div class="text-center mt-6">
                  <v-rating
                    v-model="rating"
                    color="yellow darken-3"
                    background-color="grey darken-1"
                    empty-icon="$ratingFull"
                    half-increments
                    hover
                  ></v-rating>
                </div>

                <v-divider></v-divider>
                <v-card-actions class="justify-space-between"> </v-card-actions>
              </v-card>
              <br />
              <v-card-actions>
                <v-btn :href="baseUrl" color="orange" text>
                  Хуваалцах
                </v-btn>

                <v-btn :href="article.url" target="_blank" color="orange" text>
                  харах
                </v-btn>
              </v-card-actions>
            </v-card>
          </v-flex>
        </v-layout>
      </v-flex>
    </v-container>
  </div>
</template>

<script>
import axios from "axios";
// import VueShareSocial from "vue-share-social";

// Vue.use(VueShareSocial);
// import { ShareFacebook } from "vue-share-social";
export default {
  //   components: {
  //     ShareFacebook
  //   },
  data() {
    return {
      baseUrl:
        "https://www.facebook.com/sharer/sharer.php?u=https%3A%2F%2Fdevelopers.facebook.com%2Fdocs%2Fplugins%2F&amp;src=sdkpreparse",
      articles: {}
    };
  },
  data2: () => ({
    rating: 4
  }),
  async created() {
    const config = {
      headers: {
        Accept: "application/json"
      }
    };
    try {
      const res = await axios.get(
        "https://newsapi.org/v2/everything?q=tesla&from=2021-05-08&sortBy=publishedAt&apiKey=48dd56ab7e744d33863fedd0d7ce481e",
        config
      );
      this.articles = res.data.articles;
      console.log(res.data);
    } catch (err) {
      console.log(err);
    }
  }
};
</script>

<style></style>
