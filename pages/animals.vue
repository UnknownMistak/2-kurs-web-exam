<template>
  <v-row>
    <v-col cols="12">
      <form @submit.prevent="submit">
        <v-col cols="12" v-for="(field, key) in form" :key="key">
          <v-text-field
            v-if="field.type === 'string'"
            v-model="formAns[key]"
            :label="field.title"
            required
          ></v-text-field>
          <v-select
            v-if="field.type === 'select'"
            v-model="formAns[key]"
            :items="field.values"
            :label="field.title"
            required
          ></v-select>
        </v-col>
        <button class="mr-4 btn">Отправить</button>
      </form>
    </v-col>
    <v-col cols="6" v-for="animal in animals" :key="animal.id">
      <card :data="animal"></card>
    </v-col>
  </v-row>
</template>

<script>
export default {
  data: () => ({
    form: {},
    formAns: {},
    animals: [],
  }),
  methods: {
    submit() {
      this.$axios.post("https://demo-api.vsdev.space/api/farm/baby", {});
      
    },
  },
  async mounted() {
    let { data } = await this.$axios.get(
      `https://demo-api.vsdev.space/api/farm/baby/form`
    );
    this.form = data.fields;
    const anim = await this.$axios.get(
      `https://demo-api.vsdev.space/api/farm/baby`
    );
    this.animals = anim.data;
  },
};
</script>
