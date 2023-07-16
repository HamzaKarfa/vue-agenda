<script setup lang="ts">
import { computed, onBeforeMount, onMounted, onUpdated, ref } from 'vue'
import moment from 'moment'
import Button from 'primevue/button'

let selectedDate: any = ref(moment())
let monthBefore: any = ref(moment().subtract(1, 'months'))
let monthAfter: any = ref(moment().add(1, 'months'))

onBeforeMount(() => {})

onMounted(() => {
  console.log('mounted')
  console.log(selectedDate)
})
onUpdated(() => {
  console.log('updated')
})

const events = {
  tasks: [
    {
      id: 1,
      date: '17/07/2023',
      'start-time': '09:00',
      'end-time': '10:00',
      title: 'Mobile app design',
      members: [
        {
          name: 'Mike',
          avatar_url: 'https://reqres.in/img/faces/3-image.jpg'
        },
        {
          name: 'Anita',
          avatar_url: 'https://reqres.in/img/faces/3-image.jpg'
        }
      ]
    },
    {
      id: 2,
      date: '16/07/2023',
      'start-time': '10:00',
      'end-time': '11:20',
      title: 'Software Testing',
      members: [
        {
          name: 'Anita',
          avatar_url: 'https://reqres.in/img/faces/3-image.jpg'
        },
        {
          name: 'David',
          avatar_url: 'https://reqres.in/img/faces/3-image.jpg'
        }
      ]
    }
  ]
}
</script>

<template class="calendar-component">
  <div class="flex flex-column flex-wrap align-items-center justify-content-between w-8 m-auto">
    <div class="flex align-items-center justify-content-between w-12">
      <Button
        text
        outlined
        class="flex align-items-center justify-content-center m-0 text-blue-500"
      >
        <span class="pi pi-angle-left m-0" style="font-size: 1.5rem"></span>
        <p class="mb-3">
          {{ monthBefore.format('MMMM') }}
        </p>
      </Button>
      <h2>{{ selectedDate.format('MMMM') }}</h2>
      <Button text class="flex align-items-center justify-content-center text-blue-500" outlined>
        <p class="mb-3">
          {{ monthAfter.format('MMMM') }}
        </p>
        <span class="pi pi-angle-right" style="font-size: 1.5rem"></span>
      </Button>
    </div>
    <div class="flex align-items-center justify-content-between w-12">
      <Button
        v-for="n in 7"
        text
        raised
        class="flex flex-column align-items-center justify-content-center py-4 m-4"
        :class="[n == 1 ? 'bg-blue-500 text-white' : 'surface-100 hover:surface-200 text-blue-500']"
        rounded
        @click="selectedDate = moment().add(n - 1, 'days')"
      >
        <h3 class="m-0 text-2xl">
          {{
            moment()
              .add(n - 1, 'days')
              .format('DD')
          }}
        </h3>
        <p class="m-0">
          {{
            moment()
              .add(n - 1, 'days')
              .format('ddd')
          }}
        </p>
      </Button>
    </div>

    <h1>OnGoing</h1>
    <!-- Todo Create hour agenda for selected day -->

    <div class="calendar w-12 h-5">
      <div class="timeline">
        <div class="time-marker">9 AM</div>
        <div class="time-marker">10 AM</div>
        <div class="time-marker">11 AM</div>
        <div class="time-marker">12 PM</div>
        <div class="time-marker">1 PM</div>
        <div class="time-marker">2 PM</div>
        <div class="time-marker">3 PM</div>
        <div class="time-marker">4 PM</div>
        <div class="time-marker">5 PM</div>
        <div class="time-marker">6 PM</div>
      </div>
      <div class="days">
        <div class="day mon">
         
          <div class="events">
            <div
              class="event start-9 end-5 securities px-4 py-2"
              v-for="event in events.tasks &&
              events.tasks.filter((event) => event.date == selectedDate.format('DD/MM/YYYY'))"
              :key="event.id"
              :class="
                ('start-' + event['start-time'].slice(0, 2), 'end-' + event['end-time'].slice(0, 2))
              "
            >
              <p class="text-xl m-0 font-semibold	">Securities Regulation</p>
              <p class="m-0 font-light">
                <span v-for="(member, index) in event.members" :key="member.name">
                  {{ member.name }}
                  <span v-if="index < event.members.length - 1">and </span>
                </span>
              </p>
              <div class="flex justify-content-between align-items-center my-3 w-auto">
                <div class="img-member">
                  <img
                    v-for="member in event.members"
                    :key="member.name"
                    :src="member.avatar_url"
                    alt="avatar"
                    class="w-2rem border-circle border-3 border-white border-solid"
                  />
                </div>
                <p class="m-0">
                  {{ event['start-time'] }} - {{ event['end-time'] }}
                </p>

              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">
$numHours: 10;
$timeHeight: 60px;
$calBgColor: #fff1f800;
$eventColor: #043ddbd9;

.calendar {
  display: grid;
  gap: 10px;
  grid-template-columns: auto 1fr;
  margin: 2rem;
}

.timeline {
  display: grid;
  grid-template-rows: repeat($numHours, $timeHeight);
}

.days {
  display: grid;
  grid-column: 2;
  gap: 5px;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
}

.events {
  display: grid;
  grid-template-rows: repeat($numHours, $timeHeight);
  border-radius: 5px;
  background: $calBgColor;
}

// Place on Timeline
.start-9 {
  grid-row-start: 1;
}
.start-10 {
  grid-row-start: 2;
}

.start-12 {
  grid-row-start: 4;
}

.start-1 {
  grid-row-start: 5;
}

.start-2 {
  grid-row-start: 6;
}

.start-3 {
  grid-row-start: 7;
}

.start-4 {
  grid-row-start: 8;
}

.start-5 {
  grid-row-start: 9;
}

.end-12 {
  grid-row-end: 4;
}

.end-1 {
  grid-row-end: 5;
}
.end-2 {
  grid-row-end: 6;
}

.end-3 {
  grid-row-end: 7;
}

.end-4 {
  grid-row-end: 8;
}

.end-5 {
  grid-row-end: 9;
}

.title {
  font-weight: 600;
  margin-bottom: 0.25rem;
}

.event {
  border-radius: 15px;
  padding: 1rem;
  margin: 0 1.5rem;
  color: #fff;
}

.space,
.date {
  height: 60px;
}
.corp-fi {
  background: $eventColor;
}

.ent-law {
  background: $eventColor;
}

.writing {
  background: $eventColor;
}

.securities {
  background: $eventColor;
}

.date {
  display: flex;
  gap: 1em;
}

.date-num {
  font-size: 3rem;
  font-weight: 600;
  display: inline;
}

.date-day {
  display: inline;
  font-size: 3rem;
  font-weight: 100;
}

.img-member img { 
  @for $i from 1 through 4 { 
    &:nth-child(#{$i}) { 
      position: relative;
      left: calc(-7px*$i); 
    }
  }
}
</style>
