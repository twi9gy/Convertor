<template>
    <div class="container-fluid">
        <div class="row justify-content-center">
            <div class="col-6">
                <div class="container">
                    <div class="row">
                        <div class="col">
                            <img v-bind:src = "imgsrc" class="img-fluid
                            img-thumbnail shadow p-2" />
                            <div class="container" style="margin-top: -50%">
                                <div class="row">
                                    <div class="col">
                                        <h1 class="text-white">Конвертер</h1>
                                    </div>
                                </div>
                                <div id = "computed_props" class="row p-2">
                                    <div class="col-6">
                                        <label class="text-white">{{label_from}}</label>
                                        <div class="input-group">
                                            <div class="input-group-prepend">
                                                <b-dropdown text="" >
                                                    <Item_unit
                                                            v-for="unit of units" :key="unit"
                                                            v-bind:unit="unit"
                                                            v-bind:type="0"
                                                            v-on:change_unit="change_unit"
                                                    />
                                                </b-dropdown>
                                            </div>
                                            <input id="number" v-model = "number" type="text" class="form-control"
                                                   placeholder="Введите число">
                                        </div>
                                    </div>
                                    <div class="col-6">
                                        <label class="text-white">{{label_in}}</label>
                                        <div class="input-group">
                                            <div class="input-group-prepend">
                                                <b-dropdown text="">
                                                    <Item_unit
                                                            v-for="unit of units" :key="unit"
                                                            v-bind:unit="unit"
                                                            v-bind:type="1"
                                                            v-on:change_unit="change_unit"
                                                    />
                                                </b-dropdown>
                                            </div>
                                            <input id="result" v-model="result" type="text" class="form-control"
                                                   readonly>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import Item_unit from "./Item_unit";

    export default {
        name: 'Converter',
        props: ['imgsrc', 'units'],
        data(){
            return{
                number: "",
                label_from: "Футы",
                label_in: "Метры"
            }
        },
        components: {
            Item_unit
        },
        methods:{
            change_unit(unit) {
                let tmp = this.label_in;
                if (unit[1]){
                    this.label_in = unit[0];
                    if (this.label_from === unit[0])
                        this.label_from = tmp;
                }
                else{
                    tmp = this.label_from;
                    this.label_from = unit[0];
                    if (this.label_in === unit[0])
                        this.label_in = tmp;
                }
                this.number = '';
            }
        },
        computed :{
            result : function() {
                if (this.label_from === "Футы" && this.label_in === "Метры")
                    return this.number * 0.3048;
                else if (this.label_from === "Футы" && this.label_in === "Версты")
                    return this.number * 0.0002857;
                else if (this.label_from === "Футы" && this.label_in === "Аршины")
                    return this.number * 0.4286;
                else if (this.label_from === "Метры" && this.label_in === "Футы")
                    return this.number / 0.3048;
                else if (this.label_from === "Метры" && this.label_in === "Версты")
                    return this.number * 0.0009374;
                else if (this.label_from === "Метры" && this.label_in === "Аршины")
                    return this.number * 1.4061;
                else if (this.label_from === "Аршины" && this.label_in === "Футы")
                    return this.number / 0.4286;
                else if (this.label_from === "Аршины" && this.label_in === "Метры")
                    return this.number / 1.4061;
                else if (this.label_from === "Аршины" && this.label_in === "Версты")
                    return this.number * 0.0006667;
                else if (this.label_from === "Версты" && this.label_in === "Футы")
                    return this.number / 0.0002857;
                else if (this.label_from === "Версты" && this.label_in === "Метры")
                    return this.number / 0.0009374;
                else if (this.label_from === "Версты" && this.label_in === "Аршины")
                    return this.number / 0.0006667;
                else
                    return '';
            }
        }
    }
</script>

<style scoped>
    h1, label{
        text-shadow: 1.5px 1px 2px dodgerblue;
    }
    label{
        font-size: 20px;
    }
</style>
