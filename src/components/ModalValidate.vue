<template>
    <modal 
        title="Оставить заявку"
        @close="$emit('close')">
        <div slot="body"> 
            <form @submit.prevent="onSubmit">
            <div class="form-item" :class="{ errorInput: $v.name.$error }">
                <label>Имя:</label>
                <p class="errorText" v-if="!$v.name.required"> Поле не может быть пустым!  </p>
                <p class="errorText" v-if="!$v.name.minLenght"> Количество символов должно быть больше {{$v.name.$params.minLenght.min}}! </p>
                <input 
                    v-model="name" 
                    :class="{ error: $v.name.$error }" 
                    @change="$v.name.$touch()">
            </div>
            <div class="form-item" :class="{ errorInput: $v.email.$error }">
                <label>Email:</label>
                <p class="errorText" v-if="!$v.email.required"> Поле не может быть пустым!  </p>
                <p class="errorText" v-if="!$v.email.email"> Email должен содержать "@" и "." и иметь 2 символа после точки </p>
                <input 
                    v-model="email" 
                    :class="{ error: $v.email.$error }" 
                    @change="$v.email.$touch()">
            </div>

            <button class="btn btnPrimary">Отправить</button>
            </form>
        </div>
    </modal>
</template>

<script>
import { required, minLength, email } from 'vuelidate/lib/validators'
import modal from '@/components/UI/Modal.vue'

export default {
    components: { modal },
    data(){
        return {
            name: '',
            email: ''
        }
    },
    validations: {
        name: {
            required,
            minLenght: minLength(4)
        },
        email: {
            required,
            email
        }
    },
    methods:{
        onSubmit() {
            this.$v.$touch()
            if(!this.$v.$invalid) {
                const user = {
                    name: this.name,
                    email: this.email
                }
                console.log(user)

                this.name = ''
                this.email = ''
                this.$v.$reset()
                this.$emit('close')
            }
        }
    }
}
</script>

<style lang="scss">
    .form-item .errorText {
        display: none;
        margin-bottom: 8px;
        font-size: 13.4px;
        color: #de4040;
    }

    .form-item {
        &.errorInput .errorText {
            display: block;
        }
    }
    input.error {
        border-color: #de4040;  
    }
</style>