<template>
  <Page>
    <ActionBar title="Detail of the news">
      <NavigationButton
        text="Go Back"
        android.systemIcon="ic_menu_back"
        @tap="$navigateBack"
      />
    </ActionBar>

    <ScrollView scroll="onScroll">
      <StackLayout  class="p-20">
         <Label textWrap="true"  fontWeight="bold" class="h1" :text="w.title.rendered"></Label>
        <Label textWrap="true" class="h2" text="Description"   ></Label>
        <Label  class="hr" ></Label>
<HtmlView textWrap="true" :html="w.content.rendered" />
     <!--  <Label textWrap="true" :text="w.content.rendered"></Label> -->
     
      </StackLayout>
    </ScrollView>
  </Page>
</template>
<script>
export default {
  props: ["w"],
  data() {
    return {
      words: {}
    };
  },
  mounted() {
   /*  this.w.content.rendered = this.w.content.rendered.replace(
      /(<([^>]+)>)|&#|;/gi,
      " "
    ); */

     this.w.title.rendered = this.w.title.rendered.replace(
      /(<([^>]+)>)|&#|;/gi,
      " "
    );
    //Çeviri için kullanılacaktır. Kelimeler sayılarına göre sözlük yapısına alınmıştır.
    var liste = this.w.content.rendered.trim().split(/\s+/);
    var count = this.w.content.rendered.trim().split(/\s+/).length;
    for (let index = 0; index < liste.length; index++) {
      if (this.words[liste[index]]) {
        this.words[liste[index]] += 1;
      } else {
        this.words[liste[index]] = 1;
      }
    }

    
   /*  var keys = Object.keys(this.words);
    var i,
      len = keys.length;
    var sortedDict = [];
    for (let index = 0; index < len; index++) {
      var k = keys[index];
      sortedDict.push({ key: k, value: this.words[k] });
    } */
  }
};
</script>
