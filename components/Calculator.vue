<template>
    <div class="container mx-auto justify-center w-96">
        <div class="flex m-10 p-10 w-2/2 h-4/4 justify-center bg-slate-400 px-4 rounded-md">
            <div class="grid grid-cols-4 gap-5">
                <div class="mb-6 col-span-4">
                    <label for="large-input"
                        class="block mb-2 text-sm font-semibold text-gray-900 dark:text-white">KIMSIO-5700FX</label>

                    <input type="text" id="large-input" v-model="number"
                        class="block w-full p-4 text-gray-900 border border-gray-300 rounded-lg bg-gray-50 sm:text-md focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500">
                </div>
                <button @click="clear()"
                    class="flex justify-center col-span-2 items-center hover:scale-110 bg-red-500 hover:bg-red-700 text-white font-bold py-2 px-4 rounded">
                    C
                </button>
                <button @click="remove()"
                    class="flex justify-center items-center hover:scale-110 bg-white hover:bg-gray-200 hover:text-black text-black font-bold py-2 px-4 rounded">
                    DEL
                </button>
                <button @click="addition()"
                    class="flex justify-center items-center hover:scale-110 bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
                    +
                </button>

                <button @click="append('1')"
                    class="flex justify-center items-center hover:scale-110 bg-gray-200 hover:bg-gray-500 hover:text-white text-black font-bold py-2 px-4 rounded">
                    1
                </button>
                <button @click="append('2')"
                    class="flex justify-center items-center hover:scale-110 bg-gray-200 hover:bg-gray-500 hover:text-white text-black font-bold py-2 px-4 rounded">
                    2
                </button>
                <button @click="append('3')"
                    class="flex justify-center items-center hover:scale-110 bg-gray-200 hover:bg-gray-500 hover:text-white text-black font-bold py-2 px-4 rounded">
                    3
                </button>
                <button @click="substraction()"
                    class="flex justify-center items-center hover:scale-110 bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
                    -
                </button>

                <button @click="append('4')"
                    class="flex justify-center items-center hover:scale-110 bg-gray-200 hover:bg-gray-500 hover:text-white text-black font-bold py-2 px-4 rounded">
                    4
                </button>
                <button @click="append('5')"
                    class="flex justify-center items-center hover:scale-110 bg-gray-200 hover:bg-gray-500 hover:text-white text-black font-bold py-2 px-4 rounded">
                    5
                </button>
                <button @click="append('6')"
                    class="flex justify-center items-center hover:scale-110 bg-gray-200 hover:bg-gray-500 hover:text-white text-black font-bold py-2 px-4 rounded">
                    6
                </button>
                <button @click="multiply()"
                    class="flex justify-center items-center hover:scale-110 bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
                    x
                </button>

                <button @click="append('7')"
                    class="flex justify-center items-center hover:scale-110 bg-gray-200 hover:bg-gray-500 hover:text-white text-black font-bold py-2 px-4 rounded">
                    7
                </button>
                <button @click="append('8')"
                    class="flex justify-center items-center hover:scale-110 bg-gray-200 hover:bg-gray-500 hover:text-white text-black font-bold py-2 px-4 rounded">
                    8
                </button>
                <button @click="append('9')"
                    class="flex justify-center items-center hover:scale-110 bg-gray-200 hover:bg-gray-500 hover:text-white text-black font-bold py-2 px-4 rounded">
                    9
                </button>
                <button @click="divide()"
                    class="flex justify-center items-center hover:scale-110 bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
                    /
                </button>


                <button @click="append('0')"
                    class="flex justify-center items-center hover:scale-110 bg-gray-200 hover:bg-gray-500 hover:text-white text-black font-bold py-2 px-4 rounded">
                    0
                </button>
                <button @click="dot()"
                    class="flex justify-center items-center hover:scale-110 bg-gray-200 hover:bg-gray-500 hover:text-white text-black font-bold py-2 px-4 rounded">
                    .
                </button>
                <button @click="equal()"
                    class="flex justify-center items-center hover:scale-110 bg-blue-500 hover:bg-blue-700 col-span-2 text-white font-bold py-2 px-4 rounded">
                    =
                </button>
            </div>
        </div>
    </div>
</template>

<script>
import { remove } from '@vue/shared';

export default {
    name: 'Calculator',
    props: {
        msg: String
    },
    data() {
        return {
            number: '',
            prevNum: null,
            operator: null,
            opetaorClicked: false
        }
    },
    methods: {
        clear() {
            this.number = '';
        },
        append(num) {
            if (this.opetaorClicked) {
                this.number = '';
                this.opetaorClicked = false;
            }
            this.number = `${this.number}${num}`;
        },
        remove() {
            this.number = this.number.slice(0, -1);
        },
        setPrevNum() {
            this.prevNum = this.number;
            this.opetaorClicked = true;
        },
        dot() {
            if (this.number.indexOf('.') === -1);
            this.append('.');
        },
        addition() {
            this.append('+');
            this.operator = (a, b) => a + b;
            this.setPrevNum();
        },
        substraction() {
            this.append('-');
            this.operator = (a, b) => a - b;
            this.setPrevNum();

        },
        multiply() {
            this.append('x');
            this.operator = (a, b) => a * b;
            this.setPrevNum();
        },
        divide() {
            this.append('/');
            this.operator = (a, b) => a / b;
            this.setPrevNum();
        },
        equal() {
            this.number = `${this.operator(
                parseFloat(this.prevNum),
                parseFloat(this.number)
            )}`;
            this.setPrevNum;
        }
    }
}
</script>