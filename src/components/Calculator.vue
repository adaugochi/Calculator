<template>
    <div class="row">
        <div class="col-md-4 mx-auto">
            <div class="container">
                <div class="content-wrapper">
                    <div class="content-output__wrapper">
                        <div class="content-output__value text-left">{{ currentValue }}</div>
                        <div class="content-output__answer text-right text-success">{{ result}}</div>
                    </div>
                    <div>
                        <div class="d-flex">
                            <div class="btn btn-light" @click="clear()">AC</div>
                            <div class="btn btn-light" @click="convertToPercentage">%</div>
                            <div class="btn btn-light" @click="getOperator('/')">/</div>
                            <div class="btn btn-danger" @click="deleteValue">DEL</div>
                        </div>
                        <div class="d-flex">
                            <div class="btn btn-light" @click="append(7)">7</div>
                            <div class="btn btn-light" @click="append(8)">8</div>
                            <div class="btn btn-light" @click="append(9)">9</div>
                            <div class="btn btn-secondary" @click="getOperator('+')">+</div>
                        </div>
                        <div class="d-flex">
                            <div class="btn btn-light" @click="append(4)">4</div>
                            <div class="btn btn-light" @click="append(5)">5</div>
                            <div class="btn btn-light" @click="append(6)">6</div>
                            <div class="btn btn-secondary" @click="getOperator('x')">x</div>
                        </div>
                        <div class="d-flex">
                            <div class="btn btn-light" @click="append(1)">1</div>
                            <div class="btn btn-light" @click="append(2)">2</div>
                            <div class="btn btn-light" @click="append(3)">3</div>
                            <div class="btn btn-secondary" @click="getOperator('-')">-</div>
                        </div>
                        <div class="d-flex">
                            <div class="btn btn-light" @click="dot">.</div>
                            <div class="btn btn-light" @click="append(0)">0</div>
                            <div class="btn btn-success" @click="getAnswer" @keyup.enter="getAnswer">=</div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'Calculator',
        data () {
            return {
                currentValue: '',
                result: 0,
            }
        },
        created: function () {
            window.addEventListener('keyup', (e) => {
                this.getAnswer(e);
            });
        },
        methods: {
            convertToPercentage() {
                if (this.currentValue === '') {
                    this.currentValue = this.result
                }
                this.result = parseFloat(this.currentValue) / 100;
                this.currentValue = ''
            },
            dot() {
                if (this.currentValue.indexOf('.') === -1) {
                    this.append('.')
                }
            },
            append(val) {
                this.currentValue += val;
            },
            deleteValue() {
                this.currentValue = this.currentValue.slice(0, -1)
            },
            clear() {
                this.currentValue = '';
                this.result = 0;
            },
            setPrevious(opr) {
                let sign = this.currentValue.slice(-1);
                let arrSign = ['+', '-', '*', '/'];
                if (this.currentValue === '') {
                    this.append(this.result);
                    this.append(opr)
                } else if (arrSign.includes(sign)) {
                    this.currentValue = this.currentValue.replace(sign, opr);
                } else {
                    this.append(opr)
                }
            },
            getOperator(opr) {
                switch (opr) {
                    case "+":
                        this.setPrevious(opr);
                        break;
                    case "-":
                        this.setPrevious(opr);
                        break;
                    case "x":
                        this.setPrevious('*');
                        break;
                    case "/":
                        this.setPrevious(opr);
                        break;
                    default:
                        console.log("default");
                }
            },
            getAnswer(e) {
                if (e.type === 'click' || e.keyCode === 13) {
                    this.result = parseFloat(eval(this.currentValue));
                    this.currentValue = '';
                }
            }
        },
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .content-wrapper {
        border: 1px solid #bbbbbb;
        padding: 5px;
    }
    .content-output__wrapper {
        padding: 30px 10px;
        font-size: 40px;
        margin: 5px;
        border-radius: 4px;
        box-shadow: 0 1px 3px rgba(0, 0, 0, 0.25);
    }
    .btn {
        outline: none;
        font-size: 18px;
        margin: 5px;
        padding: 15px 0;
        box-shadow: 0 1px 3px rgba(0, 0, 0, 0.25);
    }
    .btn-light, .btn-danger, .btn-secondary {
        width: 25%;
    }
    .btn-success {
        width: 50%;
    }
</style>
