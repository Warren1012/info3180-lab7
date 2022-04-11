<template>
<form id="upload" name="upload" method="POST" enctype="multipart/form-data" @submit.prevent="uploadPhoto">
    <div class="form-group">
        {{ form.description.label }}
    </div>

    <div class="form-group">
        {{ form.image.label }}
    </div>
    <button type="submit" name="submit" class="btn">Sumbit</button>
</form>
<p>HI </p>
</template>

<script>
    export default {
    data() {
        return {
           csrf_token: ''
        }
    },
    uploadPhoto()
    {
        let uploadForm = document.getElementById('uploadForm');
        let form_data = new FormData(uploadForm);
        fetch("/api/upload", {
            method: 'POST',
            body: form_data,
            headers: {
                'X-CSRFToken': this.csrf_token
                }
        })
        .then(function (response) {
            return response.json();
        })
        .then(function (data) {
         // display a success message
        console.log(data);
        })
        .catch(function (error) {
        console.log(error);
        });
    },
    getCsrfToken() {
        let self = this;
        fetch('/api/csrf-token')
        .then((response) => response.json())
        .then((data) => {
        console.log(data);
        self.csrf_token = data.csrf_token;
    })
 },
 created() {
 this.getCsrfToken();
},
}
</script>