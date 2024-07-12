<template>
  <v-container>
    <v-row
      justify="center"
      class="mt-4">
      <v-col
        cols="10"
        sm="10"
        md="10"
        lg="10"
      >
        <v-row style="justify-content: space-between">
          <v-col cols="6">
            <h1>Список отчетов</h1>
          </v-col>
          <v-col cols="6" style="text-align-last: end">
            <v-btn @click="goToCreateReport">
              <span>Создать</span>
            </v-btn>
          </v-col>
        </v-row>
        <v-row>
          <v-col cols="12">
            <v-data-table
              :headers="headers"
              :items="test"
            >
            </v-data-table>
          </v-col>
        </v-row>
      </v-col>
    </v-row>
  </v-container>
</template>

<script scope>
export default {
  data () {
    return {
      headers: [
        {
          text: '',
          align: 'start',
          sortable: false,
          value: 'empty',
        },


        {text: 'id', value: 'id'},
        {text: 'Наименование подразделения', value: 'department_name'},
        {text: 'Краткое описание обнаружения', value: 'brief_description'},
        {text: 'Рекоменлации подраздлеления внутреннего аудита', value: 'reccomendations'},
        {text: 'Мероприятие по исполнению рекомендации подразделения внутреннего аудита', value: 'action_to_implement_the_recommendation'},
        {text: 'Форма завершения', value: 'form_of_completion'},
        {text: 'Срок исполнения', value: 'date' },
        {text: 'Выполнено', value: 'completed' },
        {text: 'Выполнено не в установленный срок', value: 'expired' },
        {text: 'Не выполнено', value: 'not_done' },
        {text: 'Снято с контроля', value: 'removed_from_control' },
        {text: 'Перенесено', value: 'rescheduled' },


      ],
      test:[],
    }
  },
  methods:{
    goToCreateReport(){
       this.$router.push('/create_report')

    },
    async fetch(){
      const response = await this.$axios.$get('http://127.0.0.1:8000/audit/api/reports/')
      console.log(response)
      this.test = response
    }
  },

  mounted() {
    this.fetch();
  }


}
</script>

<style scoped>

</style>
