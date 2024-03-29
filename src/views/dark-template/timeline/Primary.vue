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
        html : `Doing the following but not limited:
                <li>Analyzing and evaluating current systems. </li>
              <li> Identifying new system requirements. </li>
              <li>Suggesting solutions for process improvement. </li>
              <li> Communicating with users to understand their additional requirements and needs. </li>
              <li> Working with IT team and developers to produce new and improve existing systems. </li>
                 <li> Designing and testing standards and solutions to help the organization operate more efficiently and effectively </li>
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
