
<!-- This is a Vue.js single file component. -->
<!-- Check the Vue.js doc here :  -->
<!-- https://vuejs.org/v2/guide/ -->

<!-- This is your HTML -->
<template>
    <div class="testimonial_B">

        <!-- Weweb Wallpaper -->
        <wwObject class="background" v-bind:ww-object="section.data.wewebWP" v-bind:section="section" ww-category="background"></wwObject>
        <div class="content">
            <wwObject v-bind:ww-object="section.data.testimonialB" v-bind:section="section"></wwObject>

            <div class="content-title">
                <div v-bind:ww-object="section.data.contentTitle" v-bind:section="section" ww-default-object-type="ww-text"></div>
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
                    <div class="testimony-arrows-container text-center">
                        <div class="transition-button">
                            <wwObject v-bind:ww-object="section.data.transitionButton" v-bind:section="section"></wwObject>
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

    if (!this.section.data.leftTestimonyBg) {
      this.section.data.leftTestimonyBg = wwLib.wwObject.getDefault({
        type: "ww-text",
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

    //Initialize image
    if (!this.section.data.wewebWP) {
      this.section.data.wewebWP = wwLib.wwObject.getDefault({
        type: "ww-image",
        data: {
          url: "http://cdn.wewebapp.io/public/images/weweb-wp.png"
        }
      });
    }

    if (!this.section.data.leftTestimonyBg) {
      this.section.data.leftTestimonyBg = wwLib.Object.getDefault({
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
  },
  methods: {}
};
</script>

<!-- This is your CSS -->
<!-- Add "scoped" attribute to limit CSS to this component only -->
<!-- Add lang="scss" or others to use computed CSS -->
<style scoped>
.hello {
  padding: 100px 50px;
}

.background {
  position: absolute;
  top: 0;
  left: 0;
  height: 100%;
  width: 100%;
}

.content {
  position: relative;
}
.testimonial_B .container {
  width: 100%;
  position: relative;
}

.testimonial_B .testimony-bg,
.testimonial_B .testimony-text-bg,
.testimonial_B .testimony-info-bg {
  position: absolute;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
}

.testimonial_B .testimony-photo {
  position: absolute;
  width: 50%;
  height: 125%;
  top: 0;
  left: 25%;
}

.testimonial_B .slider-container {
  position: relative;
  display: flex;

  -webkit-transition: transform 0.5s ease;
  -moz-transition: transform 0.5s ease;
  -o-transition: transform 0.5s ease;
  transition: transform 0.5s ease;

  transition-delay: 0.3s;
}

.testimonial_B .slide {
  /*display: flex;*/

  overflow-x: hidden;

  position: relative;

  /*
    -webkit-transform: translateX(100%);
    -moz-transform: translateX(100%);
    -o-transform: translateX(100%);
    transform: translateX(100%);
    */

  /*
    -webkit-transition: all 0.5s ease;
    -moz-transition: all 0.5s ease;
    -o-transition: all 0.5s ease;
    transition: all 0.5s ease;
    */

  transition-delay: 0.3s;
}

.testimonial_B .slide.slide-hidden:not(.active) {
  display: none;
}

/* ACTIVE ------------------------------------------------- */
.testimonial_B .slide.active {
  /*
    -webkit-transform: translateX(0);
    -moz-transform: translateX(0);
    -o-transform: translateX(0);
    transform: translateX(0);
    */
}

.testimonial_B .slide.active .testimony-photo {
  -webkit-transition: transform 0.5s ease;
  -moz-transition: transform 0.5s ease;
  -o-transition: transform 0.5s ease;
  transition: transform 0.5s ease;

  transition-delay: 0.6s;
}

.testimonial_B .slide.active .testimony-text-container,
.testimonial_B .slide.active .testimony-bottom-container {
  -webkit-transition: transform 0.5s ease;
  -moz-transition: transform 0.5s ease;
  -o-transition: transform 0.5s ease;
  transition: transform 0.5s ease;

  transition-delay: 0.8s;
}

/* PREVIOUS ----------------------------------------------- */

.testimonial_B .slide.previous {
  /*
    -webkit-transform: translateX(-100%);
    -moz-transform: translateX(-100%);
    -o-transform: translateX(-100%);
    transform: translateX(-100%);
    */
}

.testimonial_B .slide.previous .testimony-photo {
  -webkit-transition: transform 0.5s ease;
  -moz-transition: transform 0.5s ease;
  -o-transition: transform 0.5s ease;
  transition: transform 0.5s ease;

  -webkit-transform: translateX(-150%);
  -moz-transform: translateX(-150%);
  -o-transform: translateX(-150%);
  transform: translateX(-150%);
}

.testimonial_B .slide.previous .testimony-text-container,
.testimonial_B .slide.previous .testimony-bottom-container {
  -webkit-transition: transform 0.5s ease;
  -moz-transition: transform 0.5s ease;
  -o-transition: transform 0.5s ease;
  transition: transform 0.5s ease;

  -webkit-transform: translateX(1000px);
  -moz-transform: translateX(1000px);
  -o-transform: translateX(1000px);
  transform: translateX(1000px);

  transition-delay: 0.2s;
}

.testimonial_B .slide.previous .next-btn {
  -webkit-transition: all 0.5s ease;
  -moz-transition: all 0.5s ease;
  -o-transition: all 0.5s ease;
  transition: all 0.5s ease;

  -webkit-transform: translateX(150%);
  -moz-transform: translateX(150%);
  -o-transform: translateX(150%);
  transform: translateX(150%);

  opacity: 0;
}

/* NEXT --------------------------------------------------- */
.testimonial_B .slide.next .testimony-photo {
  -webkit-transition: transform 0.5s ease;
  -moz-transition: transform 0.5s ease;
  -o-transition: transform 0.5s ease;
  transition: transform 0.5s ease;

  -webkit-transform: translateX(-150%);
  -moz-transform: translateX(-150%);
  -o-transform: translateX(-150%);
  transform: translateX(-150%);
}

.testimonial_B .slide.next .testimony-text-container,
.testimonial_B .slide.next .testimony-bottom-container {
  -webkit-transition: transform 0.5s ease;
  -moz-transition: transform 0.5s ease;
  -o-transition: transform 0.5s ease;
  transition: transform 0.5s ease;

  -webkit-transform: translateX(1000px);
  -moz-transform: translateX(1000px);
  -o-transform: translateX(1000px);
  transform: translateX(1000px);

  transition-delay: 0.2s;
}

.testimonial_B .slide.next .previous-btn {
  -webkit-transition: all 0.5s ease;
  -moz-transition: all 0.5s ease;
  -o-transition: all 0.5s ease;
  transition: all 0.5s ease;

  -webkit-transform: translateX(-150%);
  -moz-transform: translateX(-150%);
  -o-transform: translateX(-150%);
  transform: translateX(-150%);

  opacity: 0;
}

/* ------------------------------------------------------- */

.testimonial_B .testimony-text,
.testimonial_B .testimony-info {
  position: relative;
}

.testimonial_B .remove-ww-obj {
  position: absolute;
  top: 0;
  left: 0;
  transform: translate(-50%, -50%);
  height: 30px;
  width: 30px;
  background-color: white;
  color: #92979c;
  box-shadow: 0px 1px 1px 0px #656565;
  -moz-box-shadow: 0px 1px 1px 0px #656565;
  -webkit-box-shadow: 0px 1px 1px 0px #656565;
  border-radius: 100%;
  text-align: center;
  line-height: 30px;
  cursor: pointer;
  z-index: 2;
}

.testimonial_B .add-ww-obj-container {
  text-align: center;
  margin: 10px 0;
}

.testimonial_B .add-ww-obj-container .add-ww-obj {
  display: inline-block;
  height: 40px;
  width: 40px;
  line-height: 40px;
  text-align: center;
  background-color: white;
  box-shadow: 0 1px 2px 0 rgba(0, 0, 0, 0.5);
  border-radius: 3px;
  -webkit-border-radius: 3px;
  -moz-border-radius: 3px;
  cursor: pointer;
}

.testimonial_B .manage-slides-buttons {
  position: absolute;
  bottom: 5px;
  left: 50%;
  transform: translateX(-50%);
}

.testimonial_B .add-slide-button {
  display: inline-block;
  width: auto;
}

.testimonial_B .remove-slide-button {
  display: inline-block;
  width: auto;
}

.testimonial_B .testimony-photo-container {
  width: 100%;
  position: relative;
  overflow: hidden;
  height: 230px;
}

.testimonial_B .slide-right {
  width: 100%;
  position: relative;
  min-height: calc(100% - 230px);
}

.testimonial_B .testimony-text-container {
  width: 100%;
  min-height: 30px;
  position: relative;
}

.testimonial_B .testimony-bottom-container {
  width: 100%;
  position: relative;
  display: flex;
}

.testimonial_B .testimony-info-container {
  width: 80%;
  position: absolute;
  min-height: 30px;
  top: -40px;
  left: 10%;
  border-radius: 7px;
  overflow: hidden;
}

.testimonial_B .testimony-arrows-container {
  /* float: right; */
  width: 100%;
  /* max-width: 300px; */
  min-height: 30px;
  /* position: relative; */
  align-items: center;
  justify-content: center;
  position: absolute;
  top: -22px;
}

.testimonial_B .testimony-bg-container {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  -webkit-transform: translateZ(0);
  -moz-transform: translateZ(0);
  -o-transform: translateZ(0);
  transform: translateZ(0);
}

.testimonial_B .testimony-text-content,
.testimonial_B .testimony-info-content {
  position: relative;
  width: 100%;
  height: 100%;
}

.testimonial_B .testimony-dialog-tail {
  display: none;
}

.testimonial_B .slide-btn {
  cursor: pointer;
}

.testimonial_B .previous-btn {
  float: left;
  margin-left: 5px;
}

.testimonial_B .next-btn {
  float: right;
  margin-right: 5px;
}

@media (min-width: 480px) {
}

@media (min-width: 768px) {
}

@media (min-width: 992px) {
  .testimonial_B .testimony-photo-container {
    width: 100%;
    height: 100%;
    position: absolute;
    top: 0;
    left: 0;
    padding-bottom: 0;
  }

  .testimonial_B .testimony-photo {
    left: 0;
    height: 100%;
  }

  .testimonial_B .slide-right {
    padding: 100px 50px 50px 50px;
    width: 50%;
    height: 100%;
    margin-left: 50%;
  }

  .testimonial_B .testimony-text-container {
    max-width: 600px;
    margin-bottom: 30px;
  }

  .testimonial_B .testimony-bg-container {
    border-radius: 7px;
    overflow: hidden;
  }

  .testimonial_B .testimony-dialog-tail {
    display: block;
    width: 20px;
    height: 20px;
    position: absolute;
    left: 0;
    bottom: 30px;
    -webkit-transform: translateX(-50%) rotate(45deg);
    -moz-transform: translateX(-50%) rotate(45deg);
    -o-transform: translateX(-50%) rotate(45deg);
    transform: translateX(-50%) rotate(45deg);
  }

  .testimonial_B .testimony-bottom-container {
    max-width: 600px;
    min-height: 30px;
  }

  .testimonial_B .testimony-info-container {
    width: 50%;
    /*float:left;*/
    max-width: 300px;
    min-height: 30px;
    position: relative;
    left: 0;
    top: 0;
  }

  .testimonial_B .testimony-arrows-container {
    float: right;
    width: 50%;
    max-width: 300px;
    min-height: 30px;
    position: relative;
    align-items: center;
    justify-content: center;
    display: flex;
    top: 0;
  }

  .testimonial_B .previous-btn {
    margin-right: 25px;
    float: none;
    margin-left: 0;
  }

  .testimonial_B .next-btn {
    float: none;
    margin-right: 0;
  }
}

@media (min-width: 1200px) {
}

@media (min-width: 1900px) {
}
</style>
