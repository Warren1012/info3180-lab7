<template>
<form id="upload" name="upload" method="POST" enctype="multipart/form-data" @submit.prevent="uploadPhoto">
    <div class="form-group">
        {{ form.description.label }}
        {{ form.description(class='form-control') }}
    </div>

    <div class="form-group">
        {{ form.image.label }}
        {{ form.image(class="form-control")}}
    </div>
    <button type="submit" name="submit" class="btn">Sumbit</button>
</form>
<p>HI </p>
</template>

<script>
    export default {
    data() {
        return {
            message: "Form"
        };
    },
    uploadPhoto()
    {
        fetch("/api/upload", {
            method: 'POST'
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
}
</script>