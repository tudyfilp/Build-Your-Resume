<template>
  <div class="container wrapper">
    <h2>
      <b>Education</b>
    </h2>
    <!-- education items -->
    <div class="mt-3">
      <div v-for="(education, index) in getEducation" :key="index" class="item_wrapper col-md-12">
        <div class="row item_expand" @click="toggleExpand(education)">
          <h5 class="col-md-10 col-sm-9 col-9">{{education.institute}} - {{education.degree}}</h5>
          <i
            class="fas fa-trash delete_icon col-md-1 col-sm-1 col-1 mt-3 px-2"
            @click="deleteEducation(education);"
          ></i>
          <i class="fas fa-chevron-down expand_icon col-md-1 col-sm-1 col-1 mt-3"></i>
        </div>
        <shared-custom-item
          class="expandable"
          :class="{active : education.expanded}"
          :model="education"
          :attr1="'institute'"
          :attr2="'degree'"
          :label1="'Institute'"
          :label2="'Degree'"
        ></shared-custom-item>
      </div>
    </div>

    <div
      class="add_button"
      @click="
      $store.commit('hide', getEducation);
      $store.commit('addEducation');
    "
    >
      <h5>
        <i class="fas fa-plus mt-3"></i> Add education
      </h5>
    </div>
  </div>
</template>
<script>
import { mapGetters } from "vuex";
import SharedCustomItem from "../../assets/SharedCustomItem.vue";
export default {
  computed: {
    ...mapGetters(["getEducation"])
  },
  components: {
    SharedCustomItem
  },
  methods: {
    toggleExpand(education) {
      if (education.expanded == true) {
        education.expanded = false;
      } else {
        this.$store.commit("hide", this.getEducation);
        education.expanded = true;
      }
    },
    deleteEducation(education) {
      this.$store.commit("deleteEducation", education);
    }
  }
};
</script>
<style scoped>
</style>


