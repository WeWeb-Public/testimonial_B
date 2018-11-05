
<!-- This is a Vue.js single file component. -->
<!-- Check the Vue.js doc here :  -->
<!-- https://vuejs.org/v2/guide/ -->

<!-- This is your HTML -->
<template>
  <div class="testimonial_B">
    <div class="content">
      <wwObject class="background" v-bind:ww-object="section.data.testimonialBg" v-bind:section="section" ww-category="background"></wwObject>

      <div class="content-title">
        <div v-bind:ww-object="section.data.contentTitle" v-bind:section="section" ww-cate="ww-text"></div>
      </div>
      <!-- bg == background -->
      <div class="left-section">
        <div v-bind:ww-object="section.data.leftSectionBg" v-bind:section="section" ww-category="background"></div>
        <wwObject tag="div" class="testmoniy-right-bg" v-bind:ww-object="section.data.leftTestimonyBg" v-bind:section="section" ww-category="background">
        </wwObject>
        <div class="testmony-right-bio" v-bind:ww-object="section.data.leftTestmonyBio" v-bind:section="section" ww-category="ww-text"></div>

      </div>
      <div class="right-section">
        <wwObject class="right-section-background" v-bind:ww-object="section.data.rightSectionBg" v-bind:section="section" ww-category="background">
        </wwObject>
        <div class="right-section-text">
          <wwObject class="right-text-background" v-bind:ww-object="section.data.rightSectionTextBg" v-bind:section="section" ww-category="background">
          </wwObject>
          <wwObject class="right-text" v-bind:ww-object="section.data.rightText" v-bind:section="section" ww-default-object-type="ww-text"></wwObject>
          <div class="right-bottom-icon" v-bind:ww-object="section.data.rightBottomIcon" v-bind:section="section" ww-category="ww-icon"></div>
          <div class="right-top-icon" v-bind:ww-object="section.data.rightTopIcon" v-bind:section="section" ww-category="ww-icon"></div>
          <div class="right-tail" v-bind:ww-object="section.data.rightTail" v-bind:section="section" ww-category="ww-background"></div>
        </div>
        <div class="right-btn-container">
          <div class="button-container">
            <div class="transition-button">
              <wwObject v-bind:ww-object="section.data.transitionButton" v-bind:section="section" ww-categoy="ww-button"></wwObject>
            </div>
            <div class="slide-btn previous-btn">
              <div class="" @click="previousSlide()" v-bind:ww-object="section.data.previous" v-bind:section="section" ww-default-object-type="ww-icon" ww-object-types-allowed="['ww-icon']" ww-ignore-link="true"></div>
            </div>
            <div class="slide-btn next-btn">
              <div class="" @click="nextSlide()" v-bind:ww-object="section.data.next" v-bind:section="section" ww-default-object-type="ww-icon" ww-object-types-allowed="['ww-icon']" ww-ignore-link="true"></div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<!-- This is your Javascript -->
<!-- ✨ Here comes the magic ✨ -->
<script>
export default {
  name: "testimonial_B",
  props: {
    // The section object is passed to you.
    // It contains all the info and data about the section
    // Use it has you like !
    section: Object
  },
  created() {
    //Initialize section data
    this.section.data = this.section.data || {};
    if (!this.section.data.testimonialBg) {
      this.section.data.testimonialBg = wwLib.wwObject.getDefault({
        type: "ww-image",
        data: {
          url: "http://cdn.wewebapp.io/public/images/weweb-wp.png"
        }
      });
    }

    // left section
    if (!this.section.data.leftSectionBg) {
      this.section.data.leftSectionBg = wwLib.wwObject.getDefault({
        type: "ww-image",
        data: {
          url: "http://cdn.wewebapp.io/public/images/weweb-wp.png"
        }
      });
    }

    if (!this.section.data.contentTitle) {
      this.section.data.contentTitle = wwLib.Object.getDefault({
        type: "ww-text",
        data: {
          text: {
            fr_FR: "Il nous font confiance",
            en_GB: "They trust us"
          },
          align: "center",
          color: "black"
        }
      });
    }

    if (!this.section.data.leftTestimonyBg) {
      this.section.data.leftTestimonyBg = wwLib.wwObject.getDefault({
        type: "ww-image",
        data: {
          url: "http://cdn.wewebapp.io/public/images/weweb-wp.png"
        }
      });
    }

    if (!this.section.data.leftTestimonyBg) {
      this.section.data.leftTestmonyBio = wwLib.Object.getDefault({
        type: "ww-text",
        data: {
          text: {
            fr_FR: "Michel Dow - Directeur immobilier Solvay",
            en_GB: "Michel Dow - Directeur immobilier Solvay"
          },
          align: "center",
          color: "black"
        }
      });
    }

    //right section
    if (!this.section.data.rightSectionBg) {
      this.section.data.rightSectionBg = wwLib.wwObject.getDefault({
        type: "ww-image",
        data: {
          url: "http://cdn.wewebapp.io/public/images/weweb-wp.png"
        }
      });
    }

    if (!this.section.data.rightText) {
      this.section.data.rightText = wwLib.Object.getDefault({
        type: "ww-text",
        data: {
          text: {
            fr_FR:
              "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate",
            en_GB:
              "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate"
          },
          align: "center",
          color: "black"
        }
      });
    }
    if (!this.section.data.rightBottomIcon) {
      this.section.data.rightBottomIcon = wwLib.wwObject.getDefault({
        type: "ww-icon",
        data: {
          url: "http://cdn.wewebapp.io/public/images/weweb-wp.png"
        }
      });
    }
    if (!this.section.data.rightTopIcon) {
      this.section.data.rightTopIcon = wwLib.wwObject.getDefault({
        type: "ww-icon",
        data: {
          url: "http://cdn.wewebapp.io/public/images/weweb-wp.png"
        }
      });
    }
    if (!this.section.data.rightTail) {
      this.section.data.rightTail = wwLib.wwObject.getDefault({
        type: "ww-image",
        data: {
          url: "http://cdn.wewebapp.io/public/images/weweb-wp.png"
        }
      });
    }

    if (!this.section.data.transitionButton) {
      this.section.data.transitionButton = wwLib.Object.getDefault({
        type: "ww-text",
        data: {
          text: {
            fr_FR: "Voir la mission",
            en_GB: "See the mission"
          },
          align: "center",
          color: "black"
        }
      });
    }

    if (!this.section.data.transitionButton) {
      this.section.data.transitionButton = wwLib.Object.getDefault({
        type: "ww-text",
        data: {
          text: {
            fr_FR: "Voir la mission",
            en_GB: "See the mission"
          },
          align: "center",
          color: "black"
        }
      });
    }

    if (!this.section.data.previous) {
      this.section.data.previous = wwLib.Object.getDefault({
        type: "ww-icon",
        data: {
          url: "http://cdn.wewebapp.io/public/images/weweb-wp.png"
        }
      });
    }

    if (!this.section.data.next) {
      this.section.data.next = wwLib.Object.getDefault({
        type: "ww-icon",
        data: {
          url: "http://cdn.wewebapp.io/public/images/weweb-wp.png"
        }
      });
    }
  },
  methods: {}
};
</script>

<!-- This is your CSS -->
<!-- Add "scoped" attribute to limit CSS to this component only -->
<!-- Add lang="scss" or others to use computed CSS -->
<style scoped>
.testimonial_B .content {
  position: relative;
  width: 100%;
  padding-bottom: 100px;
}

/* Left section CSS */
.testimonial_B .left-section {
  width: 50%;
  height: 100%;
}

.testimonial_B .testmoniy-right-bg {
  width: 100px;
}

.testimonial_B .testmoniy-right-bio {
  width: 100px;
}

.testimonial_B .right-section {
  width: 50%;
  height: 100%;
}

.testimonial_B .right-section-background {
  width: 100px;
}

.testimonial_B .right-section-text {
  width: 100px;
}

.testimonial_B .right-text-background {
  width: 100px;
}

.testimonial_B .right-text {
  width: 50px;
}

.testimonial_B .right-bottom-icon {
  width: 30px;
  height: 30px;
}

.testimonial_B .right-top-icon {
  width: 30px;
  height: 30px;
}

.testimonial_B .right-tail {
  width: 30px;
  height: 30px;
}

.testimonial_B .right-btn-container {
  width: 100%;
  height: 50px;
}

.testimonial_B .button-container {
  width: 100px;
}

.testimonial_B .transition-button {
  width: 100px;
}

.testimonial_B .slide-btn {
  width: 30px;
  height: 30px;
}

.testimonial_B .previous-btn {
  margin: 0;
}

.testimonial_B .next-btn {
  margin: 0;
}

.testimonial_B .background {
  position: absolute;
  top: 0;
  left: 0;
  height: 100%;
  width: 100%;
}
</style>
