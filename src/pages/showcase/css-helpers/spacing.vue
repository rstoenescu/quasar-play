<template>
  <q-page padding>
    <p class="caption text-left">Padding and Margin utility classes</p>

    <div class="margin-div bg-orange-2 q-my-md" style="padding: 0.1px">
      <div class="padding-div bg-green-2" :class="allHelperClasses">
        <div class="content-div bg-blue-3 q-pa-md text-center">
          class="{{ allHelperClasses }}"
        </div>
      </div>
    </div>
    <div class="row items-center" v-for="(h, index) in helpers" :key="index">
      <q-select v-model="h.mode" :options="options.mode" stack-label="Mode" class="col"/>
      <q-select v-model="h.direction" :options="options.direction" stack-label="Direction" class="col"/>
      <q-select v-model="h.size" :options="options.size" stack-label="Size" class="col"/>
      <q-input :value="helperClass(h)" readonly stack-label="Result" class="col gt-xs"/>
      <q-btn @click="helpers.splice(index, 1)" size="md" round flat dense icon="cancel" color="negative"/>
      <hr>
    </div>
    <div class="row justify-end">
      <q-btn @click="helpers.push({mode: helpers.length % 2 === 0 ? 'p' : 'm', direction: 'a', size: 'md'})" icon="add" size="md" color="positive" round dense/>
    </div>
  </q-page>
</template>

<script>
export default {
  data () {
    return {
      options: {
        mode: [
          {
            label: 'Padding',
            value: 'p'
          },
          {
            label: 'Margin',
            value: 'm'
          }
        ],
        direction: [
          {
            label: 'All',
            value: 'a'
          },
          {
            label: 'Y-Axis',
            value: 'y'
          },
          {
            label: 'X-Axis',
            value: 'x'
          },
          {
            label: 'Top',
            value: 't'
          },
          {
            label: 'Right',
            value: 'r'
          },
          {
            label: 'Bottom',
            value: 'b'
          },
          {
            label: 'Left',
            value: 'l'
          }
        ],
        size: [
          {
            label: 'Extra Small',
            value: 'xs'
          },
          {
            label: 'Small',
            value: 'sm'
          },
          {
            label: 'Medium',
            value: 'md'
          },
          {
            label: 'Large',
            value: 'lg'
          },
          {
            label: 'Extra Large',
            value: 'xl'
          }
        ]
      },
      helpers: [
        {
          mode: 'p',
          direction: 'a',
          size: 'md'
        },
        {
          mode: 'm',
          direction: 'a',
          size: 'md'
        }
      ]
    }
  },
  computed: {
    allHelperClasses () {
      return this.helpers.map(opt => this.helperClass(opt)).join(' ')
    }
  },
  methods: {
    helperClass (opt) {
      return `q-${opt.mode}${opt.direction}-${opt.size}`
    }
  }
}
</script>

<style lang="stylus" scoped>
@import '~variables'

.margin-div,
.padding-div,
.content-div
  position relative

  &:before
    position absolute
    top 0
    left 2px
    color #fff

.padding-div:before
  content "padding"

.margin-div:before
  content "margin"

.content-div:before
  content "content"

</style>
