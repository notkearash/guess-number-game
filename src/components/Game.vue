<template>
    <div class="game">
        <div class="text">
            <transition name="fade">
                <h1 v-if="started[0]">Guess the number.</h1>
            </transition>
            <transition name="fade">
                <p v-if="started[1]">{{ p }}</p>
            </transition>
            <transition name="fade">
                <form v-if="started[2]" onsubmit="return false">
                    <input
                        type="text"
                        name="number"
                        id="number"
                        autocomplete="off"
                        maxlength="3"
                        v-model="userInput"
                        :class="{ disabled: disabled }"
                    />
                    <button @click="validates" :class="{ disabled: disabled }">
                        Submit
                    </button>
                </form>
            </transition>
        </div>
    </div>
</template>

<script>
import { onMounted, ref } from "vue";

export default {
    setup() {
        // Private Variables
        let guessCount = 0;
        let messeges = [
            "guess a number between 1-100.",
            "Too big!",
            "Too small!",
            "You win!!",
        ];

        // Private Computed Variables
        function getRandomIntInclusive(min, max) {
            min = Math.ceil(min);
            max = Math.floor(max);
            return Math.floor(Math.random() * (max - min + 1) + min); //The maximum is inclusive and the minimum is inclusive
        }
        let answer = getRandomIntInclusive(1, 100);

        // Returned Variables
        let userInput = ref(0);
        let disabled = ref(false);
        let started = ref([false, false, false]);

        // Returned Computed Variables
        const printP = (messege) => {
            return messege + " Your total guesses: " + guessCount;
        };
        let p = ref(printP(messeges[0]));

        // Returned Methods
        const validates = () => {
            const standardInput = userInput.value;
            if (1 <= standardInput <= 100 && standardInput > answer) {
                guessCount++;
                p.value = printP(messeges[1]);
            } else if (1 <= standardInput <= 100 && standardInput < answer) {
                guessCount++;
                p.value = printP(messeges[2]);
            } else if (1 <= standardInput <= 100 && standardInput == answer) {
                guessCount++;
                p.value = printP(messeges[3]);
                disabled.value = true;
            } else {
                p.value = "WTF?! Enter a number between 1-100.";
            }
        };

        //Hooks
        onMounted(() => {
            setTimeout(() => {
                started.value[0] = true;
            }, 1000);
            setTimeout(() => {
                started.value[1] = true;
            }, 2000);
            setTimeout(() => {
                started.value[2] = true;
            }, 3000);
            console.log("mounted");
        });

        //Exporting
        return {
            userInput,
            disabled,
            started,
            p,
            validates,
        };
    },
};
</script>

<style scoped>
.game {
    background-color: #000;
    display: flex;
    width: 100%;
    flex-wrap: wrap;
    flex-direction: column;
    transition: all ease 0.3s;
}

.text {
    color: #fff;
    margin: 25px;
    position: relative;
    text-align: center;
    top: 25%;
}

h1 {
    font-size: 4rem;
    font-weight: bold;
}

input {
    border: none;
    border-bottom: #fff solid;
    background-color: #000;
    color: #fff;
    text-align: center;
    margin: 24px;
    min-width: 25%;
    font-size: 2rem;
    font-family: "Roboto Mono", monospace;
    outline: none;
}

input.disabled {
    pointer-events: none;
    background-color: #fff;
    color: #000;
    transition: all ease 0.3s;
}

button {
    border: none;
    padding: 12px;
    font-size: 18px;
    font-family: "Roboto Mono", monospace;
}

button:hover {
    padding: 10px;
    border: white solid 2px;
    color: white;
    background-color: black;
    font-size: 18px;
    font-family: "Roboto Mono", monospace;
    transition-duration: 0.4s;
}

button.disabled {
    padding: 10px;
    border: white solid 2px;
    color: white;
    background-color: black;
    font-size: 18px;
    font-family: "Roboto Mono", monospace;
    transition-duration: 0.4s;
    cursor: grab;
    transition: all ease 0.3s;
}

/* Animations */
.fade-enter-active,
.fade-leave-active {
    transition: all 1s ease;
}

.fade-enter-from,
.fade-leave-to {
    opacity: 0;
}
</style>
