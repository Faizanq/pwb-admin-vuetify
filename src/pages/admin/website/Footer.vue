<template>
  <v-container>
    <v-slide-y-transition mode="out-in">
      <v-container grid-list-md>
        <v-flex d-flex xs12>
          <v-card color="black" dark>
            <div style="display: inline=block; float: right;" v-show="WebsiteSettings.hasChanges">
              You have unsaved changes
              <v-btn color="success">Save Changes</v-btn>
            </div>
            <v-card-title primary class="title">Website Footer</v-card-title>
          </v-card>
        </v-flex>
        <v-card contain>
          <v-flex xs12>
            <v-card-title>
              <h2>Social Links</h2>
            </v-card-title>
          </v-flex>
          <v-layout row wrap>

            <v-flex xs1 style="text-align: center;">
              <i class="fab fa-facebook-square fa-3x"></i>
            </v-flex>
            <v-flex xs10>
              <v-text-field label="Facebook" v-model="WebsiteSettings.social_media.facebook" v-on:change="DataChanged();"></v-text-field>
            </v-flex>
            <v-flex xs1></v-flex>

            <v-flex xs1 style="text-align: center;">
              <i class="fab fa-linkedin fa-3x"></i>
            </v-flex>
            <v-flex xs10>
              <v-text-field label="LinkedIn" v-model="WebsiteSettings.social_media.linkedin" v-on:change="DataChanged();"></v-text-field>
            </v-flex>
            <v-flex xs1></v-flex>

            <v-flex xs1 style="text-align: center;">
              <i class="fab fa-twitter fa-3x"></i>
            </v-flex>
            <v-flex xs10>
              <v-text-field label="Twitter" v-model="WebsiteSettings.social_media.twitter" v-on:change="DataChanged();"></v-text-field>
            </v-flex>
            <v-flex xs1></v-flex>

            <v-flex xs1 style="text-align: center;">
              <i class="fab fa-youtube-square fa-3x"></i>
            </v-flex>
            <v-flex xs10>
              <v-text-field label="YouTube" v-model="WebsiteSettings.social_media.youtube" v-on:change="DataChanged();"></v-text-field>
            </v-flex>
            <v-flex xs1></v-flex>

            <v-flex xs1 style="text-align: center;">
              <i class="fab fa-google-plus-g fa-3x"></i>
            </v-flex>
            <v-flex xs10>
              <v-text-field label="Google+" v-model="WebsiteSettings.social_media.gplus" v-on:change="DataChanged();"></v-text-field>
            </v-flex>
            <v-flex xs1></v-flex>

            <v-flex xs1 style="text-align: center;">
              <i class="fab fa-instagram fa-3x"></i>
            </v-flex>
            <v-flex xs10>
              <v-text-field label="Instagram" v-model="WebsiteSettings.social_media.instagram" v-on:change="DataChanged();"></v-text-field>
            </v-flex>
            <v-flex xs1></v-flex>

            <v-flex xs1 style="text-align: center;">
              <i class="fab fa-pinterest-square fa-3x"></i>
            </v-flex>
            <v-flex xs10>
              <v-text-field label="Pintrest" v-model="WebsiteSettings.social_media.pinterest" v-on:change="DataChanged();"></v-text-field>
            </v-flex>
            <v-flex xs1></v-flex>

          </v-layout>
        </v-card>
      </v-container>
    </v-slide-y-transition>

    <pre>{{ WebsiteSettings }}</pre>
  </v-container>
</template>

<script>
import ApiAjax from "@/store/modules/apiAjax";

export default {
  data() {
    return {
      WebsiteSettings: {
        social_media: {
          facebook: "https://www.facebook.com/empty",
          linkedin: "https://www.linkedin.com/empty",
          twitter: "https://twitter.com/empty",
          youtube: "https://www.youtube.com/empty",
          gplus: "https://plus.google.com/empty",
          instagram: "https://www.instagram.com/empty",
          pinterest: "https://www.pinterest.com/empty"
        }
      }
    };
  },
  components: {},
  computed: {},
  mounted: function() {
    if (localStorage.WebSiteData.length > 10) {
      this.WebsiteSettings = JSON.parse(localStorage.WebSiteData); // RETURN PREVIOUSLY LOADED SETTINSS
    } else {
      ApiAjax.get("/api/v2/agency", data => {
        localStorage.SiteData = JSON.stringify(data);
        data.website.hasChanges = false; // create this setting on data load
        localStorage.WebSiteData = JSON.stringify(data.website);
      });
    }
  },
  methods: {
    DataChanged() {
      this.WebsiteSettings.hasChanges = true;
      localStorage.WebSiteData = JSON.stringify(this.WebsiteSettings);
      return true;
    }
  }
};
</script>