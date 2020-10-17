<template>
  <Page>
    <ActionBar>
      <Label text="Wired App" />
    </ActionBar>

    <GridLayout>
      <ListView @itemTap="goToDetail"  for="w in wired" class="list-group">
        <v-template>
          <FlexBoxLayout flexDirection="row" class="list-group-item">
              <Image stretch="aspectFit" src="~/images/backgroundimage.jpg"  class=" fas thumb img-circle" ></Image>
             <Label  fontWeight="bold"  textWrap="true" width="250" :text="w.title.rendered" />
            
          </FlexBoxLayout>
        </v-template>
      </ListView>
    </GridLayout>
  </Page>
</template>

<script>

import axios from "axios";
import Detail from "./Detail"
export default {
  data() {
    return {
      wired: [],
    };
  },
  methods: {
    goToDetail(event) {
       
        this.$navigateTo(Detail,{props:{w:event.item}});
    }
  },
  mounted() {
    axios({
      method: "GET",
      url: "https://www.wired.com/wp-json/wp/v2/posts/?categories=3"
    }).then(
      result => {
        for (const key in result.data) {
          if (key < 5) {
            this.wired.push(result.data[key]);
          } else {
            break;
          }
        }
      },
      error => {
        console.error(error);
      }
    );
  }
};
</script>

<style scoped lang="scss">
@import "~@nativescript/theme/scss/variables/blue";

</style>
