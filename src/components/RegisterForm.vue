<template>
  <div id="register-form" class="container">
    <v-container>
      <v-row>
        <v-col class="align-center justify-center layout text-center">
          <!-- avatar -->
          <img :src="url" height="150" v-if="url" alt="avatar" />
        </v-col>
        <v-col class="align-center justify-center layout text-center">
          <v-file-input
            :rules="rules"
            accept="image/png, image/jpeg, image/bmp"
            placeholder="Upload profile image"
            prepend-icon="mdi-camera"
            label="Profile image"
            ref="image"
            @change="previewImg($event); prepareFile($event)"
          ></v-file-input>
        </v-col>
      </v-row>
      <v-form>
        <v-stepper v-model="e6" vertical>
          <v-stepper-step :complete="e6 > 1" step="1">Personal Details</v-stepper-step>

          <v-stepper-content step="1">
            <v-card class="mb-12" height="auto">
              <v-text-field v-model="form.persData.firstName" label="First Name" required></v-text-field>
              <v-text-field v-model="form.persData.lastName" label="Last Name" required></v-text-field>
              <v-select v-model="form.persData.gender" label="Gender" :items="genders"></v-select>
              <v-text-field
                v-model="form.persData.email"
                label="Email"
                :rules="emailRules"
                type="email"
                required
              ></v-text-field>
              <v-text-field v-model="form.persData.pwd" label="Password" type="password" required></v-text-field>
              <v-text-field
                v-model="form.persData.confirmPwd"
                label="Confirm Password"
                type="password"
                required
              ></v-text-field>
            </v-card>
            <v-btn color="primary" @click="e6 = 2">Continue</v-btn>
            <v-btn text>Cancel</v-btn>
          </v-stepper-content>

          <v-stepper-step :complete="e6 > 2" step="2">Contact details</v-stepper-step>

          <v-stepper-content step="2">
            <v-card class="mb-12" height="auto">
              <v-textarea v-model="form.contactData.about" label="About"></v-textarea>
              <v-text-field v-model="form.contactData.practice" label="Practice" required></v-text-field>
              <v-textarea
                v-model="form.contactData.practiceAddress"
                label="Practice Address"
                required
              ></v-textarea>
              <v-text-field v-model="form.contactData.apt_ste" label="Apt/Ste" required></v-text-field>
              <v-text-field v-model="form.contactData.phone" label="Phone Number" required></v-text-field>
            </v-card>
            <v-btn color="primary" @click="e6 = 3">Continue</v-btn>
            <v-btn text>Cancel</v-btn>
          </v-stepper-content>

          <v-stepper-step :complete="e6 > 3" step="3">Medical details</v-stepper-step>

          <v-stepper-content step="3">
            <v-card class="mb-12" height="auto">
              <v-text-field v-model="form.medicalData.license" label="License"></v-text-field>
              <v-text-field v-model="form.medicalData.specialization" label="Specialization"></v-text-field>
              <v-text-field
                v-model="form.medicalData.additional_specialties"
                label="Additional Specialties"
              ></v-text-field>
              <v-checkbox
                v-model="form.medicalData.primaryCarePhysician"
                label="Primary Care Physician"
              ></v-checkbox>
              <v-checkbox v-model="form.medicalData.abmsCertification" label="ABMS Certification"></v-checkbox>
            </v-card>
            <v-btn color="primary" @click="e6 = 4">Continue</v-btn>
            <v-btn text>Cancel</v-btn>
          </v-stepper-content>

          <v-stepper-step step="4">Terms & conditions</v-stepper-step>
          <v-stepper-content step="4">
            <v-card color="grey lighten-1" class="mb-12" height="200px"></v-card>
            <v-btn color="primary" @click="e6 = 1">Continue</v-btn>
            <v-btn text>Cancel</v-btn>
          </v-stepper-content>
        </v-stepper>
      </v-form>
    </v-container>
  </div>
</template>
<script>
export default {
  data: () => ({
    form: {
      persData: {
        firstName: "",
        lastName: "",
        gender: "",
        email: "",
        pwd: "",
        confirmPwd: ""
      },
      contactData: {
        about: "",
        practice: "",
        practiceAddress: "",
        apt_ste: "",
        phone: ""
      },
      medicalData: {
        license: "",
        specialization: "",
        additional_specialties: "",
        primaryCarePhysician: false,
        abmsCertification: false
      }
    },
    genders: ["Male", "Female"],
    emailRules: [
      v => !!v || "E-mail is required",
      v => /.+@.+\..+/.test(v) || "E-mail must be valid"
    ],
    e6: 1,
    url: "",
    avatar: "",
    rules: [
      value =>
        !value || value.size < 5000000 || "Image size should be less than 5 MB!"
    ]
  }),
  methods: {
    prepareFile(e) {
      let fileList = e.target.files;
      this.avatar = fileList[0];
    },
    previewImg(e) {
      const file = e.target.files[0];
      this.url = URL.createObjectURL(file);
    }
  }
};
</script>
<style lang="scss">
#register-form {
  // border: 2px solid rgb(207, 203, 203);
  // border-radius: 20px;
  background: #fff;
  margin: 20px auto;
}
</style>
