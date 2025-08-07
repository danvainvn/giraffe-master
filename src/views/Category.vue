<template>
  <div>
    <v-row>
      <v-col cols="12" lg="12" xl="8">
        <div>
          <div>
            <div>
              <h2 class="text-h4 font-weight-bold">ANIMAL</h2>

              <h4 class="text-h6">Some category description goes here</h4>
            </div>

            <v-divider class="my-4"></v-divider>

            <v-row>
              <v-col cols="12" md="6" lg="4" v-for="post in posts" :key="post.id">
                <v-hover v-slot:default="{ hover }" open-delay="50" close-delay="50">
                  <div>
                    <v-card flat :color="hover ? 'white' : 'transparent'" :elevation="hover ? 12 : 0" hover to="/detail">
                      <v-img
                        :src="post.image || 'https://cdn.pixabay.com/photo/2016/11/14/04/45/elephant-1822636_1280.jpg'"
                        :aspect-ratio="16 / 9"
                        gradient="to top, rgba(25,32,72,.4), rgba(25,32,72,.0)"
                        height="200px"
                        class="elevation-2"
                        style="border-radius: 16px"
                      >
                        <v-card-text>
                          <v-btn color="accent">{{ post.category || 'Posts' }}</v-btn>
                        </v-card-text>
                      </v-img>

                      <v-card-text>
                        <div class="text-h5 font-weight-bold primary--text">
                          {{ post.title }}
                        </div>

                        <div class="text-body-1 py-4">
                          {{ post.author }}
                        </div>

                        <div class="d-flex align-center">
                          <v-avatar color="accent" size="36">
                            <v-icon dark>mdi-feather</v-icon>
                          </v-avatar>
                          <div class="pl-2">{{ post.date || '' }}</div>
                        </div>
                      </v-card-text>
                    </v-card>
                  </div>
                </v-hover>
              </v-col>
            </v-row>
          </div>
        </div>
      </v-col>

      <v-col>
        <div>
          <siderbar />
        </div>
      </v-col>
    </v-row>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: "Category",
  components: {
    siderbar: () => import("@/components/details/sidebar"),
  },
  data() {
    return {
      posts: []
    };
  },
  mounted() {
    this.fetchPosts();
  },
  methods: {
    async fetchPosts() {
      try {
        const response = await axios.get('http://localhost:3001/posts');
        this.posts = response.data;
        this.posts.forEach(post => {
          console.log(`Title: ${post.title}, Author: ${post.author}`);
        });
      } catch (error) {
        console.error('Lỗi khi lấy dữ liệu:', error);
      }
    }
  }
};
</script>
