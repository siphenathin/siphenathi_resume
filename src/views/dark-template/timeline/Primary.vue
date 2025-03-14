<template>
  <v-card
    color="grey lighten-4"
    light
  >
    <v-card-text>
      <content-section
        id="timeline"
        :title="detailed ? 'My Experience' : 'My Life in a Nutshell'"
      >
        <template slot="actions">
          <div>
            <v-switch
              v-model="detailed"
              :label="detailed ? 'Detailed' : 'Summary'"
            />
          </div>
        </template>

        <v-timeline
          dense
        >
          <v-timeline-item
            v-for="(item, i) in orderedItems"
            :key="i"
            :icon="item.icon || ''"
            :class="{transparent: item.transparent}"
            large
          >
            <template
              v-if="item.iconImage"
              v-slot:icon
            >
              <v-avatar>
                <img
                  :src="publicPath(item.iconImage)"
                >
              </v-avatar>
            </template>
            <template v-slot:opposite />
            <v-layout>
              <v-flex
                v-if="$vuetify.breakpoint.smAndUp"
                md1
                sm2
                align-self-center
              >
                <span>{{ item.year }}</span>
              </v-flex>
              <v-flex
                md11
                sm10
                xs12
              >
                <v-card class="elevation-1">
                  <v-card-title class="pb-0">
                    <div>
                      <p v-if="$vuetify.breakpoint.xsOnly">
                        {{ item.year }}
                      </p>
                      <h3>{{ item.title }}</h3>
                    </div>
                  </v-card-title>
                  <v-card-text>
                    <v-layout wrap>
                      <v-flex
                        :md7="!!item.image"
                        :md12="!item.image"
                        xs12
                      >
                        <div class="mr-1">
                          <span
                            v-if="item.text"
                            class="pre"
                          >{{ item.text }}</span>
                          <!-- eslint-disable vue/no-v-html -->
                          <div
                            v-else-if="item.html"
                            v-html="item.html"
                          />
                          <!-- eslint-enable vue/no-v-html -->
                        </div>
                      </v-flex>
                      <v-flex
                        v-if="item.image"
                        md5
                        xs12
                      >
                        <div
                          class="mt-2"
                        >
                          <v-carousel
                            v-if="Array.isArray(item.image)"
                            :show-arrows="false"
                            :height="325"
                          >
                            <v-carousel-item
                              v-for="(citem,ci) in item.image"
                              :key="ci"
                              :src="publicPath(citem)"
                            />
                          </v-carousel>
                          <v-img
                            v-else
                            :max-height="item.imageHeight ? item.imageHeight : ''"
                            :src="publicPath(item.image)"
                          />
                        </div>
                      </v-flex>
                    </v-layout>
                  </v-card-text>
                </v-card>
              </v-flex>
            </v-layout>
          </v-timeline-item>
        </v-timeline>
      </content-section>
    </v-card-text>
  </v-card>
</template>

<script>
import ContentSection from '@/views/dark-template/content/Section'
export default {
  name      : 'Timeline',
  components: { ContentSection },
  data      : () => ({
    detailed: true,
    items   : [
      {
        year : '2018-2019',
        title: 'Worked as a Business Analyst trainee at Bytes Peoples Solutions',
        html : `Skilled in the following:
                <li>Analyse a business scenario.</li>
                <li>Develop a business case.</li>
                <li>Compile user requirement specifications.</li>
                <li>Develop functional specifications.</li>
              <li>Monitor quality assurance activities throughout the life cycle of the project</li>
                  `,

        iconImage: 'img/timeline/analysis_1.png',
      },
      {
        year : '2019-2021',
        title: 'Worked as a Junior Software Developer at Experian',
        html : `Doing the following but not limited:
                <li>Assisting the Development Manager with all aspects of software design and coding.</li>
                <li> Learning and improving my coding skills. </li>
                <li> Writing and maintaining code. </li>
                <li> Working on minor bug fixes. </li>
              <li> Monitoring the technical performance of internal systems. </li>
              <li>Responding to requests from the development team. </li>
              <li> Gathering information from consumers about program functionality. </li>
              <li> Writing reports. </li>
                 <li> Conducting development tests. </li>
                  `,

        iconImage: 'img/timeline/icon-dev_1.png',
      },
      {
        year : '2022-Present',
        title: 'Working as System Analyst at Capitec Banks',
        html : `As a System Analyst/System Support Analyst at Capitec Bank, my role revolves around monitoring, troubleshooting, and optimizing IT systems to ensure seamless banking operations.
          <li> A key aspect of my job involves working with Splunk, where I analyze logs, generate reports, and set up alerts to proactively identify and resolve system issues.</li>
          <li> My daily tasks include: </li>

          <li> System Monitoring & Troubleshooting: Using Splunk and other tools to track system performance, investigate errors, and resolve incidents. </li>
          <li> Log Analysis & Reporting: Extracting insights from system logs to enhance operational efficiency and detect potential risks. </li>
          <li> Incident Management: Collaborating with different teams to resolve technical issues, ensuring minimal downtime and business continuity. </li>
          <li> Automation & Optimization: Developing dashboards, alerts, and automated reports to improve system monitoring and issue detection. </li>
          <li> Support & Communication: Assisting internal teams with system-related queries and ensuring that IT infrastructure aligns with business needs. </li>
          <li> Overall, my role is crucial in maintaining the stability, security, and performance of Capitec Bank’s IT systems, ensuring a smooth banking experience for customers. </li>
                  `,

        iconImage: 'img/timeline/icon-dev_1.png',
      },
    ],
  }),
  computed: {
    orderedItems () {
      const items = [...this.items].reverse()
      if (this.detailed)
        return items
      return items.filter((item) => {
        return !item.detailed
      })
    },
  },
}
</script>

<style scoped>
.title {
  border-bottom: 2px #bfbfbf solid;
  line-height: 1.5 !important;
}
.pre {
  white-space: pre;
}
.transparent{
  opacity: 0.6;
}
</style>
