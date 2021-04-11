<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-8">
                <div class="card">
                    <div class="card-header">Example Component</div>
                    <div class="card-body">
                        <p v-model="summMainDiagonal">Сумма главной диагонали - <strong>{{summMainDiagonal}}</strong></p>
                        <p v-model="summSideDiagonal">Сумма дополнительной диагонали - <strong>{{summSideDiagonal}}</strong></p>
                        <p>
                            <label>Введите размер матрицы:</label>
                            <input id="numsize" type="number" name="numsize" value="">
                            <button @click="reSumm()">Пересчитать</button>
                        </p>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        props: ['allusers'],
        data: () => ({
            matrixSizeDefault: 5,
            matrixSizeCustom: null,
            summMainDiagonal: 0,
            summSideDiagonal: 0,
            matrix: null
        }),
        mounted() {
            let self = this
            this.matrix = this.matrixArray(this.matrixSizeDefault)
            console.log(this.matrix)
            this.summMainDiagonal = this.summMine(this.matrix)
            this.summSideDiagonal = this.summSide(this.matrix)
        },
        created() {

        },
        methods:{
            matrixArray(size){
                let self = this
                let rows = size
                let columns = size
                let arr = [];
                let count = this.allusers.length
                for(let i=0; i<rows; i++){
                    arr[i] = [];
                    for(let j=0; j<columns; j++){
                        if (count > 0) {
                            arr[i][j] = this.allusers[j].id
                        } else {
                            arr[i][j] = 0
                        }
                        count = count - 1
                    }
                }
                return arr;
            },
            summMine(arr){
                let sum = arr.reduce((total,current, idx) => total + (current[idx] || 0) , 0);
                return sum;
            },
            summSide(arr){
                let sum = arr.reduce((total,current, idx) => total + (current[current.length - idx - 1] || 0) , 0);
                return sum;
            },
            reSumm(){
                let size = document.getElementById('numsize').value
                this.matrix = this.matrixArray(size)
                console.log(this.matrix)
                this.summMainDiagonal = this.summMine(this.matrix)
                this.summSideDiagonal = this.summSide(this.matrix)
            }
        }
    }
</script>
