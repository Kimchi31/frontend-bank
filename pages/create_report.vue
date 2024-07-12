<template>
  <v-container>
    <v-row justify="center" class="mt-4">
      <v-col cols="10" sm="10" md="10" lg="10">
        <v-row>
          <v-col cols="12">
            <h1>Создание отчета</h1>
          </v-col>
        </v-row>
        <v-row>
          <v-col cols="12">
            <v-row>
              <v-col cols="12">
                <v-select
                  v-model="department"

                  :items="items"
                  item-text="name"
                  item-value="code"
                  label="Наименование подразделения"
                ></v-select>
              </v-col>

              <v-col cols="12">
                <v-text-field
                  label="Краткое описание обнаружения"
                  v-model="brief_description"
                  placeholder="описание"
                ></v-text-field>
              </v-col>

              <v-col cols="12">
                <v-text-field
                  label="Рекомендация подразделения внутреннего аудита"
                  v-model="reccomendations"
                  placeholder="рекомендация"
                ></v-text-field>
              </v-col>

              <v-col cols="12">
                <v-text-field
                  label="Мероприятие по исполнению рекомендации подразделения внутреннего аудита"
                  v-model="action_to_implement_the_recommendation"
                  placeholder="рекомендации по исполнению"
                ></v-text-field>
              </v-col>

              <v-col cols="12">
                <v-text-field
                  label="Форма завершения"
                  v-model="form_of_completion"
                  placeholder="форма завершения"
                ></v-text-field>
              </v-col>

              <v-col cols="12">
                <v-menu
                  ref="menu"
                  v-model="menu"
                  :close-on-content-click="false"
                  :return-value.sync="date"
                  transition="scale-transition"
                  offset-y
                  min-width="auto"
                >
                  <template v-slot:activator="{ on, attrs }">
                    <v-text-field
                      v-model="date"
                      label="Срок Исполнения"
                      prepend-icon="mdi-calendar"
                      readonly
                      v-bind="attrs"
                      v-on="on"
                    ></v-text-field>
                  </template>
                  <v-date-picker v-model="date" no-title scrollable>
                    <v-spacer></v-spacer>
                    <v-btn text color="primary" @click="menu = false">
                      Cancel
                    </v-btn>
                    <v-btn text color="primary" @click="$refs.menu.save(date)">
                      OK
                    </v-btn>
                  </v-date-picker>
                </v-menu>
              </v-col>

              <v-col cols="12" style="display: flex">
                <v-checkbox
                  label="Выполнено"
                  v-model="completed"
                  style="margin-right: 30px"
                ></v-checkbox>
                <v-checkbox
                  label="Выполнено не в установленный срок"
                  v-model="expired"
                  style="margin-right: 30px"
                ></v-checkbox>
              </v-col>
              <v-col cols="12" style="display: flex">
                <v-checkbox
                  label="Не выполнено"
                  v-model="not_done"
                  style="margin-right: 30px"
                ></v-checkbox>
                <v-checkbox
                  label="Снято с контроля"
                  v-model="removed_from_control"
                  style="margin-right: 30px"
                ></v-checkbox>
                <v-checkbox
                  label="Перенесено"
                  v-model="rescheduled"
                  style="margin-right: 30px"
                ></v-checkbox>
              </v-col>

              <v-file-input
                show-size
                counter
                multiple
                label="File input"
                v-model="file"
              ></v-file-input>

              <v-col cols="12">
                <v-btn @click="send">Отправить</v-btn>
              </v-col>
            </v-row>
          </v-col>
        </v-row>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      items: [
        { name: 'Департамент Банковского Регулирования', code: 1 },
        { name: 'Департамент Рынка Ценных Бумаг', code: 2 },
        { name: 'Департамент Защиты Прав Потребителей Финансовых Услуг', code: 3 },
        { name: 'Департамент Стратегии и Анализа', code: 4 },
        { name: 'Юридический Департамент', code: 5 },
        { name: 'Департамент Развития Человеческого Капитала', code: 6 },
        { name: 'Департамент Информационных Технологий', code: 7 },
        { name: 'Департамент Международного Сотрудничества', code: 8 },
        { name: 'Департамент Регулирования Небанковских Организаций', code: 9 },
        { name: 'Управление Внешних Коммуникаций', code: 10 },
        { name: 'Управление Службы Председателя Агентства', code: 11 },
        { name: 'Управление Внутреннего Аудита', code: 12 },
        { name: 'Управление по Защите Государственных Секретов и Мобилизационной Работе', code: 13 },
        { name: 'Управление Учета и Планирования', code: 14 },
        { name: 'Управление Надзорных Технологий', code: 16 }
      ],
      menu: false,
      date: (new Date(Date.now() - new Date().getTimezoneOffset() * 60000))
        .toISOString()
        .substr(0, 10),

      // Поля
      department: null,
      brief_description: '',
      reccomendations: '',
      action_to_implement_the_recommendation: '',
      form_of_completion: '',
      completed: false,
      expired: false,
      not_done: false,
      removed_from_control: false,
      rescheduled: false,
      file: null,
    };
  },
  methods: {
    async send() {
      // this.formData = new FormData();
      // this.formData.append('department', this.department);
      // this.formData.append('description', this.description);
      // this.formData.append('recommendations', this.recommendations);
      // this.formData.append('action_to_implement_the_recommendation', this.action_to_implement_the_recommendation);
      // this.formData.append('form_of_completion', this.form_of_completion);
      // this.formData.append('deadline', this.date);
      // this.formData.append('completed', this.completed ? 'true' : 'false');
      // this.formData.append('expired', this.expired ? 'true' : 'false');
      // this.formData.append('not_done', this.not_done ? 'true' : 'false');
      // this.formData.append('removed_from_control', this.removed_from_control ? 'true' : 'false');
      // this.formData.append('rescheduled', this.rescheduled ? 'true' : 'false');

      const formData = {
        department: this.department,
        brief_description: this.brief_description,
        reccomendations: this.reccomendations,
        action_to_implement_the_recommendation: this.action_to_implement_the_recommendation,
        form_of_completion: this.form_of_completion,
        deadline: this.date,
        completed: this.completed,
        expired: this.expired,
        not_done: this.not_done,
        removed_from_control: this.removed_from_control,
        rescheduled: this.rescheduled,
        // file: this.file[0]
      }
      console.log('-----------')
      console.log(formData)
      console.log(this.file)

      try {
        // Отправка данных
        const response = await this.$axios.post('http://localhost:8000/audit/create-reports/', formData)
        console.log('Success:', response);
      } catch (error) {
        console.error('Error:', error);
      }
    }
  }
};
</script>

<style scoped>
</style>
