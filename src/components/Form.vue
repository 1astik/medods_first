<template>
    <div>

        <success-component v-if="success" @close="success = false"></success-component>

        <div class="main-text">
            <h1>Форма создания клиента</h1>
        </div>
        <form class="form">
            <div class="form-group">
                <label for="second_name">Фамилия*</label>
                <input type="text" name="second_name" id="second_name" v-model.trim="person.second_name"
                       @blur="$v.person.second_name.$touch()"
                       class="form-control"
                       placeholder="Фамилия" :class="{'is-invalid': $v.person.second_name.$error}">
                <div class="invalid-feedback" v-if="$v.person.second_name.$error">Поле обязательно к заполнению</div>
            </div>

            <div class="form-group">
                <label for="p_name">Имя*</label>
                <input type="text" name="p_name" id="p_name" v-model.trim="person.p_name" @blur="$v.person.p_name.$touch()"
                       class="form-control"
                       placeholder="Имя" :class="{'is-invalid': $v.person.p_name.$error}">
                <div class="invalid-feedback" v-if="$v.person.p_name.$error">Поле обязательно к заполнению</div>
            </div>

            <div class="form-group">
                <label for="patronymic">Отчество</label>
                <input type="text" name="patronymic" id="patronymic" v-model.trim="person.patronymic"
                       class="form-control"
                       placeholder="Отчество">
            </div>

            <div class="form-group">
                <label for="p_name">Дата рождения*</label>
                <input type="date" name="date" id="date" v-model.trim="person.date" @blur="$v.person.date.$touch()"
                       class="form-control"
                       placeholder="Дата рождения" :class="{'is-invalid': $v.person.date.$error}">
                <div class="invalid-feedback" v-if="$v.person.date.$error">Поле обязательно к заполнению</div>
            </div>

            <div class="form-group">
                <label for="p_name">Номер телефона*</label>
                <input type="number" name="phone_number" id="phone_number" v-model.trim="person.phone_number"
                       @blur="$v.person.phone_number.$touch()"
                       class="form-control"
                       placeholder="Номер телефона" :class="{'is-invalid': $v.person.phone_number.$error}">
                <div class="invalid-feedback" v-if="$v.person.phone_number.$error && !$v.person.phone_number.required">Поле
                    обязательно к
                    заполнению
                </div>
                <div class="invalid-feedback" v-if="!$v.person.phone_number.minLength || !$v.person.phone_number.maxLength">Всего 11
                    символов
                </div>
                <div class="invalid-feedback" v-if="$v.person.phone_number.$error && !$v.person.phone_number.first">Первый символ 7
                </div>
            </div>

            <div class="form-group">
                <label for="gender">Пол</label>
                <input type="text" name="gender" id="gender" v-model.trim="person.gender"
                       class="form-control"
                       placeholder="Пол">
            </div>


            <div>
                <h4>Группа клиентов*</h4>
                <div class="form-group">
                    <label><input type="checkbox" @click="setGroup" id="VIP">VIP</label>
                </div>
                <div class="form-group">
                    <label> <input type="checkbox" id="Problem" @click="setGroup">Проблемные</label>
                </div>
                <div class="form-group">
                    <label><input type="checkbox" id="OMS" @click="setGroup">ОМС</label>
                </div>
            </div>

            <div>
                <h4>Лечащий врач</h4>
                <div class="form-group">
                    <select name="doc" class="custom-select" v-model="person.doc">
                        <option value="Ivanov">Иванов</option>
                        <option value="Zaharov">Захаров</option>
                        <option value="Chernyshova">Чернышева</option>
                        <option value="not_selected" >Выберите врача</option>
                    </select>
                </div>
            </div>


            <div class="form-group">
                <label for="sms"><input type="checkbox" name="sms" id="sms" v-model.trim="person.sms">Не отправлять СМС</label>
            </div>


            <div>
                <h2>Адрес:</h2>
                <div class="form-group">
                    <label for="index">Индекс</label>
                    <input type="text" name="index" id="index" v-model.trim="person.address.index"
                           class="form-control"
                           placeholder="Индекс">
                </div>
                <div class="form-group">
                    <label for="country">Страна</label>
                    <input type="text" name="country" id="country" v-model.trim="person.address.country"
                           class="form-control"
                           placeholder="Страна">
                </div>
                <div class="form-group">
                    <label for="oblast">Область</label>
                    <input type="text" name="oblast" id="oblast" v-model.trim="person.address.oblast"
                           class="form-control"
                           placeholder="Область">
                </div>
                <div class="form-group">
                    <label for="p_name">Город*</label>
                    <input type="text" name="city" id="city" v-model.trim="person.address.city"
                           @blur="$v.person.address.city.$touch()"
                           class="form-control"
                           placeholder="Город" :class="{'is-invalid': $v.person.address.city.$error}">
                    <div class="invalid-feedback" v-if="$v.person.address.city.$error && !$v.person.address.city.required">Поле
                        обязательно к заполнению
                    </div>
                </div>
                <div class="form-group">
                    <label for="street">Улица</label>
                    <input type="text" name="street" id="street" v-model.trim="person.address.street"
                           class="form-control"
                           placeholder="Улица">
                </div>
                <div class="form-group">
                    <label for="building">Дом</label>
                    <input type="text" name="building" id="building" v-model.trim="person.address.building"
                           class="form-control"
                           placeholder="Дом">
                </div>
            </div>

            <div>
                <h2>Паспорт:</h2>
                <div>
                    <h4>Тип документа*</h4>
                    <div class="form-group">
                        <select name="type" class="custom-select" v-model="person.passport.type">
                            <option value="passport">Паспорт</option>
                            <option value="rozhd">Свидетельство о рождении</option>
                            <option value="vodt">Вод. удостоверение</option>
                        </select>
                    </div>
                </div>
                <div class="form-group">
                    <label for="series">Серия</label>
                    <input type="text" name="series" id="series" v-model.trim="person.passport.series"
                           class="form-control"
                           placeholder="Серия">
                </div>
                <div class="form-group">
                    <label for="number">Номер</label>
                    <input type="text" name="number" id="number" v-model.trim="person.passport.number"
                           class="form-control"
                           placeholder="Номер">
                </div>
                <div class="form-group">
                    <label for="state">Кем выдан</label>
                    <input type="text" name="state" id="state" v-model.trim="person.passport.state"
                           class="form-control"
                           placeholder="Кем выдан">
                </div>
                <div class="form-group">
                    <label for="passport_date">Дата выдачи*</label>
                    <input type="date" name="city" id="passport_date" v-model.trim="person.passport.date"
                           @blur="$v.person.passport.date.$touch()"
                           class="form-control"
                           placeholder="Дата выдачи" :class="{'is-invalid': $v.person.passport.date.$error}">
                    <div class="invalid-feedback" v-if="$v.person.passport.date.$error && !$v.person.passport.date.required">Поле
                        обязательно к заполнению
                    </div>
                </div>
            </div>

            <button class="create-btn" :class="{'active-btn': !checkErrors()}" @click="send" :disabled="checkErrors()">Создать
            </button>

        </form>
    </div>
</template>

<script>
    import SuccessComponent from "./SuccessComponent";
    import {required, minLength, maxLength} from 'vuelidate/lib/validators';

    export default {
        name: "Form",
        components:{
            SuccessComponent
        },
        data() {
            return {
                success: false,
                person:{
                    p_name: '',
                    second_name: '',
                    patronymic: '',
                    date: '',
                    phone_number: '',
                    gender: '',
                    group_client: [],
                    doc: 'not_selected',
                    sms: false,
                    address: {
                        index: '',
                        country: '',
                        oblast: '',
                        city: '',
                        street: '',
                        building: ''
                    },
                    passport: {
                        type: 'passport',
                        series: '',
                        number: '',
                        state: '',
                        date: ''
                    }
                }

            }
        },
        validations: {
            person: {
                p_name: {
                    required,
                },
                second_name: {
                    required,
                },
                date: {
                    required,
                },
                phone_number: {
                    required,
                    minLength: minLength( 11 ),
                    maxLength: maxLength( 11 ),
                    first( phone_number ) {
                        return (
                            phone_number[0] === "7"
                        );
                    }
                },
                address: {
                    city: {
                        required
                    }
                },
                passport: {
                    date: {
                        required
                    }
                }
            }
        },
        methods: {
            checkErrors(){
                return !(this.$v.person.p_name.required && this.$v.person.second_name.required && this.$v.person.date.required && this.$v.person.address.city.required && this.$v.person.passport.date.required && this.$v.person.phone_number.required && !this.$v.person.phone_number.$error && this.person.group_client[0] !== undefined)
            },
            setGroup( e ) {

                const search = this.person.group_client.includes( e.target.id );
                if ( !search ) {
                    this.person.group_client.push( e.target.id )
                } else {
                    this.person.group_client = this.person.group_client.filter( item => {
                        return item !== e.target.id
                    } )
                }

            },
            send( e ) {
                e.preventDefault();

                console.log(this.person);
                this.success = true;
            }
        }
    }
</script>

<style lang="sass">
.main-text
    text-align: center
    h1
        margin: 0
        padding-top: 1rem

.form
    max-width: 600px
    margin: 0 auto
    padding: 2rem
    .create-btn
        color: #fff
        background-color: #007bff
        border-color: #007bff
        display: block
        width: 100%
        padding: .5rem 1rem
        font-size: 1.25rem
        line-height: 1.5
        border-radius: .3rem
        opacity: 60%
    .active-btn
        opacity: 100%
        &:hover
            cursor: pointer
            background-color: #0068d0


*
    box-sizing: border-box

    .form-group

        .custom-select
            display: block
            font-size: 16px
            font-family: sans-serif
            font-weight: 700
            color: #444
            line-height: 1.3
            padding: .6em 1.4em .5em .8em
            width: 100%
            max-width: 100%
            box-sizing: border-box
            margin: 0
            border: 1px solid #aaa
            box-shadow: 0 1px 0 1px rgba(0, 0, 0, .04)
            border-radius: .5em
            -moz-appearance: none
            -webkit-appearance: none
            appearance: none
            background-color: #fff
            background-image: url(data:image/svg+xml;charset=US-ASCII,%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20width%3D%22292.4%22%20height%3D%22292.4%22%3E%3Cpath%20fill%3D%22%23007CB2%22%20d%3D%22M287%2069.4a17.6%2017.6%200%200%200-13-5.4H18.4c-5%200-9.3%201.8-12.9%205.4A17.6%2017.6%200%200%200%200%2082.2c0%205%201.8%209.3%205.4%2012.9l128%20127.9c3.6%203.6%207.8%205.4%2012.8%205.4s9.2-1.8%2012.8-5.4L287%2095c3.5-3.5%205.4-7.8%205.4-12.8%200-5-1.9-9.2-5.5-12.8z%22%2F%3E%3C%2Fsvg%3E), linear-gradient(to bottom, #ffffff 0%, #e5e5e5 100%)
            background-repeat: no-repeat, repeat
            background-position: right .7em top 50%, 0 0
            background-size: .65em auto, 100%
            cursor: pointer

        .invalid-feedback
            width: 100%
            margin-top: .25rem
            font-size: 80%
            color: #9d0d00
        margin-bottom: 1rem

        label
            display: inline-block
            margin-bottom: .5rem




    .form-control
        display: block
        width: 100%
        height: calc(1.5em + .75rem + 2px)
        padding: .375rem .75rem
        font-size: 1rem
        font-weight: 400
        line-height: 1.5
        color: #495057
        background-color: #fff
        background-clip: padding-box
        border: 1px solid #ced4da
        border-radius: .25rem
        transition: border-color .15s ease-in-out, box-shadow .15s ease-in-out
    .is-invalid
        border: 1px solid red


</style>