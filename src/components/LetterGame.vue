<template>
    <button @click="reset">Start Over</button>
    <h2>{{ letter1 }}</h2>
    <div><button @click="answerBefore">Before</button> or <button @click="answerAfter">After</button></div>
    <h2>{{ letter2 }}</h2>
    <p>{{ `${letter1} ${isBefore ? 'comes' : 'does not come'} before ${letter2}` }}</p>
    <label for="score">score:</label>
    <p>{{ score }}</p>
</template>

<script>
    export default {
        name: 'LetterGame',
        data() {
            return {
                letter1: '',
                letter2: '',
                isBefore: null,
                answer: '',
                score: 0,
            }
        },
        mounted() {
            this.generateLetters();
        },
        methods: {
            generateLetters() {
                const alphabet = "abcdefghijklmnopqrstuvwxyz".toUpperCase();
                let l1, l2;
                
                do {
                    l1 = alphabet[Math.floor(Math.random() * alphabet.length)];
                    l2 = alphabet[Math.floor(Math.random() * alphabet.length)];
                } while (l1 === l2);
                
                this.letter1 = l1;
                this.letter2 = l2;
                
                this.isBefore = l1.charCodeAt(0) - l2.charCodeAt(0) < 0;
            },
            answerBefore() {
                if (this.isBefore) this.score++;
                else this.score--;
                this.generateLetters();
            },
            answerAfter() {
                if (!this.isBefore) this.score++;
                else this.score--;
                this.generateLetters();
            },
            reset() {
                this.score = 0;
                this.generateLetters();
            }
        }
    }
</script>