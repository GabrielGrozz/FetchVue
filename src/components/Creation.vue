<template>
    <div class="creation-container">
        <div class="creation">
            <form action="" class="form">
                <label class="label" for="name">Nome</label>
                <input type="text" name="name" id="name">

                <label class="label" for="content">Conteudo</label>
                <textarea name="content" id="content"></textarea>

                <button class="saveContent" type="submit">Salvar</button>

            </form>
        </div>
    </div>
</template>

<script setup>

</script>

<style scoped>
.creation-container {
    display: flex;
    justify-content: center;
    align-items: center;
}

.creation {
    position: absolute;
    height: 300px;
    width: 400px;
    top: 20%;
    background: purple;
    padding: 10px;

}

.form {
    display: flex;
    flex-direction: column;
    align-items: center;
}

label {
    margin: 5px 0;
}

#name {
    margin-bottom: 20px;
}

#content {
    position: relative;
    resize: none;
    width: 90%;
    height: 150px;
}
</style>