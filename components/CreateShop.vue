<template>
  <div v-loading="loading" class="shop-details-form-container">
    <el-alert v-if="published" title="Shop is not published yet!" type="warning">
      <p>You can add your shop details and publish it!</p>
    </el-alert>

    <el-form ref="form" :model="form" class="form-container">
      <p>You can add your shop details and publish it to the tangle!</p>

      <div class="shop-details-form-main-container">
        <el-row>
          <el-col :span="24">
            <br />
            <br />
            <el-form-item label="Kategorie">
              <el-select v-model="form.category" placeholder="Bitte wähle eine Kategorie aus">
                <el-option label="Einzelhandel " value="shop"></el-option>
                <el-option label="Apotheke" value="pharmacy"></el-option>
              </el-select>
            </el-form-item>

            <el-form-item label="Shop Name:">
              <el-input
                v-model="form.name"
                :rows="1"
                type="text"
                class="shop-name-input"
                autosize
                placeholder="Your shop name"
              />
            </el-form-item>

            <el-form-item label="Description:">
              <el-input
                v-model="form.description"
                rows="5"
                type="textarea"
                class="shop-description-input"
                autosize
                placeholder="Your shop description"
              />
            </el-form-item>

            <el-form-item label="Location">
              <LocationChooseMap @update="updateIac" />
            </el-form-item>
          </el-col>
        </el-row>
      </div>
      <el-button @click="onCancel" type="warning">Cancel</el-button>
      <el-button style="margin-left: 10px;" type="primary" @click="onSubmit">Create</el-button>
    </el-form>
  </div>
</template>

<script>
import LocationChooseMap from "./shop/LocationChooseMap";
export default {
  name: "CreateShop",
  components: { LocationChooseMap },
  props: {
    published: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      loading: false,
      shop: {},
      form: {
        name: ""
      }
    };
  },
  created() {
    // fetch shop from database
    // let shop_string = localStorage.getItem("shop") || "{}";
    // this.shop = JSON.parse({shop_string});
  },
  methods: {
    onSubmit: async function() {
      // save it to tangle!
      console.log("onSubmit", this.form);
      console.log("this.iac)", this.form.iac);
    },
    onCancel() {
      this.$router.push("/");
    },
    updateIac(newIac) {
      this.form.iac = newIac;
    }
  }
};
</script>

<style lang="scss">
.shop-details-form-container {
  max-width: 480px;
}
</style>