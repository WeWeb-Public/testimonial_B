
<!-- This is a Vue.js single file component. -->
<!-- Check the Vue.js doc here :  -->
<!-- https://vuejs.org/v2/guide/ -->

<!-- This is your HTML -->
<template>
    <div class="testimonial_B">
        <!-- wwManager:start -->
        <wwSectionEditMenu :sectionCtrl="sectionCtrl"></wwSectionEditMenu>
        <!-- wwManager:end -->
        <wwObject class="background" v-bind:ww-object="section.data.testimonialBg" v-bind:section="section" ww-category="background"></wwObject>

        <!--TOP WWOBJS-->
        <div class="top-ww-objs">
            <wwLayoutColumn tag="div" ww-default="ww-text" :ww-list="section.data.topWwObjs" @ww-add="add(section.data.topWwObjs, $event)" @ww-remove="remove(section.data.topWwObjs, $event)">
                <wwObject v-for="topWwObj in section.data.topWwObjs" :key="topWwObj.uniqueId" :ww-object="topWwObj"></wwObject>
            </wwLayoutColumn>
        </div>

        <div class="content" :style="{'width':(100 / section.data.testimonies.length) + '%'}" ww-min-height="80" v-for="(testimony, index) in section.data.testimonies" :key="testimony.uniqueId" :class="{'active': activeTestimony == index, 'previous': activeTestimony > index, 'next': activeTestimony < index, 'slide-hidden': !loaded}">
            <!--  <div class="slide" :style="{'width':(100 / section.data.testimonies.length) + '%'}" ww-min-height="80" v-for="(testimony, index) in section.data.testimonies" :key="testimony.uniqueId" :class="{'active': activeTestimony == index, 'previous': activeTestimony > index, 'next': activeTestimony < index, 'slide-hidden': !loaded}"> -->
            <div :class="{'left-content-animation-start': isActive, 'left-content-animation-end': notActive}" class="left-section">
                <wwObject class="left-section-bg" v-bind:ww-object="section.data.leftSectionBg" v-bind:section="section" ww-category="background"></wwObject>

                <div class="testimony-left-pic-container">
                    <wwObject class="testimony-left-pic" tag="div" v-bind:ww-object="section.data.leftTestimonyPic" v-bind:section="section" ww-category="background"></wwObject>
                </div>

                <div class="testimony-left-bio">
                    <wwObject tag="div" v-bind:ww-object="section.data.leftTestmonyBio" v-bind:section="section" ww-default-object-type="ww-text"></wwObject>
                </div>
            </div>

            <div :class="{'right-content-animation-start': isActive, 'right-content-animation-end': notActive}" class="right-section">
                <wwObject class="right-section-bg" v-bind:ww-object="section.data.rightSectionBg" v-bind:section="section" ww-category="background"></wwObject>

                <div class="right-section-text-container">
                    <wwObject class="right-text-bg" v-bind:ww-object="section.data.rightSectionTextBg" v-bind:section="section" ww-category="background"></wwObject>
                    <wwLayoutColumn tag="div" ww-default="ww-text" :ww-list="testimony.texts" class="right-text" @ww-add="addNewText(testimony.texts, $event, testimony)" @ww-remove="removeText(testimony.texts, $event)">
                        <wwObject v-for="(text, index) in testimony.texts" :key="index" :ww-object="text"></wwObject>
                    </wwLayoutColumn>

                    <div class="right-icon right-bottom-icon fa fa-quote-right" :ww-object="section.data.rightBottomIcon" ww-category="ww-icon"></div>
                    <div class="right-icon right-top-icon fa fa-quote-left" :ww-object="section.data.rightTopIcon" ww-category="ww-icon"></div>
                    <div class="right-tail" :ww-object="section.data.rightTail" ww-category="ww-background"></div>
                </div>

                <div class="button-container">
                    <div class="mission-button">
                        <wwObject v-bind:ww-object="section.data.transitionButton" v-bind:section="section" ww-inside-ww-object="true" ww-default-object-type="ww-text" ww-object-types-allowed="['ww-text']"></wwObject>
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

        <wwLayoutColumn tag="div" ww-default="ww-text" :ww-list="section.data.testimonies" class="add-testimony" @ww-add="addTestimony($event)" @ww-remove="removeTestimony($event)">add new testimony</wwLayoutColumn>

        <div class="bottom-ww-objs">
            <wwLayoutColumn tag="div" ww-default="ww-text" :ww-list="section.data.bottomWwObjs" @ww-add="add(section.data.bottomWwObjs, $event)" @ww-remove="remove(section.data.bottomWwObjs, $event)">
                <wwObject v-for="bottomWwObjs in section.data.bottomWwObjs" :key="bottomWwObjs.uniqueId" :ww-object="bottomWwObjs"></wwObject>
            </wwLayoutColumn>
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
        sectionCtrl: Object
    },

    data() {
        return {
            isActiveLeft: false,
            isActiveRight: false,
            isActive: false,
            notActive: false,
            activeTestimony: 0,
            loaded: false
        };
    },
    computed: {
        //Get the section object here !
        // It contains all the info and data about the section
        // Use it has you like !
        section() {
            return this.sectionCtrl.get();
        }
    },
    created() {
        //Initialize section data
        this.section.data = this.section.data || {};
        let needUpdate = false;

        this.section.data.testimonies = this.section.data.testimonies || [];

        if (_.isEmpty(this.section.data.topWwObjs)) {
            this.section.data.topWwObjs = [];
            needUpdate = true;
        }

        if (_.isEmpty(this.section.data.bottomWwObjs)) {
            this.section.data.bottomWwObjs = [];
            needUpdate = true;
        }
        if (!this.section.data.testimonialBg) {
            this.section.data.testimonialBg = wwLib.wwObject.getDefault({
                type: "ww-image",
                data: {
                    url: "http://cdn.wewebapp.io/public/images/weweb-wp.png"
                }
            });
        }

        if (!this.section.data.contentTitle) {
            this.section.data.contentTitle = wwLib.wwObject.getDefault({
                type: "ww-text",
                data: {
                    text: {
                        fr: "Il nous font confiance",
                        en: "They trust us"
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
                data: {
                    url: "http://cdn.wewebapp.io/public/images/weweb-wp.png"
                }
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
                        fr: "Michel Dow - Directeur immobilier Solvay",
                        en: "Michel Dow - Directeur immobilier Solvay"
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
                data: {
                    url: "http://cdn.wewebapp.io/public/images/weweb-wp.png"
                }
            });
        }

        if (!this.section.data.rightSectionTextBg) {
            this.section.data.rightSectionTextBg = wwLib.wwObject.getDefault({
                type: "ww-image",
                data: {
                    url: "http://cdn.wewebapp.io/public/images/weweb-wp.png"
                }
            });
        }

        if (!this.section.data.rightText) {
            this.section.data.rightText = wwLib.wwObject.getDefault({
                type: "ww-text",
                data: {
                    text: {
                        fr:
                            "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate",
                        en:
                            "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate"
                    },
                    align: "justify",
                    color: "white"
                }
            });
        }
        if (!this.section.data.text) {
            this.section.data.text = wwLib.wwObject.getDefault({
                type: "ww-text"
            });
            needUpdate = true;
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
                        fr: "Voir la mission",
                        en: "See the mission"
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
                    icon: "fa fa-arrow-left",
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
                    icon: "fa fa-arrow-right",
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

        if (needUpdate) {
            this.sectionCtrl.update(this.section);
        }

        setTimeout(() => {
            this.loaded = true;
            /* this.setTextTopPadding(); */
        }, 1);
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
        },

        addTestimony(option) {
            console.log("inside addtestimony");
            this.section.data.testimonies.splice(option.index, 0, {
                texts: [],
                infos: [],
                uniqueId: wwLib.wwUtils.getUniqueId()
            });
            console.log(
                "this.section.data.testimonies before upadte:",
                this.section.data.testimonies
            );

            this.sectionCtrl.update(this.section);
            console.log(
                "this.section.data.testimonies before after:",
                this.section.data.testimonies
            );
        },

        removeTestimony(option) {
            this.section.data.testimonies.splice(options.index, 1);
            this.sectionCtrl.update(this.section);
        },

        previousSlide() {
            if (this.activeTestimony > 0) {
                this.activeTestimony--;
            } else {
                this.activeTestimony = this.section.data.testimonies.length - 1;
            }
            /* this.setTextTopPadding(); */
        },

        nextSlide() {
            if (
                this.activeTestimony <
                this.section.data.testimonies.length - 1
            ) {
                this.activeTestimony++;
            } else {
                this.activeTestimony = 0;
            }
            /* this.setTextTopPadding(); */
        },

        removeText(list, option) {
            /*  if (index !== -1) {
                list.splice(index, 1);
            } */
            list.splice(option.index, 1);
            this.sectionCtrl.update(this.section);
        },

        addNewText(list, option, t) {
            list.splice(option.index, 0, option.wwObject);
            //this.sectionCtrl.update(this.section); /FIXME: check this when marc saw what was the problem with the update current behavior text are added in the list splice but destroyed when we update the section
        },

        add(list, options) {
            list.splice(options.index, 0, options.wwObject);
            this.sectionCtrl.update(this.section);
        },

        remove(list, options) {
            /*  if (index !== -1) { */
            list.splice(options.index, 1);
            this.sectionCtrl.update(this.section);
        }
        /*         setTextTopPadding() {
            if ($(window).width() < 992) {
                for (var i = 0; i < $(".slide").length; i++) {
                    this.$element
                        .find($(".slide")[i])
                        .find(".testimony-text-content")
                        .css(
                            "margin-top",
                            $scope.$element
                                .find($(".slide")[i])
                                .find(".testimony-info-content")
                                .height() - 40
                        );
                }
            } else {
                $(".testimony-text-content").css("margin-top", 0);
            }
        }
 */
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

/* 
tmp button to add new testiomny
 */

.testimonial_B .add-testimony {
    background-color: #ffffff;
    color: #666666;
    padding: 6px 24px;
    position: relative;
    left: 47%;
    width: 170px;
    margin-bottom: 30px;
    margin-top: 30px;
    left: 50%;
    pointer-events: all;
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

/* -------------------------------------------------------------------------------- */

.testimonial_B .top-ww-objs,
.testimonial_B .bottom-ww-objs {
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
    pointer-events: all;
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

.testimonial_B .right-content-animation-start {
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

.testimonial_B .right-content-animation-end {
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
