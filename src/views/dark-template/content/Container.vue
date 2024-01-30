<template>
  <v-card color="grey lighten-4" light>
    <v-card-text>
      <content-section title="Who am I?" class="font-weight-regular"
        >Knowledgeable Logician.
      </content-section>
      <content-section v-if="prouds.length" title="What am I proud of?">
        <v-layout v-for="(proud, i) in prouds" :key="i">
          <v-flex md1 xs3>
            <v-icon right>
              {{ proud.icon }}
            </v-icon>
          </v-flex>
          <v-flex md11 xs9>
            <p>
              <strong>{{ proud.text }}</strong
              ><br />
              <small>{{ proud.source }}</small>
            </p>
          </v-flex>
        </v-layout>
      </content-section>
      <content-section v-if="educations" title="Education">
        <v-layout v-for="(education, i) in educations" :key="i">
          <v-flex md4> {{ education.from }} - {{ education.to }} </v-flex>
          <v-flex md8>
            <strong v-if="education.title">{{ education.title }}</strong>
            <div v-if="education.location">
              <i>{{ education.location }}</i>
            </div>
            <div v-if="education.description">
              {{ education.description }}
            </div>
          </v-flex>
        </v-layout>
      </content-section>
      <content-section v-if="certificates" title="Certifications">
        <v-layout v-for="(certificates, i) in certificates" :key="i">
          <v-flex md4> {{ certificates.from }} - {{ certificates.to }} </v-flex>
          <v-flex md8>
            <strong v-if="certificates.title">{{ certificates.title }}</strong>
            <div v-if="certificates.location">
              <i>{{ certificates.location }}</i>
            </div>
            <div v-if="certificates.description">
              {{ certificates.description }}
            </div>
          </v-flex>
        </v-layout>
      </content-section>
      <content-section v-if="skills" id="to-timeline" title="Skills">
        <template slot="actions">
          (% are relative not absolute)
        </template>
        <v-layout wrap>
          <template v-for="(skill, i) in skills">
            <v-flex v-if="skill.divider" :key="i" md12 xs12 mb-4 />
            <v-flex v-else :key="i+1" md6 xs12>
              <div class="mr-2 ml-2">
                <div class="align-center">
                  <v-icon small>
                    {{ skill.icon }}
                  </v-icon>
                  {{ skill.title }}
                </div>
                <v-progress-linear
                  class="progress"
                  color="secondary"
                  height="3"
                  :value="skill.value"
                />
              </div>
            </v-flex>
          </template>
        </v-layout>
      </content-section>
    </v-card-text>
  </v-card>
</template>

<script>
import ContentSection from "@/views/dark-template/content/Section";
export default {
  name: "MainContent",
  components: { ContentSection },
  data: () => ({
    prouds: [],
    educations: [
      {
        from: "2020",
        to: "Currently Paused!",
        title: "Honours in Computing",
        location: "University of South Africa",
      },
      {
        from: "2010",
        to: "2017",
        title: "Bachelor of Science in Computer Science",
        location: "University of the Western Cape",
      },
      {
        from: "2007",
        to: "2009",
        title: "Matric",
        location: "Simanyene High School",
        description: "2007 started grade 10, and done grade 12 in 2009",
      },
    ],
    certificates: [
      {
        from: "2020-April",
        to: "2021-April",
        title: "Project Management",
        location: "Experian",
      },
      {
        from: "2019-Jan",
        to: "2020 - June",
        title: "Business Administration",
        location: "Experian",
      },
    ],
    skills: [
      {
        title: "Java",
        icon: "mdi-language-java",
        value: 75,
      },
      {
        title: "JavaScript",
        icon: "mdi-language-javascript",
        value: 80,
      },

      {
        title: "Vue.js Framework",
        icon: "mdi-vuejs",
        value: 90,
      },
      {
        title: "Windows OS",
        icon: "mdi-windows",
        value: 90,
      },
      {
        title: "DevOps",
        icon: "mdi-circle",
        value: 90,
      },
      {
        title: "Agile",
        icon: "mdi-circle",
        value: 90,
      },
      { divider: true },
      {
        title: "Ubuntu OS",
        icon: "mdi-ubuntu",
        value: 70,
      },
      {
        title: "TypeScript",
        icon: "mdi-language-typescript",
        value: 47,
      },
      {
        title: "Python",
        icon: "mdi-language-python",
        value: 50,
      },
      {
        title: "Node.js",
        icon: "mdi-nodejs",
        value: 60,
      },
      {
        title: "Express.js Framework",
        icon: "mdi-nodejs",
        value: 35,
      },
      {
        title: "Git",
        icon: "mdi-git",
        value: 67,
      },
      { divider: true },
      {
        title: "Vuetify Framework",
        icon: "mdi-vuejs",
        value: 70,
      },
      {
        title: "Analytics ",
        icon: "mdi-chart-bar",
        value: 70,
      },
      {
        title: "C",
        icon: "mdi-language-c",
        value: 38,
      },
      { divider: true },
      {
        title: "Postgresql",
        icon: "mdi-database",
        value: 68,
      },
      {
        title: "MySQL",
        icon: "mdi-database",
        value: 60,
      },
      {
        title: "MongoDB",
        icon: "mdi-database",
        value: 50,
      },
      {
        title: "Azure",
        icon: "mdi-cloud",
        value: 50,
      },
      {
        title: "Microsoft Power BI",
        icon: "mdi-chart-bar",
        value: 30,
      },
      {
        title: "Jira",
        icon: "mdi-jira",
        value: 50,
      },
    ],
  }),
};
</script>

<style scoped>
.title {
  border-bottom: 2px #bfbfbf solid;
  line-height: 1.5 !important;
}
.progress {
  margin-top: 0.1rem;
}
</style>
