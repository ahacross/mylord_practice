<template>
  <div class="q-pa-md">
    <q-expansion-item
      v-for="({ label, list }, idx) in practiceList"
      :key="idx"
      group="practiceGroup"
      :label="label">
      <q-card>
        <q-card-section>
          <template v-for="(item, monthIdx) in list" :key="monthIdx">
            <div :class="{ highLight: highlightsDate === item.date }">
              <span style="margin-right: 5px">
                {{ item.date.split('.')[2] + '일' }} -
                <strong>{{ item.title }}</strong>
                {{ item.description }}
                <a v-if="item.down" :href="item.down">악보다운</a>
              </span>
              <br />
              <a
                v-for="(part, partIdx) in partList"
                :key="partIdx"
                :href="
                  item.type === 'youtube'
                    ? item.url[partIdx]
                    : item.url.split('mp').join(part.short)
                "
                target="_blank">
                {{ part.text }}
              </a>
            </div>
            <br />
            <br />
          </template>
        </q-card-section>
      </q-card>
    </q-expansion-item>

    <q-expansion-item group="practiceGroup" label="송영">
      <q-card>
        <q-card-section>
          <template v-for="(item, idx) in 송영" :key="idx">
            <span>
              <span style="margin-right: 5px">
                {{ item.description }} {{ item.title }}
              </span>
              <br />
              <a
                v-for="(part, partIdx) in partList.slice(1)"
                :key="partIdx"
                :href="item.url[partIdx]"
                target="_blank">
                {{ part.text }}
              </a>
            </span>
            <br />
            <br />
          </template>
        </q-card-section>
      </q-card>
    </q-expansion-item>
    <q-expansion-item group="practiceGroup" label="할렐루야">
      <q-card>
        <q-card-section>
          <span>
            <a
              v-for="(part, partIdx) in partList"
              :key="partIdx"
              :href="할렐루야[partIdx]"
              target="_blank">
              {{ part.text }}
            </a>
          </span>
        </q-card-section>
      </q-card>
    </q-expansion-item>
  </div>
</template>

<script>
import dayjs from 'dayjs'
export default {
  data() {
    return {
      isExpend: false,
      partList: [
        { text: '합창', short: 'mp' },
        { text: '소프라노', short: 'ss' },
        { text: '알토', short: 'aa' },
        { text: '테너', short: 'tt' },
        { text: '베이스', short: 'bb' }
      ],
      practiceList: [],
      송영: [],
      highlightsDate: '',
      할렐루야: []
    }
  },
  async mounted() {
    this.setHighLightDate()

    const res = await fetch(
      `/practiceLink/songList.json?t=${new Date().getTime()}`
    )
    this.practiceList = await res.json()

    const res2 = await fetch('/practiceLink/송영.json')
    this.송영 = await res2.json()
    this.할렐루야 = [
      'https://youtu.be/m-fS6VFaq10',
      'https://youtu.be/LR3mtuaEPh8',
      'https://youtu.be/gZdkV3BvNdg',
      'https://youtu.be/wnqvNTFnvz4',
      'https://youtu.be/jpeSNkIRo40'
    ]
  },
  methods: {
    setHighLightDate() {
      const today = dayjs()
      let date = null
      if (today.day()) {
        date = today.add(7 - today.day(), 'd')
      }
      this.highlightsDate = (date || today).format('YYYY.MM.DD')
    }
  }
}
</script>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}

a:link,
a:visited {
  color: #181818;
  padding: 3px 5px;
  margin: 5px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
}
a:hover,
a:active {
}

.highLight {
  background: coral;
}
</style>
