
<!-- This is a Vue.js single file component. -->
<!-- Check the Vue.js doc here :  -->
<!-- https://vuejs.org/v2/guide/ -->

<!-- This is your HTML -->
<template>
  <div class="testimonial_B">
    <!-- wwManager:start -->
    <wwSectionEditMenu v-bind:section="section"></wwSectionEditMenu>
    <!-- wwManager:end -->

    <wwObject class="background" v-bind:ww-object="section.data.testimonialBg" v-bind:section="section" ww-category="background"></wwObject>
    <div class="content">

      <div :class="{'left-content-animation-start': isActive, 'left-content-animation-end': notActive}" class="left-section">
        <wwObject class="left-section-bg" v-bind:ww-object="section.data.leftSectionBg" v-bind:section="section" ww-category="background"></wwObject>

        <div class="testimony-left-pic-container">
          <wwObject class="testimony-left-pic" tag="div" v-bind:ww-object="section.data.leftTestimonyPic" v-bind:section="section" ww-category="background">
          </wwObject>
        </div>

        <div class="testimony-left-bio">
          <wwObject tag="div" v-bind:ww-object="section.data.leftTestmonyBio" v-bind:section="section" ww-default-object-type="ww-text"></wwObject>
        </div>
      </div>

      <div :class="{'right-contet-animation-start': isActive, 'right-contet-animation-end': notActive}" class="right-section">

        <wwObject class="right-section-bg" v-bind:ww-object="section.data.rightSectionBg" v-bind:section="section" ww-category="background">
        </wwObject>

        <div class="right-section-text-container">
          <wwObject class="right-text-bg" v-bind:ww-object="section.data.rightSectionTextBg" v-bind:section="section" ww-category="background">
          </wwObject>
          <wwObject class="right-text" v-bind:ww-object="section.data.rightText" v-bind:section="section" ww-default-object-type="ww-text"></wwObject>
          <div class="right-icon right-bottom-icon fa fa-quote-right" v-bind:ww-object="section.data.rightBottomIcon" v-bind:section="section" ww-category="ww-icon"></div>
          <div class="right-icon right-top-icon fa fa-quote-left" v-bind:ww-object="section.data.rightTopIcon" v-bind:section="section" ww-category="ww-icon"></div>
          <div class="right-tail" v-bind:ww-object="section.data.rightTail" v-bind:section="section" ww-category="ww-background"></div>
        </div>

        <div class="button-container">

          <div class="mission-button">
            <wwObject v-bind:ww-object="section.data.transitionButton" v-bind:section="section" ww-inside-ww-object="true" ww-default-object-type="ww-text" ww-object-types-allowed="['ww-text']">
            </wwObject>
          </div>

          <div class="transition-button">
            <div>
              <wwObject class="slide previous-btn" @click.native="previousFn" v-bind:ww-object="section.data.previousBtn" v-bind:section="section" ww-category="ww-icon"></wwObject>
            </div>
            <div>
              <wwObject class="slide next-btn" @click.native="nextFn" v-bind:ww-object="section.data.nextBtn" v-bind:section="section" ww-category="ww-icon"></wwObject>
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
    // Use it as you like !
    section: Object
  },

  data() {
    return {
      isActiveLeft: false,
      isActiveRight: false,
      isActive: false,
      notActive: false
    };
  },
  methods: {
    wait(ms) {
      return new Promise((r, j) => setTimeout(r, ms));
    },
    slideFn() {
      this.isActive = true;
      this.wait(1000)
        .then(() => {
          this.notActive = !this.notActive;
          this.wait(1000)
            .then(() => {
              this.isActive = false;
              this.notActive = false;
            })
            .catch(err => {});
        })
        .catch(err => {});
    },
    previousFn() {
      this.slideFn();
    },
    nextFn() {
      this.slideFn();
    }
  },
  created() {
    //Initialize section data
    this.section.data = this.section.data || {};

    if (!this.section.data.testimonialBg) {
      this.section.data.testimonialBg = wwLib.wwObject.getDefault({
        type: "ww-image",
        data: {}
      });
    }

    if (!this.section.data.contentTitle) {
      this.section.data.contentTitle = wwLib.wwObject.getDefault({
        type: "ww-text",
        data: {
          text: {
            fr_FR: "Il nous font confiance",
            en_GB: "They trust us"
          },
          align: "center",
          size: 2,
          color: "black"
        }
      });
    }
    // left section
    if (!this.section.data.leftSectionBg) {
      this.section.data.leftSectionBg = wwLib.wwObject.getDefault({
        type: "ww-image",
        data: {}
      });
    }

    if (!this.section.data.leftTestimonyPic) {
      this.section.data.leftTestimonyPic = wwLib.wwObject.getDefault({
        type: "ww-image",
        data: {
          url:
            "https://wewebprod.s3.eu-west-1.amazonaws.com/designs/277/sections/Mqtvc0q6xHHeMeYXeFed48x7gXje6ufu.png"
        }
      });
    }
    //

    if (!this.section.data.leftTestmonyBio) {
      this.section.data.leftTestmonyBio = wwLib.wwObject.getDefault({
        type: "ww-text",
        data: {
          text: {
            fr_FR: "Michel Dow - Directeur immobilier Solvay",
            en_GB: "Michel Dow - Directeur immobilier Solvay"
          },
          align: "left",
          color: "white"
        }
      });
    }

    //right section
    if (!this.section.data.rightSectionBg) {
      this.section.data.rightSectionBg = wwLib.wwObject.getDefault({
        type: "ww-image",
        data: {}
      });
    }

    if (!this.section.data.rightSectionTextBg) {
      this.section.data.rightSectionTextBg = wwLib.wwObject.getDefault({
        type: "ww-image",
        data: {}
      });
    }

    if (!this.section.data.rightText) {
      this.section.data.rightText = wwLib.wwObject.getDefault({
        type: "ww-text",
        data: {
          text: {
            fr_FR:
              "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate",
            en_GB:
              "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate"
          },
          align: "justify",
          color: "white"
        }
      });
    }
    if (!this.section.data.rightBottomIcon) {
      this.section.data.rightBottomIcon = wwLib.wwObject.getDefault({
        type: "ww-icon",
        data: {}
      });
    }
    if (!this.section.data.rightTopIcon) {
      this.section.data.rightTopIcon = wwLib.wwObject.getDefault({
        type: "ww-icon",
        data: {}
      });
    }
    if (!this.section.data.rightTail) {
      this.section.data.rightTail = wwLib.wwObject.getDefault({
        type: "ww-image",
        data: {}
      });
    }

    if (!this.section.data.transitionButton) {
      this.section.data.transitionButton = wwLib.wwObject.getDefault({
        type: "ww-text",
        data: {
          text: {
            fr_FR: "Voir la mission",
            en_GB: "See the mission"
          },
          prev: true,
          align: "center",
          color: "black"
        }
      });
    }

    if (!this.section.data.previous) {
      this.section.data.previousBtn = wwLib.wwObject.getDefault({
        type: "ww-icon",
        data: {
          icon: "fa fa-chevron-left",
          color: "#897978",
          backgroundColor: "#FFFFFF",
          borderColor: "",
          classes: [
            "ww-class-img-format-round",
            "ww-class-font-size-small",
            "ww-class-icon-size-medium"
          ]
        }
      });
    }

    if (!this.section.data.next) {
      this.section.data.nextBtn = wwLib.wwObject.getDefault({
        type: "ww-icon",
        data: {
          icon: "fa fa-chevron-right",
          color: "#897978",
          backgroundColor: "#FFFFFF",
          borderColor: "",
          classes: [
            "ww-class-img-format-round",
            "ww-class-font-size-small",
            "ww-class-icon-size-medium"
          ]
        }
      });
    }
  }
};
</script>

<!-- This is your CSS -->
<!-- Add "scoped" attribute to limit CSS to this component only -->
<!-- Add lang="scss" or others to use computed CSS -->
<style scoped>
.testimonial_B {
  position: relative;
}

.testimonial_B .background {
  position: absolute;
  top: 0;
  left: 0;
  height: 100%;
  width: 100%;
  z-index: -1;
  overflow: hidden;
}

.testimonial_B .content {
  position: relative;

  width: 100%;
  height: 700px;
  padding-bottom: 100px;
}

/* Left section CSS */
.testimonial_B .left-section {
  width: 50%;
  height: 100%;
  position: absolute;
  left: 0px;
}

.testimonial_B .left-section-bg {
  width: 100%;
  height: 100%;
  background-color: white;
}
.testimonial_B .testimony-left-pic-container {
  width: 350px;
  height: 400px;
  position: absolute;
  left: 0;
  top: 0px;
  margin-left: 50%;
}
/* #FF3F66 -rose
  #897978 -grey text
*/
.testimonial_B .testimony-left-pic {
  width: 100%;
  height: 100%;
}

.testimonial_B .testimony-left-bio {
  width: 40%;
  height: 100px;
  background-color: #ff3f66;
  padding: 20px;
  margin-left: 50%;
  bottom: 20%;
  position: absolute;
}

.testimonial_B .right-section {
  width: 50%;
  height: 100%;
  position: relative;
  margin-left: 50%;
}

.testimonial_B .right-section-bg {
  width: 100%;
  height: 100%;
  background-color: white;
}

.testimonial_B .right-section-text-container {
  width: 55%;
  height: 55%;
  position: absolute;
  top: 0px;
}

.testimonial_B .right-text-bg {
  width: 100%;
  height: 100%;
  margin: 10% 0 0 10%;
  position: absolute;
  border-radius: 25px;
  box-sizing: border-box;

  background-color: #897978;
}

.testimonial_B .right-text {
  width: 80%;
  height: 80%;
  margin: 20%;
  line-height: 25px;
}

.testimonial_B .right-icon {
  width: 30px;
  height: 30px;
  padding: 4px;
  background-color: #897978;
  position: absolute;
  align-self: center;
  color: rgb(255, 255, 255);
  display: block;
  font-size: 20px;
  font-stretch: 100%;
  font-style: normal;
  font-weight: 400;
  border-radius: 5px;
  box-sizing: border-box;
  line-height: 24px;
  text-align: center;
}

.testimonial_B .right-tail {
  width: 30px;
  height: 30px;
  position: absolute;
  top: 100px;
  left: 10%;
  font-size: 20px;
  background-color: #897978;
  transform: matrix(0.707107, 0.707107, -0.707107, 0.707107, -15, 0);
}

.testimonial_B .button-container {
  width: 60%;
  height: 100px;
  position: absolute;
  bottom: 10px;
  left: 10%;
  display: inline-flex;
  text-size-adjust: 100%;
}

.testimonial_B .mission-button {
  width: 140px;
  height: 38px;
  background-color: rgb(255, 255, 255);
  border-radius: 500px;
  border-color: rgb(137, 121, 120);
  border-style: solid;
  border-width: 2px;
  box-sizing: border-box;
  color: rgb(137, 121, 120);
  cursor: pointer;
  font-size: 14px;
  line-height: 150%;
  padding: 5px 10px 10px 5px;
  text-align: center;
  margin-top: 1.5%;
}
.testimonial_B .transition-button {
  float: right;
  margin-left: 10%;
}

.testimonial_B .slide {
  width: 45px;
  height: 45px;
  text-align: center;
  color: rgb(137, 121, 120);
  cursor: pointer;
  font-size: 25px;
  line-height: 130%;
  border-radius: 500px;
  border-color: rgb(137, 121, 120);
  border-style: solid;
  border-width: 2px;
  padding: 10px;
  pointer-events: auto;
}

.testimonial_B .previous-btn {
  float: left;
  margin-right: 40px;
}

.testimonial_B .next-btn {
  float: right;
}

/* ------------------------Start------------------------- */

.testimonial_B .left-content-animation-start {
  -webkit-transition: transform 0.5s ease;
  -moz-transition: transform 0.5s ease;
  -o-transition: transform 0.5s ease;
  transition: transform 0.5s ease;

  -webkit-transform: translateX(-150%);
  -moz-transform: translateX(-150%);
  -o-transform: translateX(-150%);
  transform: translateX(-150%);
}

.testimonial_B .right-contet-animation-start {
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

/* ------------------------End------------------------- */

.testimonial_B .left-content-animation-end {
  -webkit-transition: transform 0.5s ease;
  -moz-transition: transform 0.5s ease;
  -o-transition: transform 0.5s ease;
  transition: transform 0.5s ease;

  -webkit-transform: translateX(0);
  -moz-transform: translateX(0);
  -o-transform: translateX(0%);
  transform: translateX(0);
}

.testimonial_B .right-contet-animation-end {
  -webkit-transition: transform 0.5s ease;
  -moz-transition: transform 0.5s ease;
  -o-transition: transform 0.5s ease;
  transition: transform 0.5s ease;

  -webkit-transform: translateX(0);
  -moz-transform: translateX(0);
  -o-transform: translateX(0);
  transform: translateX(0);

  transition-delay: 0.2s;
}

@media (max-width: 750px) {
  .testimonial_B .content {
    position: relative;
    width: 100%;
    height: 700px;
    padding-bottom: 100px;
    overflow: visible;
  }

  /* Left section CSS */
  .testimonial_B .left-section {
    width: 100%;
    height: 50%;
    position: relative;
  }

  .testimonial_B .left-section-bg {
    width: 100%;
    height: 100%;
    background-color: white;
  }
  .testimonial_B .testimony-left-pic-container {
    width: 60%;
    height: 100%;
    position: absolute;
    left: 0;
    top: 0px;
    margin-left: 20%;
  }
  /* #FF3F66 -rose
  #897978 -grey text
*/
  .testimonial_B .testimony-left-pic {
    width: 100%;
    height: 100%;
  }

  .testimonial_B .testimony-left-bio {
    width: 60%;
    height: 50px;
    padding: 10px;
    font-size: 12px;
    margin-left: 20%;
    bottom: -10px;
    position: relative;
  }

  .testimonial_B .right-section {
    width: 100%;
    height: 50%;
    position: relative;
    top: 15%;
    margin-left: 0%;
  }

  .testimonial_B .right-section-bg {
    width: 100%;
    height: 100%;
    background-color: white;
  }

  .testimonial_B .right-section-text-container {
    width: 90%;
    height: 100%;
    position: absolute;
    top: 0px;
    margin-left: 5%;
  }

  .testimonial_B .right-text-bg {
    width: 100%;
    height: 100%;
    margin: 0px;
    position: absolute;
    border-radius: 0px;
    box-sizing: border-box;

    background-color: #897978;
  }

  .testimonial_B .right-text {
    width: 80%;
    height: 80%;
    margin: 10%;
    line-height: 25px;
  }

  .testimonial_B .right-icon {
    display: none;
  }

  .testimonial_B .right-tail {
    display: none;
  }

  .testimonial_B .button-container {
    width: 90%;
    height: 100px;
    position: relative;
    bottom: -10px;
    left: 0;
    margin-left: 5%;
  }
}

.testimonial_B .mission-button {
  width: 140px;
  height: 38px;
  font-size: 14px;
  line-height: 150%;
  margin-left: calc((100% - 140px) / 2);
}
.testimonial_B .transition-button {
  float: right;
  margin-left: 10%;
}

.testimonial_B .slide {
  width: 45px;
  height: 45px;
  font-size: 25px;
  line-height: 130%;
  padding: 10px;
}

.testimonial_B .previous-btn {
  position: absolute;
  left: 0px;
}

.testimonial_B .next-btn {
  position: absolute;
  right: 0px;
}

@media (min-width: 768px) and (max-width: 900px) {
  .testimonial_B .content {
    overflow: hidden;
  }
  .testimonial_B .testimony-left-pic-container {
    width: 70%;
    height: 400px;
    position: absolute;
    left: 0;
    top: 0px;
    margin-left: 30%;
  }

  .testimonial_B .testimony-left-bio {
    width: 70%;
    height: 100px;
    background-color: #ff3f66;
    padding: 20px;
    margin-left: 30%;
    bottom: 20%;
    position: absolute;
  }

  .testimonial_B .right-section-text-container {
    width: 80%;
    height: 60%;
    position: absolute;
    top: 0px;
  }
  .testimonial_B .right-bottom-icon {
    right: 10%;
    bottom: -13%;
  }

  .testimonial_B .right-top-icon {
    top: 6%;
    left: 25%;
  }
  .testimonial_B .button-container {
    width: 70%;
    margin-left: 5%;
  }

  .testimonial_B .slide {
    width: 45px;
    height: 45px;
    cursor: pointer;
    line-height: 80%;
    padding: 10px 0px 10px 0px;
  }
}

@media (min-width: 992px) {
  .testimonial_B .content {
    overflow: hidden;
  }
  .testimonial_B .testimony-left-pic-container {
    width: 60%;
    margin-left: 40%;
  }
  .testimonial_B .testimony-left-bio {
    width: 60%;
    margin-left: 40%;
  }
  .testimonial_B .right-section-text-container {
    width: 70%;
    height: 60%;
    position: absolute;
    top: 0px;
  }
  .testimonial_B .right-bottom-icon {
    right: 10%;
    bottom: -13%;
  }

  .testimonial_B .right-top-icon {
    top: 6%;
    left: 25%;
  }
  .testimonial_B .button-container {
    width: 60%;
    height: 100px;
    position: absolute;
    bottom: 10px;
    left: 12%;
    display: inline-flex;
    text-size-adjust: 100%;
  }

  .testimonial_B .slide {
    width: 45px;
    height: 45px;
    line-height: 95%;
    padding: 10px;
  }
}

@media (min-width: 1400px) {
  .testimonial_B .content {
    overflow: hidden;
  }
  .testimonial_B .testimony-left-pic-container {
    width: 50%;
    margin-left: 50%;
  }
  .testimonial_B .testimony-left-bio {
    width: 50%;
    margin-left: 50%;
  }

  .testimonial_B .right-section-text-container {
    width: 55%;
    height: 55%;
  }

  .testimonial_B .slide {
    width: 45px;
    height: 45px;
    line-height: 130%;
    padding: 5px;
  }
  .testimonial_B .right-bottom-icon {
    right: 10%;
    bottom: -18%;
  }

  .testimonial_B .right-top-icon {
    top: 11%;
    left: 25%;
  }

  .testimonial_B .button-container {
    width: 40%;
    height: 100px;
    position: absolute;
    bottom: 10px;
    left: 15%;
    display: inline-flex;
    text-size-adjust: 100%;
  }
}
</style>
