<template>
  <div style="padding:5%">
    <div class="p-grid">
      <div class="p-col">
        <h2 style="color:#b5b5b7">STAY IN TOUCH</h2>
      </div>
      <div class="p-col" style="color:#b5b5b7">
        <p>Get CleanVid news delivered straight to your inbox.</p>
      </div>
    </div>
    <FormulateForm>
      <FormulateInput
        type="email"
        name="sample"
        placeholder="Email"
        validation="required|email"
        :wrapper-class="['my-wrapper-class']"
      />
    </FormulateForm>
  </div>
</template>
<script>
export default {
  data() {
    return {
      values: {},
      schema: [
        {
          component: "h3",
          children: "Student registration",
        },
        {
          label: "Your name",
          name: "name",
          validation: "required",
        },
        {
          label: "Your email",
          name: "email",
          help: "Please use your student email address",
          validation: "bail|required|email|ends_with:.edu",
          "validation-messages": {
            ends_with: "Please use a .edu email address",
          },
        },
        {
          type: "submit",
        },
      ],
    };
  },
};
</script>
<style>
.my-wrapper-class>div>input {
    background-color: #ffffff;
    height: 50px;
    width: 90%;
    border-radius: 20px;
    padding: 10px;
}
</style>