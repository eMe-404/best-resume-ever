<template>
<div class="resume" id="template">
    <div id="resume-header">
        <div id="header-left">
            <h2 id="position">{{person.position}}</h2>
            <h2 id="name">{{person.name.first}} {{person.name.last}}</h2>
            <div id="info-flex">
                <span id="email"><a :href='"mailto:" + person.contact.email'>
                  <i class="fa fa-envelope" aria-hidden="true"></i> {{person.contact.email}}</a></span>
                <span id="phone"><i class='fa fa-phone-square' aria-hidden="true"></i> {{person.contact.phone}}</span>
                <span id="website"><a :href='person.contact.website'><i class="fa fa-home" aria-hidden="true"></i> {{person.contact.website}}</a></span>
                <span id="github"><a :href='"https://github.com/" + person.contact.github'><i class="fa fa-github" aria-hidden="true"></i> {{person.contact.github}}</a></span>
            </div>
        </div>
        <div id="header-right">
            <div id="headshot"></div>
        </div>
    </div>
    <div id="resume-body">
        <div id="experience-container">

            <h2 id="experience-title"><i class="fa fa-suitcase"></i> 实习经历 & 校园活动</h2>
            <div class="spacer"></div>
            <div class="experience" v-for="experience in person.experience">
              <div id="exStyle">
                <h2 class="company">{{experience.company}}</h2>
                <p class="job-info"><span class="job-title">{{experience.position}} | </span><span class="experience-timeperiod">{{experience.timeperiod}}</span></p>
              </div>
                <!--<p class="job-description" v-html="experience.description" v-if="experience.description">{{experience.description}}</p>-->
                <ul v-if="experience.list" >
                    <li v-for="item in experience.list"><span class="list-item-black">{{item}}</span></li>
                </ul>
            </div>
        </div>
        <div id="skills-container" v-if="person.skills != []">
        <h2 id="skills-title"><i class="fa fa-cogs"></i> 专业技能</h2>
        <div class="spacer"></div>

        <ul id="skill-list">
          <li class="skill" v-for="skill in person.skills"><span class="list-item-black">{{skill.name}}</span></li>
        </ul>
          <p id="skill-description">{{person.skillDescription}}</p>
      </div>
        <div id="education-container">
            <h2 id="education-title"><i class="fa fa-graduation-cap"></i> 教育背景</h2>
            <div class="spacer"></div>
            <div class="education" v-for="education in person.education">
              <h2><span class="degree">{{education.degree}} | </span><span class="education-timeperiod">{{education.timeperiod}}</span></h2>
                <p class="">{{education.description}}</p>

            </div>
        </div>

    </div>
    <div id="resume-footer">
        <div v-if="person.about">
            <h2><i id="aboutMeIcon" class="fa fa-thumbs-up"></i> 关于我</h2>
            <p v-html="person.about">{{person.about}}</p>
        </div>
    </div>
</div>
</template>

<script>
import Vue from 'vue';
import { getVueOptions } from './resumes';

export default Vue.component('purple', getVueOptions(name));
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="less" scoped>
@text-purple: #1f4e79;
#template {
    box-sizing:border-box;
    font-family:'Open Sans', sans-serif;
    h1, h2 {
        /*font-family:'Open Sans Condensed', sans-serif;*/
        margin:0;
        color: @text-purple;
    }

    p {
        margin:0;
        font-size:15px;
    }

    ul li {
        color:@text-purple;
        font-size:15px;
    }

    a {
        color:#FFF;
        text-decoration:none;
    }

    .list-item-black {
        color:black;
    }

    #resume-header {
        color: white;
        height: 136px;
        background-color: #1f4e79;
        box-shadow: inset 0px 0px 200px #301030;
        padding: 40px 100px 25px;
        display: flex;

        #header-left {
            /*width: 465px;*/
            width:100%;
            float: left;
            h1 {
                font-size:56px;
                color:white;
                text-transform:uppercase;
                line-height:56px;
            }
            h2 {
                font-size:22px;
                color:white;
            }
            #info-flex {
                display:flex;
                margin-top:20px;
                font-size:15px;
              flex-wrap: wrap;


                span {
                    /*margin-right:25px;*/
                    flex-basis: 50%;
                  margin-top: 10px;
                }
                i {
                    margin-right:5px;
                }
            }
        }

        #header-right {
          /*border: 1px solid red;*/
            width: 150px;
            float: right;
            margin: -29px -50px 0 0;
            box-sizing: border-box;
            height: 180px;
            background-color: #FFF;
            padding: 5px;
            #headshot {

                width: 100%;
                height: 100%;
                background:url('../assets/person.jpg');
                background-position:center;
                background-size:cover;
            }
        }
    }

    #resume-body {
        padding: 40px 100px;

        #experience-title, #education-title, #skills-title {
            font-size:26px;
            text-transform:uppercase;
        }

        .experience {
            margin: 10px 0 10px 50px;
            ul {
                margin: 5px 0 0 0;
            }
        }

        .company, .education-description {
            font-size:20px;
        }

        .job-info {
            margin-bottom:5px;
        }



        .job-title, .degree {
            font-weight:700;
            color: @text-purple;
            font-size:16px;
        }

        .experience-timeperiod, .education-timeperiod {
            font-weight:100;
            color: @text-purple;
            font-size:16px;
        }

        .education {
            margin: 10px 0 10px 50px;
        }

        #skill-list {
            column-count: 3;
            list-style-position: inside;
            ul li {
                font-size:14px;
            }
        }

        #education-container, #skills-container {
            margin-top: 20px;
            margin-bottom: 20px;
        }
    }
    #resume-footer {
        padding: 20px 100px;
        height: 135px;
        background-color: #1f4e79;
        box-shadow: inset 0px 0px 100px #301030;
        box-sizing: border-box;
        position: absolute;
        bottom: 0px;
        width: 100%;
        h2, p {
            color:white;
        }
    }

}

.spacer {
    width:100%;
    border-bottom:1px solid @text-purple;
    margin:5px 0 10px;

}
  .name{
    margin-top: 10px;
  }

  p{
    font-size: 15px;
  }

  #exStyle{
    display: flex;
    justify-content: space-between;
  }

  #experience-container{
    margin-bottom: 30px;
  }

  h2 i{
    color: black;
  }
  #aboutMeIcon{
    color: white;
  }
</style>
