<template>
  <div class="q-pa-md">
    <q-expansion-item
      v-for="({ label, list }, idx) in practiceList"
      :key="idx"
      :label="label">
      <q-card>
        <q-card-section>
          <template v-for="(item, monthIdx) in list" :key="monthIdx">
            <span>
              <span style="margin-right: 5px">
                {{ item.date }} - {{ item.title }} {{ item.description }}
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
            </span>
            <br />
            <br />
          </template>
        </q-card-section>
      </q-card>
    </q-expansion-item>
  </div>
</template>

<script>
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
      practiceList: [
        {
          label: '1월 성가곡 연습',
          list: [
            {
              date: '1일',
              title: '주님께 감사',
              description: '중앙성가 19 (p.74)',
              url: 'http://ad2007.iptime.org/Web/jaart/cor/19/1-1/u18_data10_mp.html'
            },
            {
              date: '8일',
              title: '오직 주만 따르오리',
              description: '중앙성가 19 (p.95)',
              url: 'http://ad2007.iptime.org/Web/jaart/cor/19/1-1/u18_data12_mp.html'
            },
            {
              date: '15일',
              title: '심령이 가난한 자는',
              description: '중앙성가 19 (p.142)',
              url: 'http://ad2007.iptime.org/Web/jaart/cor/19/1-1/u18_data17_mp.html'
            },
            {
              date: '22일',
              title: '내 진정 사모하는',
              description: '새찬송가 (88장)',
              type: 'youtube',
              url: [
                'https://m.youtube.com/watch?v=LwSFBLbnfhI',
                'https://m.youtube.com/watch?v=zYVFKnEPdUs',
                'https://m.youtube.com/watch?v=5t-1CNsnI0Q',
                'https://m.youtube.com/watch?v=lGrAt6hlTUQ',
                'https://m.youtube.com/watch?v=BT-skgAJX_o'
              ]
            },
            {
              date: '29일',
              title: '십자가를 질 수 있나',
              description: '중앙성가 19 (p.156)',
              url: 'http://ad2007.iptime.org/Web/jaart/cor/19/1-1/u18_data19_mp.html'
            }
          ]
        }
      ]
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
</style>
