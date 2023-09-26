<template>
    <div class="w-100 mt-10">
        <div class="w-1/2 mx-auto text-center">
            <div class="py-2 bg-blue-600 text-white">
                <h1>My Calender</h1>

            </div>
            <div class="flex p-2 justify-between">
                <span>{{ dateInfo.monthName }}</span>
                <span>{{ dateInfo.fullYear }}</span>
            </div>
            <div class="grid grid-cols-7 gap-3 pt-3">
                <span class="p-2 border-res-100 w-full" v-for="day in days" :key="day">{{ day }}</span>
                <span class="p-2 border-res-100 w-full" v-for="dayNum in dateInfo.firstDayIndex" :key="dayNum" ></span>
                <span class="p-2 border-res-100 w-full" 
                v-for="dayNum in dateInfo.monthDaysCount" 
                :key="dayNum" 
                :class="(year == dateInfo.fullYear && month == dateInfo.month && dayNum == currentDay)?
                'bg-yellow-400 text-blue-950':'' "
                >{{ dayNum }}</span>
            </div>
            <div class="flex p-2 justify-between">
                <button @click="prev">Prev</button>
                <button @click="next">Next</button>
            </div>
        </div>
    </div>
</template>
<script>
    
export default {
  name: 'MyCalender',
  data () {
    let date = new Date()
    console.log(date)
    const he = new Intl.Locale("ar-EG");
    console.log(he);
    return {
        days: ['Sat','Sun','Mon','Tue','Wed','Thu','Fri'],
        date: date,
        month: date.getMonth(),
        year: date.getFullYear(),
        currentMonth: date.getMonth(),
        currentYear: date.getFullYear(),
        currentDay: date.getDate()
    }
  },
  computed:{
    dateInfo: function(){
        const date = new Date(this.currentYear,this.currentMonth+1,0)
        console.log([date.getDay(),date.getDate()],this.currentMonth)
        return {
            firstDayIndex:date.getDay(),
            monthDaysCount:date.getDate(0),
            month:date.getMonth(),
            fullYear:date.getFullYear(),
            monthName:date.toLocaleString("default",{month:'long'})
        }
    },
  },
  methods:{
    prev () {
        if(this.currentMonth == 0){
            this.currentYear--
            this.currentMonth = 11
        }else{
            this.currentMonth--
        }
    },
    next () {
        if(this.currentMonth == 11){
            this.currentYear++
            this.currentMonth = 0
        }else{
            this.currentMonth++
        }
    }
  }
}
</script>