<script setup>
import { reactive, ref } from "vue";
import {
  mdiBallotOutline,
  mdiAccount,
  mdiMail,
  mdiGithub,
  mdiCar,
  mdiCarInfo,
  mdiCarSearch,
} from "@mdi/js";
import SectionMain from "@/components/SectionMain.vue";
import CardBox from "@/components/CardBox.vue";
import FormCheckRadioGroup from "@/components/FormCheckRadioGroup.vue";
import FormFilePicker from "@/components/FormFilePicker.vue";
import FormField from "@/components/FormField.vue";
import FormControl from "@/components/FormControl.vue";
import BaseDivider from "@/components/BaseDivider.vue";
import BaseButton from "@/components/BaseButton.vue";
import BaseButtons from "@/components/BaseButtons.vue";
import SectionTitle from "@/components/SectionTitle.vue";
import LayoutAuthenticated from "@/layouts/LayoutAuthenticated.vue";
import SectionTitleLineWithButton from "@/components/SectionTitleLineWithButton.vue";
import NotificationBarInCard from "@/components/NotificationBarInCard.vue";
import Dropzone from "@/components/Dropzone.vue";

const selectOptions = [
  { id: 1, label: "Normal" },
  { id: 2, label: "Taller" },
  { id: 3, label: "Empresa" },
];

const form = reactive({
  name: "",
  email: "",
  phone: "",
  department: selectOptions[0],
  subject: "",
  question: "",
});

const customElementsForm = reactive({
  checkbox: ["lorem"],
  radio: "one",
  switch: ["one"],
  file: null,
});

const submit = () => {
  //
};

const formStatusWithHeader = ref(true);

const formStatusCurrent = ref(0);

const formStatusOptions = ["info", "success", "danger", "warning"];

const formStatusSubmit = () => {
  formStatusCurrent.value = formStatusOptions[formStatusCurrent.value + 1]
    ? formStatusCurrent.value + 1
    : 0;
};

const showImages = (e) => {
  console.log(customElementsForm.file);
};
</script>

<template>
  <LayoutAuthenticated>
    <SectionMain>
      <SectionTitleLineWithButton
        :icon="mdiBallotOutline"
        title="Datos del Cliente"
        main
      >
        <BaseButton
          href="https://github.com/justboil/admin-one-vue-tailwind"
          target="_blank"
          :icon="mdiGithub"
          label="Star on GitHub"
          color="contrast"
          rounded-full
          small
        />
      </SectionTitleLineWithButton>
      <CardBox is-form @submit.prevent="submit">
        <FormField label="Nombre y correo">
          <FormControl
            v-model="form.name"
            :icon="mdiAccount"
            placeholder="Nombre completo"
            required
          />
          <FormControl
            v-model="form.email"
            type="email"
            :icon="mdiMail"
            placeholder="correo@example.com"
          />
        </FormField>

        <FormField label="Telefono" help="Ingresa los 10 digitos.">
          <FormControl
            v-model="form.phone"
            type="tel"
            placeholder="Tu número de telefono"
            maxlength="10"
            minlength="10"
            required
          />
        </FormField>

        <FormField label="Tipo de Cliente">
          <FormControl v-model="form.department" :options="selectOptions" />
        </FormField>

        <FormField label="Observaciones" help="Maximo 255 characters">
          <FormControl type="textarea" placeholder="El clientes es..." />
        </FormField>

        <BaseDivider />

        <FormField label="Marca y modelo del vehiculo">
          <FormControl
            v-model="form.carName"
            :icon="mdiCar"
            placeholder="Ejemplo: Ford Mustang 2012 Azul"
            required
          />
        </FormField>

        <FormField
          label="Numero de Serie (VIN)"
          help="Ingresa los 17 digitos VIN"
        >
          <FormControl
            v-model="form.carVIN"
            :icon="mdiCarInfo"
            minlength="17"
            maxlength="17"
            placeholder="Ejemplo: 1FAHP3F29CL409616"
            required
          />
        </FormField>
        <FormField label="Placas">
          <FormControl
            v-model="form.carPlacas"
            :icon="mdiCarSearch"
            placeholder="XXX-XX-XXX"
            required
          />
        </FormField>

        <FormField label="Observaciones" help="Maximo 255 characters">
          <FormControl type="textarea" placeholder="La falla que tiene..." />
        </FormField>
        <FormFilePicker
          v-model="customElementsForm.file"
          multiple
          label="Subir Fotos"
          @upload-images="showImages"
        />

        <Dropzone />

        <template #footer>
          <BaseButtons>
            <BaseButton type="submit" color="info" label="Submit" />
            <BaseButton type="reset" color="info" outline label="Reset" />
          </BaseButtons>
        </template>
      </CardBox>
    </SectionMain>

    <SectionTitle>Custom elements</SectionTitle>

    <SectionMain>
      <CardBox>
        <FormField label="Checkbox">
          <FormCheckRadioGroup
            v-model="customElementsForm.checkbox"
            name="sample-checkbox"
            :options="{ lorem: 'Lorem', ipsum: 'Ipsum', dolore: 'Dolore' }"
          />
        </FormField>

        <BaseDivider />

        <FormField label="Radio">
          <FormCheckRadioGroup
            v-model="customElementsForm.radio"
            name="sample-radio"
            type="radio"
            :options="{ one: 'One', two: 'Two' }"
          />
        </FormField>

        <BaseDivider />

        <FormField label="Switch">
          <FormCheckRadioGroup
            v-model="customElementsForm.switch"
            name="sample-switch"
            type="switch"
            :options="{ one: 'One', two: 'Two' }"
          />
        </FormField>

        <BaseDivider />

        <FormFilePicker
          v-model="customElementsForm.file"
          label="Subir Fotos"
          images="true"
        />
      </CardBox>

      <SectionTitle>Form with status example</SectionTitle>

      <CardBox
        class="md:w-7/12 lg:w-5/12 xl:w-4/12 shadow-2xl md:mx-auto"
        is-form
        is-hoverable
        @submit.prevent="formStatusSubmit"
      >
        <NotificationBarInCard
          :color="formStatusOptions[formStatusCurrent]"
          :is-placed-with-header="formStatusWithHeader"
        >
          <span
            ><b class="capitalize">{{
              formStatusOptions[formStatusCurrent]
            }}</b>
            state</span
          >
        </NotificationBarInCard>
        <FormField label="Fields">
          <FormControl
            v-model="form.name"
            :icon-left="mdiAccount"
            help="Your full name"
            placeholder="Name"
          />
        </FormField>

        <template #footer>
          <BaseButton label="Trigger" type="submit" color="info" />
        </template>
      </CardBox>
    </SectionMain>
  </LayoutAuthenticated>
</template>
