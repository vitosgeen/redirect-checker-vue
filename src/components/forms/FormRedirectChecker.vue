<template>
    <form @submit.prevent="handleSubmit" class="check-redirect-form">
        <div class=" input-group ">
        <div class="col-auto">
            <div class="url-input-field form-floating">
            <input type="url" class="form-control redirect-input" placeholder="Url" id="url-input" v-model="urlInput" required />
            <label for="url-input" class="form-label">Url</label>
            <span>{{ urlInput }}</span>
            </div>
        </div>
        <div class="col-auto ">
            <input type="submit" id="send-input" value="Check" class="btn btn-primary btn-lg redirect-button" />
        </div>
        </div>           
    </form>
</template>

<script>
export default {
    name: 'FormTag',
    props: ["method", "action", "name", "event"],
    methods: {
        submit() {
            let myForm = this.$refs[this.$props.name];

            if (myForm.checkValidity()) {
                console.log("My event name", this.$props['event']);
                console.log("Name", this.$props.name);
                this.$emit(this.$props['event']);
            }
            myForm.classList.add("was-validated");
        }
    },
}
</script>